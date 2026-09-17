# LinkedIn Comment Threading Rules

## Two-level flattening

LinkedIn's UI shows replies two levels deep. Every reply, no matter how many logical turns into a conversation, is stored with `parentComment` pointing to the TOP-level comment.

```
Post (urn:li:activity:P)
│
├─ Comment A (id: 111)             ← top-level
│    parentComment: none
│    URN: urn:li:comment:(urn:li:activity:P, 111)
│
│  ├─ Reply B (id: 222)             ← 2nd-level
│  │    parentComment: urn:li:comment:(urn:li:activity:P, 111)
│  │
│  └─ Reply C (id: 333)             ← STILL 2nd-level (under Comment A)
│       parentComment: urn:li:comment:(urn:li:activity:P, 111)
│       (NOT under Reply B, even if logically C replies to B)
│
└─ Comment D (id: 444)             ← top-level
     parentComment: none
```

## Posting rule

When calling `POST /linkedin-comments` with `parentComment`:
- If you're replying to a top-level comment → `parentComment` = that comment's URN
- If you're replying to a 2nd-level reply → `parentComment` = the TOP-level comment's URN (walk up the tree)
- If `parentComment` is omitted, the comment posts as top-level

## Why this matters

Wrong parentComment URN causes one of these:
- 400 Bad Request (some posts reject it outright)
- Comment silently posted under the wrong parent (user sees it in the wrong place)
- Comment gets orphaned if the 2nd-level URN is rejected

## Deriving the TOP-level comment URN

This is a two-step pipeline, not two competing ways to do the same thing:

1. **Find which id is top-level.** When given a 2nd-level reply's id, walk the
   fetched comment tree to find which top-level comment it sits under. The
   function below is illustrative pseudocode for that walk — it does not exist
   in `lib/`, it just shows the logic this skill's steps describe in prose
   (SKILL.md carries `top_level_comment_id` through the reply queue for this
   exact reason, so the walk only has to happen once per comment, not once per
   draft):

   ```python
   def find_top_comment_urn(post_urn: str, comment_id: str, post_comments: list) -> str:
       for top in post_comments:  # each element is a top-level comment dict
           if top["id"] == comment_id:
               return f"urn:li:comment:({post_urn},{comment_id})"
           for reply in top.get("replies", []):
               if reply["id"] == comment_id:
                   return f"urn:li:comment:({post_urn},{top['id']})"
       raise ValueError("Comment not found in tree")
   ```

2. **Build the actual URN string.** Once you have the top-level id (from the
   walk above, or already carried as `top_level_comment_id`), the real,
   callable function is `lib.url_parser.build_parent_comment_urn(post_urn,
   top_level_comment_id)` — this is what SKILL.md's steps actually call. It
   only builds the string; it does not do the walk, which is why both exist.

## URL formats the skill accepts

**Direct top-level comment permalink:**
```
https://www.linkedin.com/feed/update/urn:li:activity:P?commentUrn=urn%3Ali%3Acomment%3A%28activity%3AP%2C111%29
```

**Reply permalink (notice `replyUrn` query):**
```
https://www.linkedin.com/feed/update/urn:li:activity:P?commentUrn=urn%3Ali%3Acomment%3A%28activity%3AP%2C111%29&replyUrn=urn%3Ali%3Acomment%3A%28activity%3AP%2C222%29
```

When `replyUrn` is present, that's the specific comment being replied to (for reactions). The `commentUrn` is already the top-level parent.

## Reaction targets

Reactions can land on the post itself or on any comment or reply — Publora's
`create_reaction` takes this as `target_urn` (renamed from the confusingly
named `post_urn` it used to be called, since the value is frequently a
comment's URN, not a post's).

Default flow: react on the specific comment being replied to, never on the
post. In `lib.publish(kind="reply", ...)`, that means passing `react_target`
explicitly as the comment/reply's own URN — `parent_comment` is always the
top-level comment's URN (required for posting), which is only the *same*
value as the reaction target when the reply is to a top-level comment
directly. Replying to a 2nd-level reply and omitting `react_target` reacts on
the top-level comment instead of the one actually being replied to. Never
skip the reaction entirely — a pure reply with no reaction reads as
transactional.

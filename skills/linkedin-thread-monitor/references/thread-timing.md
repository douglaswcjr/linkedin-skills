# Thread Timing Matrix

## Thread stage classification

This is the single source of truth for stage names and thresholds —
`SKILL.md` cites this table rather than redefining it.

**When the author has replied**, the stage is driven entirely by how recent
that reply is, not by the age of the original comment:

| Time since author's reply | Stage | Priority |
|---|---|---|
| <2h | **Hot** — respond within 90 min | HIGH |
| 2-12h | **Warm** — respond within 2h | HIGH |
| 12h+, but the thread's last turn is still <72h old | **Cool** — respond within 4h | Medium |
| Thread's last turn is >72h old | **Dormant** — switch to DM | Medium (if inbound-quality) |

**When the author has not replied yet**, the stage is driven by the age of
the user's own comment:

| Time since user's comment | Stage | Priority |
|---|---|---|
| <6h | **Watch** — author may still reply, check back | Low |
| 6-24h | **Cold** — skip, past the peak-reply window | — |
| >24h | **Dormant** — switch to DM if inbound-quality | — |

## The peak-reply window explained

Not to be confused with the "Warm" stage above — this is a different axis:
when authors *tend* to reply at all (population behavior), not how fast you
should follow up once one actually does.

Real example from 2026-04:
- 14:27 UTC: the user posted a comment on a CEO's post ("moat moved from tools to taste")
- 12:06 UTC next day (~22h later): the author replied personally ("How are you building that conviction muscle with your team?")
- 16:24 UTC that day (~28h after original comment, ~4h after the author's reply): the user replied with their answer

This is the exact window the skill targets. Miss it by 12+ hours and the reply lands in a dormant thread where the author doesn't get the notification prominently.

## First 60 min on own posts

Different metric — how fast the USER replies to comments on their own posts:
- Target: every comment replied to within 5-15 min during first 60 min
- Each reply within 90 min fires ~90% boost on that thread
- 3+ substantive comments in first 30 min = second algo push

## Engagement half-life

- **0-6h:** 70% of all eventual reactions/comments happen here
- **6-24h:** 25% — the long tail
- **24-72h:** 5% — trickle
- **>72h:** essentially dead (<1% of eventual engagement)

## Rule: when thread dies, switch to DM

If a thread is dormant (>72h since last turn) but the counterpart was high-quality, don't reply in thread — the post won't surface their notification. Instead, draft a DM:

```
[Name] — circling back on our thread about [specific topic from thread].

[Your one new thought or data point].

Worth a 15-min conversation? Tuesday or Thursday this week if yes.
```

The DM should reference the thread specifically, not be a generic pitch.

## Anti-patterns

- Chaining 3+ replies under one top comment (looks like thread hijack)
- Replying after 72h in the thread itself (low visibility, looks desperate)
- Generic "catching up on this thread" without a new thought
- DMing before the public thread closes naturally (skips the earned step)
- Replying to replies OF replies (LinkedIn flattens — it doesn't nest that deep)

## Publishing-adjacent timing windows (own posts)

| Phase | Window | Action |
|---|---|---|
| Warm-up | 15 min **BEFORE** publishing | Leave 3-5 substantive comments on others' posts |
| Critical | First 30 min AFTER publishing | Reply to every comment within minutes; distribution contracts if dead |
| Seeding | 15-30 min after posting | Leave 3-5 bonus comments on your own post to create thread depth |
| Visibility bump | Reply within 1st hour | +35% visibility lift (author-reply signal) |

## Peer engagement (safe pattern, not a pod)

A **safe peer group** is 5-8 people in adjacent fields who actually read each other's work and comment only when they have something substantive to say.

Distinguishes from pods by:
- Varied timing (no fixed daily slot)
- Varied commenters per post (not the same 6 people every time)
- Comment substance >10 words, with new angles
- No reciprocity obligation

Pod detection catches:
- Same accounts engaging at the same clock minute daily (e.g., 9:01 AM)
- 15+ comments landing within a 90-second window
- Identical like/comment pattern across every post

Real penalty observed: one creator dropped from 8,500 to 340 impressions overnight after pod detection. Recovery: 6-8 weeks.

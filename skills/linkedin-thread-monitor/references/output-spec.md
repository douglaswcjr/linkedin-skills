# Mode 1. Thread monitoring — output spec

Canonical sample outputs for the daily thread-monitoring report. See `SKILL.md` for the workflow steps.

## Daily report

| Posted | Author | Post | Comment | Reply? | Stage | Action |
|---|---|---|---|---|---|---|
| 18h ago | Author A | SaaS Co. | "moat moved to taste" | author replied 14h ago | Cool (reply 12h+ ago) | Reply within 4h |
| 20h ago | Author D | DevTools Inc. | "flip the default" | author replied 5h ago | Warm (reply 2-12h ago) | Reply within 2h |
| 22h ago | Author B | Enterprise SaaS | "integration depth moat" | No | Cold | Skip |
| 3h ago | Author C | AI vendor | "twin economies" | No | Watch | Check in 3h |

## For each warm thread

- Thread preview (last 3 turns)
- Suggested response (drafted via `linkedin-reply-handler`)
- Reaction target (the specific reply URN, not the post)
- Priority (high / medium / low)

## Weekly roll-up

- Total comments posted
- Author-reply rate (target 15%+)
- Conversion to DM (when thread closes warm)

## Example run

> Input: monitor your-handle profile, last 24h

> Output:
> - 1 warm thread: the author replied 5h ago on their post. Current stage: Warm (reply 2-12h ago). Suggested response ready. Action: post within 2 hours.
> - 1 cool thread: the author replied 14h ago. Current stage: Cool (reply 12h+ ago). Action: reply within 4h.
> - 8 cold threads (no author engagement, 6-24h old). Skip.
> - 3 watching threads (<6h old, author may still reply). Check again in 3-6h.

# Examples — LinkedIn Post Audit

## Example

> Input: "In today's fast-paced world, businesses are fundamentally leveraging AI to unlock massive ROI — here's what I learned..."

> Output:
> - **FAIL** (2 blockers)
> - L1 "In today's fast-paced world" (filler opener, check #4)
> - L1 "fundamentally", "leveraging", "unlock" — 3 vocabulary/grammar markers in one sentence, over the 3+ density threshold (check #6). Counted as one blocker for the paragraph, not three separate ones
> - Not a blocker: the em dash. One em dash in a short post is explicitly fine (check #1) — flagging it here would be wrong
> - **Suggested rewrite:** "Businesses are using AI to cut costs 40%. Here's what I learned."

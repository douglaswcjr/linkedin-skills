# Mode 2. Engager analytics — output spec

Canonical sample outputs for the engager-analytics report. See `SKILL.md` for the workflow steps.

## Engager roster

| # | Type | Name | Title | Company | Profile | ICP tier |
|---|---|---|---|---|---|---|
| 1 | commenter | Author A | Director | Cosmetics Co | linkedin.com/in/... | Prospect |
| 2 | commenter | Author B | Senior PM | Enterprise SaaS Co | linkedin.com/in/... | Aspirational |
| 3 | liker | Author C | Founder | Solo brand LLC | linkedin.com/in/... | Peer |

## Tier breakdown

| Tier | Definition | Count | % of total |
|---|---|---|---|
| Peer | Founder / operator at company in same niche, 5-50 employees | 12 | 24% |
| Aspirational | Senior leader at 50+ company in adjacent niche | 9 | 18% |
| Prospect | Director / C-suite at company matching ICP | 18 | 36% |
| Other | Doesn't fit any tier | 11 | 22% |

## Action lists

Each capped at `top_n` (default 5 — see `SKILL.md` Input):

- **Follow back** (peers worth reciprocal engagement): top `top_n` by activity
- **Comment-drop targets** (aspirational creators with their own posts): top `top_n`
- **DM-able prospects** (with the rationale): top `top_n`, filtered against Inbound-quality signals first, with one-line opener seed

## Example run

> Input: analyze engagers on two post URLs from this week (`https://www.linkedin.com/posts/<author>_...-A` and `...-B`), max 100 each

> Output:
> - 50 commenters fetched per post ($0.25 each, $0.50 total)
> - Tier split: 6 Peer / 14 Aspirational / 18 Prospect / 12 Other
> - 3 cross-post engagers detected (engaged with both posts supplied in this run)
> - Top 5 DM-able prospects with one-line openers attached

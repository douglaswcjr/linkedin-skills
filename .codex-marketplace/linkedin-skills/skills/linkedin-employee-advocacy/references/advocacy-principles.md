# Employee Advocacy — Four Operating Principles

The 8x/6-8x figures below trace to MSLGroup research on employee vs. brand-page content, echoed in LinkedIn's own marketing data — commonly cited, not independently reproduced at that exact magnitude by anyone outside that research. Everything else here is 2026 practitioner consensus, not a single cited study; treat the specific numbers as working targets to calibrate against your own program's data, not as guaranteed outcomes.

## 1. Scale authentically

Individuals compose in **their own voice**, not corporate language.

- Team-written copy that sounds like the brand = 3x lower engagement than personal voice
- Use a short voice-capture interview at onboarding (5-10 min) to document each person's tone
- Don't normalize — keep the variance. The person who curses occasionally stays that way. The one who writes in technical prose stays that way.

**Litmus test:** if someone reads 5 random posts from your team and can tell which person wrote each one, you're doing it right.

## 2. Maintain control

Brand guidelines integrated into the workflow. Review is **risk-based, not role-based, and never blocks the voice.**

Full 3-tier queue and SLAs: `governance-playbook.md` — that file is the source of truth for this principle. Summary: a post routes on what it *contains* (names a customer, cites an internal number, critiques a competitor, touches a regulated topic), not on who wrote it.

- **Tier A — auto-publish:** no specific claim about customers, financials, roadmap, or competitors
- **Tier B — 24h SLA, silent-approval after 24h:** names a customer, cites an internal number, critiques a named competitor, announces something unannounced
- **Tier C — 48h SLA, explicit go/no-go:** regulated topics, forward-looking statements, active legal/PR matters

**What seniority actually changes:** a VP or Director writing low-risk (Tier A) content all day never touches a queue — in practice that's most of what they post, so it *feels* like a bypass. But the same VP citing an internal revenue number lands in Tier B/C exactly like anyone else. New hires default to review on everything for the first 4 weeks regardless of tier, then follow the normal risk-based routing.

**What the review catches:**
- Factual errors about products / customers
- Confidential info leaks
- Regulatory issues (finance, health, disclosure rules)

**What the review does NOT change:**
- Voice, tone, formatting
- Opinions the team member has about their own work
- Topic selection (within pillars)
- Hashtags, emoji

## 3. Remove friction

Per-post time budget: **5 minutes**. Anything more and the program dies by week 3.

- AI does heavy lifting: ideation, drafts, visual suggestions
- Team member reviews, edits, approves, publishes
- Approval workflow is async: 0 min for Tier A (most content), 24h/48h SLA for Tier B/C — see `governance-playbook.md`
- Mobile posting is a first-class path (not desktop-only)

**Math:** 5 min/post × 3 posts/week × 11 people = **2.75 hrs total team time per week** for full program output.

## 4. Prove ROI

Track team reach, engagement, and pipeline impact. Without attribution, the program gets cut at the first budget review.

### The 3 KPIs

- **Team reach** — sum of impressions across all creators
- **Team engagement** — comments + reactions + shares
- **Pipeline impact** — inbound DMs, meetings booked, closed-won deals with LinkedIn as first-touch

### What NOT to use as primary KPI

- Follower count (vanity, slow-moving)
- Post frequency (effort, not outcome)
- Hashtag performance (not a business metric)

## Benchmarks (2026)

- Launch → first team post: **14 days** target
- Active team size: **8-11** members for meaningful output
- Team output: **23-40 posts/week** at 8 members (2.9-5 posts/person/week — see the worked example below; a number like "70+ posts/week" doesn't reconcile with the 5-minute time budget or with per-person cadence anywhere in this bundle, so don't use it)
- Per-post time: **5 min** max
- Team touchpoints: **40,000/month** at 11 people × 3 posts/week × 300-impression floor
- Per-post impression floor: **300** (anything lower, audit profile/hook)
- Employee vs. brand page: **8x engagement**, **6-8x reach**

## Example team config

```yaml
team:
  VP Marketing (author: Alice):
    cadence: 2 posts/week
    review: Tier A by default (most of her content); Tier B/C if a post meets the risk criteria, same as anyone
    pillars: [thought leadership, contrarian takes]
  Senior PMM (author: Bob):
    cadence: 3 posts/week
    review: Tier A by default; Tier B/C if a post meets the risk criteria
    pillars: [product positioning, competitive teardowns]
  Marketing Manager (author: Carol):
    cadence: 3 posts/week
    review: Tier A by default; routes to Tier B (24h SLA) more often given her pillars name customers
    pillars: [campaign recaps, customer wins]
  Content Writer (author: Dan):
    cadence: 4 posts/week
    review: Tier A by default; Tier B/C if a post meets the risk criteria
    pillars: [industry analysis, frameworks]
  ... (5 more team members)

weekly_output: 23 posts total from 8 members
weekly_time_cost: 1.9 hours
target_team_reach: 15,000 impressions/week (growing toward 40,000/month)
```

## Pillar × person matrix

The "all-same pillars kills reach" anti-pattern (see `../SKILL.md`) needs a way to check it before cadence locks (Day 11 of the launch playbook), not after reach quietly drops. Lay out everyone's pillars in one table and scan for overlap:

| Person | Pillar 1 (primary) | Pillar 2 |
|---|---|---|
| Alice (VP Marketing) | Thought leadership | Contrarian takes |
| Bob (Senior PMM) | Product positioning | Competitive teardowns |
| Carol (Marketing Manager) | Campaign recaps | Customer wins |
| Dan (Content Writer) | Industry analysis | Frameworks |

**Rule:** no two people share a Pillar 1. A shared Pillar 2 is fine if the angle differs (two people can both touch "customer wins" if one covers enterprise and the other SMB) — it's a full overlap across someone's *entire* pillar set that produces the redundancy the anti-pattern warns about. Catch it here, before launch, not from a reach report six weeks in.

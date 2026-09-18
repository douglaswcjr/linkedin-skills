---
name: linkedin-employee-advocacy
description: "Stand up and run a LinkedIn employee advocacy program for a marketing or sales team. Covers 14-day launch playbook, brand-guideline governance, per-post time budget, cadence benchmarks, and team ROI (reach, engagement, pipeline). Triggers on \"employee advocacy\", \"get the team posting\", \"scale LinkedIn across team\", \"advocacy ROI\". Not for planning one person's own calendar (use linkedin-content-planner)."
---

# LinkedIn Employee Advocacy

Stand up a marketing-team LinkedIn advocacy program that scales without killing authenticity. Employee posts get **8x more engagement** than brand-page posts (MSLGroup research, echoed in LinkedIn's own marketing data — commonly cited, not independently reproduced at that exact magnitude) — this skill operationalizes that advantage.

## When to use

- Marketing leader wants to get their team posting on LinkedIn
- User is planning an advocacy program launch
- Team is posting but output is inconsistent / off-brand / low-engagement
- Need ROI measurement framework for an existing program
- Requests: "how do I get the team posting", "launch advocacy", "scale LinkedIn across 10 people"

## Input

- Team size (5-50 typical)
- Marketing goal (reach / pipeline / recruiting / thought leadership)
- Current state (everyone silent / some active / inconsistent)
- Brand guideline constraints

## Output

- **14-day launch plan** (if cold-starting)
- **Operating model** (voice capture, ideation, approval, posting, measurement)
- **Cadence targets** per team member (realistic, not punishing)
- **KPI dashboard spec** (team reach, engagement, pipeline attribution)
- **Governance playbook** (brand safety without blocking velocity)

## Four operating principles

Scale authentically (individual voice, never corporate tone), maintain control (review the risk surface, never the voice — see Governance below), remove friction (5-minute per-post time budget), prove ROI (reach + engagement + pipeline, or the program gets cut at the first budget review). Full detail and the reasoning behind each: `references/advocacy-principles.md` — that file is the single source of truth for these; don't restate numbers here that could drift out of sync with it.

## Benchmarks

Launch target **14 days**, per-post time budget **5 minutes** — used directly in the playbook below. Every other number (team size, output range, touchpoint math, employee-vs-brand-page reach) lives in `references/advocacy-principles.md`.

## 14-day launch playbook

### Days 1-3: Voice capture
- Short interview with each team member (5-10 min) to extract their actual voice
- Identify their domain expertise and 2-3 content pillars
- Set realistic individual cadence (some commit to 1/week, some 3/week — don't force uniformity)

### Days 4-7: First posts
- Everyone ships their first post, drafted in their voice
- Marketing reviews only for brand safety (never for style)
- Celebrate every first post internally — social proof unlocks the next team member

### Days 8-10: Ideation pipeline
- Set up a shared ideation source (newsletter digest, trending-topics feed, internal wins)
- Each team member gets 5-10 topic suggestions per week
- They pick, not assigned

### Days 11-14: Early cadence (ramp week 3-4 level)
- This is still weeks 3-4 of the 60-day ramp in `references/team-cadence-matrix.md`: **1 post/week per seat**, fixed days/times, not steady-state — full cadence doesn't start until week 9+ (day 57+).
- Before locking anyone's pillars, run the pillar × person matrix (`references/advocacy-principles.md`) — no two people should share a Pillar 1, or the "all-same pillars" anti-pattern below is already baked into week 1.
- Set up KPI dashboard (see below)
- Run first weekly review

## Governance: brand-safe without being blocked

Full 3-tier queue, SLAs, and what reviewers must never touch: `references/governance-playbook.md`. Summary:

- **Tier A — 0 min, auto-publish (~70-80% of content):** personal opinion, no specific claim about customers, financials, roadmap, or competitors.
- **Tier B — 24h SLA, silent-approval after 24h (~15-25%):** names a customer, cites an internal number, critiques a named competitor, announces something unannounced.
- **Tier C — 48h SLA, explicit go/no-go (<5%):** regulated topics, forward-looking statements, an active legal or PR matter.

**Tier is set by what the post contains, not who wrote it.** A VP citing an internal revenue number still routes to Tier B/C. Seniority only changes how much *low-risk* content a person is trusted to publish without ever hitting a queue — it is not an unconditional bypass on higher-risk content.

**What marketing does NOT review, at any tier:** voice, tone, formatting, hashtags, emoji, or topic selection within pillars.

## ROI measurement

### Per-person metrics (content quality)
- Impressions per post
- Engagement rate (reactions + comments + shares / impressions)
- Comments (depth signal)
- Profile views attributed to post

### Team-level metrics (program health)
- Total team reach
- Total team engagement
- Individual contribution rank (leaderboard)
- Active members / total members (participation rate)

### Business metrics (pipeline impact)
- Inbound DMs sourced from LinkedIn content
- Meetings booked from LinkedIn
- Closed-won deals with LinkedIn as first-touch channel
- Employee referrals sourced from LinkedIn (if recruiting is a goal)

## Anti-patterns

- **Copy-paste corporate posts across team accounts** — LinkedIn detects this, suppresses all of them
- **Ghostwriting that erases the writer's voice** — reads as fake
- **Mandatory posting cadence without individual calibration** — program dies in 6 weeks
- **Tier-B approval loops >24h** — makes the program feel like work (Tier C's 48h is a deliberate exception for regulated/legal content, not a violation of this rule)
- **Measuring only vanity metrics** — program gets cut without pipeline attribution
- **All-same pillars across team** — redundancy kills team reach (360Brew penalizes clustering)

## Resources

- `references/advocacy-principles.md` — the 4 operating principles with examples, benchmarks, and the pillar × person matrix
- `references/team-cadence-matrix.md` — realistic cadence by role + seniority
- `references/governance-playbook.md` — what to review, what not to, SLA

## Related skills

- `linkedin-post-writer` — each team member uses this for individual drafts
- `linkedin-profile-optimizer` — team profiles should match before the program launches (otherwise profile clicks convert poorly)
- `linkedin-content-planner` — each team member gets their own pillar mix
- `linkedin-thread-monitor` — track which team members' comments drive author replies
- `linkedin-engager-analytics` — see who's engaging with each team member's posts
- `linkedin-comment-drafter` — its **reshare mode** is how team members amplify a brand or colleague post to their own feed with a short take (`lib.repost(post_url, commentary)` on approval); the cleanest advocacy action after an original post

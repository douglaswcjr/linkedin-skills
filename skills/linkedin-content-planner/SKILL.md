---
name: linkedin-content-planner
description: "Generate a 7-day LinkedIn content plan from a theme, audience, and pillars. Produces per-day post pillar, format, hook type, CTA, posting time, daily comment targets, and a weekly inbound-readiness check. Use when the user wants to plan a week or month of content, not draft a single post (use linkedin-post-writer)."
---

# LinkedIn Content Planner

Produce a 7-day LinkedIn plan built around the 3-pillar discipline (Authority 40-50%, Personal Narrative 30-40%, Community 20-30%). Optionally adds a Product/Offer pillar at 10-15%.

## When to use

- User asks "plan my week" or "what should I post this week"
- User wants to escape ad-hoc shipping and establish rhythm
- Before a launch week (user needs product-pillar alignment)
- An account is recovering from dormancy, a shadowban, or a pod-detection penalty (routes to the recovery protocol instead of the standard calendar; see below)

## Input

- **Theme** (optional): e.g., "AI agents shipping in production", "first 6 months of a pre-seed launch"
- **Audience description:** e.g., "B2B founders, AI ops leaders, marketing VPs"
- **Persona** (optional): Founder / Executive / Sales / Marketing / Generic. Picks the default pillar mix from `references/pillars-framework.md` § Persona-specific pillar mixes (Founder uses the dedicated founders edition below) instead of the flat 40/30/20/10. Ask directly if the audience description implies one of these roles and the user hasn't said which.
- **Pillar mix** (optional): overrides the persona default; defaults to 40% Authority / 30% Narrative / 20% Community / 10% Product when no persona is given
- **Posting days** (optional): defaults to Tue/Wed/Thu/Fri (4 posts). Monday defaults to a comment-only day regardless of which posting days are chosen; it never gets a slot in the calendar unless the user explicitly asks for a 5th post that week.
- **Follower count** (optional): calibrates comment-volume target and format mix per `references/pillars-framework.md` § Growth-stage playbook. Under 1,000: weight toward commenting over posting (10-15 comments/day) and don't worry about post frequency. 1,000-10,000: 3-4 posts/week, carousels perform best. 10,000+: 1-2 long-form/week plus daily short takes. Defaults to the 5k-20k band's targets (10-20 comments/day) when not given.
- **Recovering account?** (optional, yes/no): if yes, switch to the Recovery mode output below instead of a standard weekly calendar.
- **Voice profile** (optional, auto-loaded): if `../../references/voice-profile.md` has `filled: yes`, match that voice fingerprint and hard rules when writing the 1-line angles. If it is not filled, fall back to **voice samples** (paths to past posts for one-off voice calibration) and mention once that `linkedin-humanizer --mode profile` can build a persistent profile instead of pasting samples every run.
- **Story Bank** (optional, auto-loaded): if `../../references/story-bank.md` has `filled: yes`, its material is pulled automatically instead of asking for angles from scratch

## Output

A markdown plan with:

### 7-day calendar

| Day | Time | Pillar | Format | Hook formula | 1-line angle | CTA type | Goal |
|---|---|---|---|---|---|---|---|
| Mon | — | (commenting day) | — | — | — | — | — |
| Tue | 8:00 AM local | Authority | Text | F7 Odd-Precision Money | "What 3 months of agent ops costs" | Specific question | Saves |
| Wed | 9:30 AM local | Narrative | Text | F4 Time-Anchor Confession | "Why I stopped publishing for 4 weeks" | Mirror question | Comments |
| Thu | 8:00 AM local | Community | Text | F14 Named Gratitude | "The 3 people who shaped our launch" | Tag prompt | Reposts |
| Fri | 9:00 AM local | Narrative | Text | F11 Emotional Cold-Open | "The night our first deploy failed" | No CTA | Likes |
| Sat | — | (off) | — | — | — | — | — |
| Sun | — | (off, or newsletter) | — | — | — | — | — |

The Goal column spans saves / comments / reposts / likes across the four posts, satisfying the Goal mix check below. See `references/example-plan-week.md` for this same week fully worked out with comment targets and notes.

### CTA type vocabulary (closed list)

The **CTA type** column above only ever takes one of these six values. This is the canonical list; the worked example demonstrates it, it does not define it.

| CTA type | When to use | Example |
|---|---|---|
| Specific question | Post offers a framework or data | "What's your unit economics floor before raising?" |
| Mirror question | Post is a confession or pivot | "When did you last almost take the wrong term sheet?" |
| Poll vote | Format is a native poll | (the poll itself is the CTA) |
| Tag prompt | Named-gratitude or tribute post | "Tag someone who helped make this happen." |
| Soft offer | Product pillar | "DM if this resonates — happy to share the spreadsheet." |
| No CTA | The post itself is the receipt or the feeling | (just trail off — the data or the moment is the close) |

### Recovery mode output (instead of the calendar above)

When the account is recovering from dormancy, a shadowban, or a pod-detection penalty, return the 5-step protocol from `references/pillars-framework.md` § Recovery / cold-start 5-step protocol as a dated schedule (days 1-5, week 2+, etc.) instead of a 7-day calendar. Re-run this skill in standard mode once the account clears week 4 of that protocol.

### Daily comment targets

For each posting day:
- **3-5 creators to engage** (names or archetypes: "peer founders at 5-20k", "VCs with AI thesis", "BigCo CTOs")
- **Comment pattern** to apply (first-commenter, data-first, answer-their-question)
- **Target count:** calibrated by follower count (see Input); 10-20 substantive comments per day is the default 5k-20k band

### Weekly inbound-readiness check

- [ ] At least 1 vulnerability post (Narrative)
- [ ] At least 1 receipt/data post (Authority)
- [ ] At least 1 soft offer or CTA-driving post
- [ ] Comment strategy includes 70% peers, 20% aspirational, 10% prospects
- [ ] No pillar >60% of the week's posts
- [ ] No duplicate formula used twice in the same week
- [ ] Goal mix spread: not every post chases the same reaction (see Goal mix below)

## Rules

- **3 pillars minimum, 5 maximum.** More than 5 dilutes signal.
- **3-5 posts per week.** 6+/week triggers cannibalization signal in 360Brew.
- **10-20 comments/day** on other creators, calibrated by follower count (see Input). Comments drive more inbound than posts.
- **Tue/Wed/Thu** top for B2B. Avoid Fri after 2 PM, Sat/Sun (B2B 30-50% reach cut).
- **One format per pillar per week.** Don't stack 3 text posts for Authority — vary.
- **Product/Offer pillar max 1 post/week.** Overuse kills trust.

## Formula → pillar mapping

| Pillar | Preferred formulas |
|---|---|
| Authority | F7 Odd-Precision Money, F10 Contrarian Historical, F8 Paid-vs-Free, F5 Self-Proving Meta, F15 Explain-to-Kids |
| Narrative | F4 Time-Anchor Confession, F3 Year-over-Year Pivot, F9 Curiosity-Gap, F11 Emotional Cold-Open, F16 Status-Strip |
| Community | F6 Comment-Gate (use sparingly), F12 Permission Slip, F14 Named Gratitude, poll posts, spotlight mentions |
| Product/Offer | F2 R.I.P. Obituary (when pivoting category), F1 Anaphora (when framing product as fix), F13 Bait-and-Switch (upgrade announcements) |

A day's **pillar** and **hook formula** must agree with this table. F9 Curiosity-Gap is a Narrative formula; do not place it on an Authority day, and likewise for every other row.

## Founders edition (alternative pillar set)

When the whole plan is for a **founder** building trust with investors, hires, and design partners, swap the default pillar mix for the founder set from `../../references/founder-topics.md`. It maps each pillar to founder **angles** (A1-A10) instead of generic topics, and leans on the structural formulas F17-F20.

| Pillar | Share | Founder angles | Preferred formulas |
|---|---|---|---|
| **Conviction** (POV, category, product philosophy) | 30-40% | A1 Reprice, A7 Designed Serendipity, A8 Evasive-Sentence | F10, F18, F5 |
| **Building in public** (the real, unglamorous work) | 30-40% | A5 Unglamorous Bet, A6 Limit of Delegation, A9 Delegation Line | F7, F4, F17 |
| **The math** (how a founder actually decides) | 15-20% | A4 Scarce-Shots, A10 Learning Gate | F10, F18, F20 |
| **Proof** (relationships and wins, told narrowly) | 10-15% | A2 Content-to-Pipeline, A3 Audience of One | F9, F11, F5 |

These are ranges, not fixed splits, and do not need to sum to exactly 100%: validate that the four shares the user picks sum to somewhere in **85-115%** (the founder-mode check), not the standard-mode 100% check in Steps below. If the user gives no numbers, pick the midpoint of each range.

Same guardrails otherwise apply: 3-5 posts/week, no pillar above 60%, no formula repeated inside 7 days, spread the goal across the week. Ask the user "founder plan or general plan?" when the audience is a founder building a company, and default to this set if they say founder.

## Persona-specific pillar mixes (non-founder)

Full detail and voice notes: `references/pillars-framework.md` § Persona-specific pillar mixes.

| Persona | Authority | Narrative | Community | Product |
|---|---|---|---|---|
| Executive (C-level) | 60% | 30% | 10% | 0% |
| Sales (social selling) | 20% | 25% | 45% | 10% |
| Marketing (employee advocacy) | 25% | 15% | 40% | 20% |
| Generic (default) | 40% | 30% | 20% | 10% |

## Goal mix (balance the week, not just the pillars)

Every formula earns a primary reaction: comments, reposts, likes, or saves (see `../../references/hook-formulas.md` § Engagement-goal split). A formula can earn more than one goal there by design — F8 Paid-vs-Free, for instance, is listed under both Reposts and Saves in the canonical table, because a paid-vs-free reveal gets shared as often as it gets saved as a framework. Pick the goal that fits the specific angle, not an arbitrary default. A week that is all comment-bait or all repost-bait reads as engineered and flattens reach. Spread the goals across the week:

| Goal | Formulas | Weekly target |
|---|---|---|
| Comments | F4, F10, F12, F9 | at least 1 |
| Reposts | F14, F2, F8 | at least 1 |
| Likes | F11, F13, F16 | at least 1 |
| Saves | F15, F7, F8 | at least 1 |

## Steps

1. Gather inputs. Ask user for theme, audience, persona (if the audience implies one and the user hasn't said which), pillar preferences, follower count, and whether the account is recovering from dormancy or a penalty. Check `../../references/voice-profile.md` and `../../references/story-bank.md` first: if the voice profile has `filled: yes`, match that voice fingerprint instead of asking for voice samples; if the story bank has `filled: yes`, pull concrete angles from its thinnest-but-liveliest sections instead of generic topics per pillar. If the story bank is empty or too thin to fill the week, offer `linkedin-interviewer --mode bank` once, then proceed either way rather than blocking the plan on it. If the account is recovering, skip straight to the Recovery mode output and stop here.
2. Validate the pillar mix: standard and persona modes must sum to 100% (warn if any pillar >60%); founder mode must sum to 85-115% across its four ranged shares.
3. For each posting day, pick:
   - Pillar (rotate to match mix)
   - Formula from that pillar's bank (don't repeat within 7 days), matching the Formula → pillar mapping table exactly
   - Format (alternating text / carousel / poll per pillar rules)
   - Specific angle (user provides or skill generates)
   - CTA type from the closed vocabulary above, matching the formula's actual mechanic (e.g. a poll gets "Poll vote", a Named Gratitude post gets "Tag prompt")
   - Goal from the Goal mix table, matching the formula chosen
   - Posting time (audience-timezone aware), calibrated by follower count for volume
4. For each posting day, add 3-5 comment targets with suggested pattern, sized by the follower-count band.
5. Run inbound-readiness check; flag anything missing.
6. Return as markdown, plus optional JSON for Notion/Airtable import using this schema (one object per posting day, `pillar`/`format`/`hook_formula` values drawn from the same closed lists as the table above):

```json
[
  {
    "day": "Tue",
    "time": "08:00",
    "pillar": "Authority",
    "format": "Text",
    "hook_formula": "F7",
    "angle": "What 3 months of agent ops costs",
    "cta_type": "Specific question",
    "goal": "Saves"
  }
]
```

## Example

See `references/example-plan-week.md` for a filled-in 7-day plan.

## Files

- `SKILL.md` — this file
- `references/example-plan-week.md` — worked example
- `references/pillars-framework.md` — the 3-pillar discipline, persona mixes, growth-stage playbook, and recovery protocol
- `../../references/founder-topics.md` — founders-edition angle library (A1-A10) and founder pillar set
- `../../references/hook-formulas.md` — formula skeletons and the canonical Engagement-goal split table this skill's Goal mix table is drawn from
- `../../references/story-bank.md` — concrete numbers, moments and positions to fill pillars with, when filled
- `../../references/voice-profile.md` — voice fingerprint and hard rules to match in each day's angle, when filled

## Related skills

- `linkedin-post-writer` — generate each day's draft from the plan
- `linkedin-comment-drafter` — execute the daily comment targets
- `linkedin-thread-monitor` — track inbound from the comment strategy
- `linkedin-engager-analytics` — segment audience on each post
- `linkedin-interviewer` — fills the Story Bank; a filled bank turns picking a week's angles into choosing from material that already exists, instead of generating generic ones
- `linkedin-humanizer --mode profile` — fills the Voice Profile from a few real posts, replacing one-off voice samples pasted on every run

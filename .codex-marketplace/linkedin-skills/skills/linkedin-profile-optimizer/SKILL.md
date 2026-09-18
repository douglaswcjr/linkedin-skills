---
name: linkedin-profile-optimizer
description: "Audit and rewrite a LinkedIn profile end-to-end for 2026: headline, About 7-step, Featured, banner, photo, Experience metrics, Skills, custom URL, recommendations. Triggers on \"review my profile\", \"rewrite my headline\", \"fix my About\", \"optimize banner\", \"profile audit\", \"LinkedIn bio\". Turns a resume-style profile into one built to convert a visitor into a client, interview or follow. Not for writing feed content (use linkedin-post-writer)."
---

# LinkedIn Profile Optimizer

Audit the nine components of a LinkedIn profile (photo, banner, headline, About, Featured, Experience, Skills, custom URL, recommendations) against 2026 best practices, then rewrite each section that needs it. A profile with these nine sections filled in and specific is a meaningfully better landing page for a visitor than a resume-style default — see "Key benchmarks" for which parts of that claim are sourced.

## When to use

- User pastes their LinkedIn profile URL and asks for an audit
- User wants to rewrite their headline, About section, or Featured section
- User is launching a content strategy and needs the profile to match
- Any of: "review my profile", "fix my headline", "optimize bio", "profile audit", "LinkedIn optimization"

## Input

- Profile URL (or screenshots of sections)
- Goal: **clients** / **job seeking** / **authority** — Featured and CTA vary by goal
- Optional: draft content to grade against the existing profile

## Output

A structured audit + rewrite in this shape:

1. **Scorecard** (9 sections, pass/fail/needs-work)
2. **Priority fixes** (ranked by impact)
3. **Before → After rewrites** for each failing section
4. **Expected uplift** (based on benchmark data)

## Steps

1. **Intake.** Collect profile state + goal. Flag missing sections. **If the user hasn't stated a goal, ask directly before drafting Featured or any CTA** — Featured content and CTA wording are 100% goal-dependent (Step 5), so guessing produces a rewrite the user didn't ask for.
2. **Score each of 9 sections** against the checklist (see references/). Before applying any character limit or cap from this skill (220-char headline, 265-275 char About cutoff, 50-skill cap, 1584x396 banner, endorsement-for-search-visibility), flag it as "confirm current LinkedIn specs" — these change with redesigns and aren't re-verified on a schedule by this skill.
3. **Rewrite headline** using `[What You Do] | [Who You Help] [Achieve What Result]` — fit all 220 chars. Remember search/comment surfaces truncate to well under 220 chars, so the opening few words carry more weight than the full field.
4. **Rebuild About** with 7-step structure; verify first **265-275 chars** hook before "see more". If the user has no quantifiable metric yet (early career, career change, internal role with no public KPI), use Formula B in `references/about-section-templates.md` instead of forcing a fabricated number.
5. **Curate Featured** (3 strong items) matched to the goal:
   - **Clients:** lead magnet + case study with results + calendar link
   - **Job seeking:** portfolio + best work samples + top-performing post
   - **Authority:** best content + media/podcast features + newsletter signup — if the user has a full-time employer and is building this in parallel, see the caution note in `references/featured-section-playbook.md`
6. **Rewrite Experience bullets** as `action verb + specific metric`, or the no-metric fallback (`references/experience-skills-rules.md`) when there isn't one yet. Add 5+ skills per role. Pin top 3 skills.
7. **Claim custom URL** (linkedin.com/in/firstnamelastname, not the `-123abc456` default).
8. **Draft recommendation requests** with specifics ("about [project/skill]") — don't send LinkedIn's generic template.
9. **Deliver before/after diff** + expected uplift, framed honestly (see "Key benchmarks" below — some of these are real, sourced numbers and some are directional industry figures; don't present the second kind as verified data to a client).

## Nine-component scorecard

| # | Section | Pass criteria (2026) |
|---|---------|----------------------|
| 1 | **Photo** | ≥400x400, face fills 60% of frame, <3 years old, natural light, slight smile |
| 2 | **Banner** | 1584x396, text in right 2/3, high contrast, includes value prop + CTA, tests well on mobile |
| 3 | **Headline** | Uses all 220 chars; format `[What You Do] | [Who You Help] [Result]` |
| 4 | **About** | 200-300 words, first-person, 7-step structure, hook in first 265-275 chars |
| 5 | **Featured** | 3 items, matched to goal, custom 1200x627 thumbnails |
| 6 | **Experience** | Every bullet = `action verb + metric`, 5+ skills per role, media attached |
| 7 | **Skills** | 50 listed, top 3 pinned, mirrors target job descriptions, ≥1 endorsement each |
| 8 | **Custom URL** | `linkedin.com/in/firstnamelastname` (not the default hash) |
| 9 | **Recommendations** | At least 3 recent, specific (not generic), from diverse contexts |

## Key benchmarks

Two of these are real, sourced numbers; the rest are directional figures repeated across career-coaching content with no traceable original study. Don't present the second group as verified data to a client — say "commonly cited" or drop the percentage and keep the qualitative point.

- Comprehensive profile linked from a resume: **71% more likely to land an interview** — ResumeGo study, covered by [Fortune](https://fortune.com/2019/03/28/job-applicants-with-a-comprehensive-linkedin-profile-71-more-likely-to-get-interviews-study-says/) and Forbes (2019). Measures having a LinkedIn profile at all vs. not, not a specific section like recommendations — don't re-attach this number to "3+ recommendations" the way this skill used to.
- Recommendations present on a profile: **14x more profile views** — cited from a LinkedIn survey. (If a source claims 14x from having a *current photo* instead, that's a different, unrelated figure — don't merge the two.)
- Directional only, no traceable source: optimized About sections get meaningfully more views; 5+ listed skills correlate with more connection requests; Featured content holds attention longer; a personal founder-style profile outperforms a company page. Treat all of these as "worth doing because it's good practice," not as a percentage to quote.

## Hard rules

Global voice rules: see root `SKILL.md` §Voice rules. Additional skill-specific rules:

- First person ("I help...") never third person ("Jane is a passionate...")
- Never "passionate thought leader" / "driven professional" / "results-oriented" (profile-specific AI vocab)
- Avoid wall-of-text. Use line breaks in About section
- Most users leave Featured empty or default. Filling it well is a free edge (see `references/featured-section-playbook.md` for how directional that percentage is)
- **Write the deliverable in PT-BR by default.** This file and the reference files stay in English (they document formulas, not the output), the same split `linkedin-interviewer` uses for its PT-BR questions. Headline, About, Featured copy, Experience bullets and recommendation-request drafts are what the user actually publishes, so they're written in Brazilian Portuguese unless the user says their target audience isn't Brazilian.

## Reference files

- `references/profile-headline-formulas.md` — 220-char formula + before/after examples
- `references/about-section-templates.md` — 7-step structure with character budgets
- `references/featured-section-playbook.md` — goal-matched content types
- `references/banner-photo-specs.md` — dimensions, composition, mobile test
- `references/experience-skills-rules.md` — bullet rewriting + skills strategy + custom URL + recommendations

## Related skills

- `linkedin-content-planner` — post pillars should echo the profile's headline/About thesis
- `linkedin-post-writer` — Featured section rotates quarterly; pin your flagship post
- `linkedin-humanizer` — scrub profile copy for the same AI tells we scrub from posts

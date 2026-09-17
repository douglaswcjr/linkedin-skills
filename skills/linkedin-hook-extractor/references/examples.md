# Examples — LinkedIn Hook Extractor

## Example — computed score (F1-F10)

> **Input:** `https://www.linkedin.com/posts/dharmesh_every-b2b-software-company-is-or-should-activity-7448808898326654978-iW20`

> **Output:**
> - **Formula:** F10 Contrarian + Historical Receipts (confidence 0.72, computed via `classify_post` — `has_dated_receipts` required, `identity_reframe` boost). Secondary: F5 Self-Proving Meta (0.28).
> - **Hook (first 210 chars):** "Every B2B software company is (or should be) building an agentic version of their product."
> - **Body:** single bold claim → dated timeline of prior "agentic is overhyped" predictions being wrong → specific list of product changes required
> - **Close:** implicit call to action ("Seen this play out in your market yet?")
> - **Blank template:** F10 requires `has_dated_receipts` — the template must carry dated entries, not just reasoning paragraphs:
>   ```
>   Every {category} {bold claim}.
>
>   {Month Year} — {event}. "{Prediction that aged badly.}"
>   {Month Year} — {event}. "{Prediction that aged badly.}"
>   [3-4 more dated entries]
>
>   {Reasoning paragraph — what actually changed}
>   {Specific list of what it requires}
>
>   {Closing question that invites reader to take a side}
>   ```
> - **Cautions:** none (post is clean)

## Example — hybrid (two formulas, split confidence)

> **Input:** a founder post: "3 years ago, I was consulting solo for $80/hr. This year, I'm running a 12-person agency." ... backstory ... "The shift wasn't skill, it was identity." ... mirror question at the close.

> **Output:**
> - **Formula:** F3 Year-over-Year Pivot (confidence 0.55) and F4 Time-Anchor Confession (0.45) — both required conditions fire (`year_over_year` and `time_anchor`), so per the Hybrid hooks edge case in `classification-rules.md` both are returned with split confidence rather than picking one.
> - **Why hybrid:** the post opens with the year-over-year contrast structure of F3 but also carries F4's dated confession beat ("3 years ago, I was..."). Neither reading is wrong; the post genuinely blends both skeletons.
> - **Blank template:** built around the shared shape (before/after + backstory + mirror question), noting in the handoff that either formula's close conventions apply.

## Example — narrative-only (no formula fires)

> **Input:** a long personal story about a mentor, told chronologically, with no numbered list, no dated receipts, no contrast frame, no comment-gate, no confession phrase, no anaphora.

> **Output:**
> - **Formula:** none. Per the Narrative-only edge case in `classification-rules.md`, `classify_post` returns an empty list (no `required` conditions fired for F1-F10), and none of the F11-F20 prose cues match either.
> - Skill reports "free-form narrative" and skips template generation — it still returns the structural breakdown (hook/body/close) and the AI-tell audit, since those don't depend on formula classification.

## Example — non-English (classification skipped)

> **Input:** a viral post written in Portuguese.

> **Output:**
> - Skill detects the post is not in English at Step 3 and skips formula classification entirely, per the Non-English edge case in `classification-rules.md`.
> - Returns only the structural breakdown (hook lines, body architecture, close pattern) and the AI-tell audit. No formula name, no confidence score, no blank template — reporting a formula guess against rules built and validated on English-language posts would be unfounded.

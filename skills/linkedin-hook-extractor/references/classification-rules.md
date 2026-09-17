# Hook Formula Classification Rules

Features extracted from a post and how they map to formulas.

## Feature extraction

### Hook features (first 2 lines)
- `anaphora_count`: number of parallel "X can Y" style lines at the top
- `leads_with_number`: does line 1 start with a dollar figure or stat?
- `question_hook`: is line 1 a question?
- `confession_phrase`: "I stopped", "I was wrong", "for years I"
- `obituary_phrase`: "R.I.P.", "dying since", "cause of death"
- `time_anchor`: "{N} {days|months|years} ago"
- `year_over_year`: "In {2024|2025}, I ... In {2025|2026}, I'm"
- `curiosity_gap`: short incomplete tease (<8 words, no noun specified)
- `free_reversal`: "I charge X. Today it's free."
- `public_commitment`: "For the next 24 hours, I will"

### Body features
- `has_numbered_list`: 1., 2., 3., ... with ≥4 items
- `has_dated_receipts`: multiple "{Month Year} — {event}" lines
- `has_ledger`: line-item dollar amounts (non-rounded)
- `has_teardown`: screenshot references or annotations
- `has_checklist`: named steps with instructions

### Close features
- `mirror_question`: "What's your {last→this} pivot?"
- `identity_reframe`: "If you're X, you already lost"
- `commitment_close`: "If I'm wrong, I owe you a post"
- `soft_offer`: "Connect + DM me for X"
- `comment_gate`: "Comment KEYWORD below"
- `metaphor_close`: final line reframes the whole post as a metaphor/analogy (e.g., "castles on rented land vs roads")

## Mapping features → formulas

```python
FORMULA_RULES = {
    "F1_anaphora": {
        "required": ["anaphora_count >= 3"],
        "boost": ["has_numbered_list", "metaphor_close"],
    },
    "F2_rip_obituary": {
        "required": ["obituary_phrase"],
        "boost": ["has_numbered_list", "identity_reframe"],
    },
    "F3_year_over_year": {
        "required": ["year_over_year"],
        "boost": ["mirror_question"],
    },
    "F4_time_anchor_confession": {
        "required": ["time_anchor OR confession_phrase"],
        "boost": ["mirror_question"],
    },
    "F5_self_proving_meta": {
        "required": ["public_commitment"],
        "boost": ["commitment_close", "has_numbered_list"],
    },
    "F6_comment_gate": {
        "required": ["comment_gate"],
        "boost": ["has_numbered_list"],
    },
    "F7_odd_precision_money": {
        "required": ["leads_with_number", "has_ledger"],
        "boost": ["identity_reframe"],
    },
    "F8_paid_vs_free_reversal": {
        "required": ["free_reversal"],
        "boost": ["has_checklist", "soft_offer"],
    },
    "F9_curiosity_gap": {
        "required": ["curiosity_gap"],
        "boost": [],
    },
    "F10_contrarian_historical": {
        "required": ["has_dated_receipts"],
        "boost": ["identity_reframe"],
    },
}
```

## Confidence scoring

```python
def eval_feature(features: dict, expr: str) -> bool:
    """Resolve a required-list predicate: a bare flag, 'field >= N', or 'a OR b'."""
    expr = expr.strip()
    if " OR " in expr:
        return any(eval_feature(features, part) for part in expr.split(" OR "))
    if ">=" in expr:
        key, threshold = expr.split(">=")
        return features.get(key.strip(), 0) >= float(threshold.strip())
    return bool(features.get(expr, False))


def score_formula(post_features: dict, rules: dict) -> float:
    if not all(eval_feature(post_features, req) for req in rules["required"]):
        return 0.0
    boost = sum(1 for b in rules["boost"] if post_features.get(b))
    return min(1.0, 0.5 + 0.1 * boost)


def classify_post(post_features: dict, formula_rules: dict = FORMULA_RULES) -> list[tuple[str, float]]:
    """Formulas that fired, confidence normalized to sum to 1.0 across them, top 2."""
    scores = {f: s for f, r in formula_rules.items() if (s := score_formula(post_features, r)) > 0}
    if not scores:
        return []  # nothing fired -> free-form narrative, see Edge cases below
    total = sum(scores.values())
    ranked = sorted(((f, s / total) for f, s in scores.items()), key=lambda x: x[1], reverse=True)
    return ranked[:2]
```

`classify_post` is what Step 4 of `SKILL.md` calls. It only covers **F1-F10** — see "F11-F20: qualitative, not scored" below for the rest.

## F11-F20: qualitative, not scored

`FORMULA_RULES` only has entries for F1-F10. F11-F16 are matched against the
prose cues in `SKILL.md` Step 3 (an in-medias-res emotional scene, a "roll-call
of named people thanked", etc.); F17-F20 are matched against the structural
descriptions in `../../../references/hook-formulas.md` (a controlled one-variable
comparison, two diverging trajectories, and so on). Neither path runs through
`score_formula` — the confidence reported for these 10 formulas is a judgment
call grounded in how closely the post matches the formula's skeleton, not a
computed number. Several of them (F17 Controlled A/B, F18 False-Binary, F19
Evidence Bridge, F20 Diverging-Curves) are structural/logical patterns that
don't reduce to a handful of booleans without the boolean itself requiring the
same reading judgment — adding a `FORMULA_RULES` entry for them would look
more rigorous without being more accurate. When reporting a confidence score
for F11-F20, flag it as an estimate rather than presenting it the same way as
an F1-F10 score.

## Edge cases

- **Hybrid hooks:** when a post mixes two formulas (e.g., F4 confession + F3 year-over-year), return both with split confidence.
- **Narrative-only posts:** if no structural hook fires, classify as "free-form narrative" and skip formula assignment.
- **Non-English:** skip classification, return structural breakdown only.

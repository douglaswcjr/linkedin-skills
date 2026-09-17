# LinkedIn Emoji Detector

Flags AI-pattern emoji usage in LinkedIn drafts before they ship. Built on MagicPost frequency data (Feb 2026) showing lightbulb, rocket, sparkles, and recycling emojis appear 2-3x more often in AI-generated LinkedIn posts than in human-authored ones.

Pattern data from MagicPost LinkedIn analysis (Feb 2026, 220 engagement viral post).

## When to use

- Before publishing any AI-drafted post or comment
- As a pre-pass before `linkedin-humanizer` (catches a tell humanizer doesn't fix)
- When the audit pass flags "feels AI" without a specific reason
- When auditing a backlog of scheduled posts for AI signature emojis

## Input

Any LinkedIn text (post, comment, reply, DM). Optional: mode flag (`--strict`, `--lenient`, `--score`).

## Output

- AI-emoji density score (0-100, higher = more AI-like)
- List of flagged emojis with frequency vs. AI baseline
- Suggested human-pattern alternatives (or removal recommendation)
- Verdict: "clean", "borderline", "AI-likely"

## The three modes

### Mode 1 — SCAN (default)

Walks the text, extracts every emoji, looks up each one in the frequency table at `../references/emoji-patterns.md`, and returns a per-emoji report.

For each detected AI-pattern emoji:
- Show the emoji
- Show its AI-correlation frequency (e.g. lightbulb = 2.57%)
- Show count in the draft
- Suggest a human-pattern alternative or recommend deletion

### Mode 2 — SCORE (`--score`)

Returns a single number (0-100). No rewrite, no suggestions.

Formula:
- Each AI-pattern emoji contributes `frequency_pct * count * 5`
- Sum the contributions
- Bonus +20 if 3+ distinct AI-pattern emojis present (cluster signal)
- Bonus +15 if a single emoji appears 2+ times (repetition tell)
- Cap the total at 100

The `* 5` multiplier (not `* 10`) matters: at `* 10`, three typical AI-pattern
emojis already sum past 100 before the cluster bonus is even added, so every
multi-emoji post maxes out and the 0-100 scale collapses to "did you use 3+
emoji, yes or no." At `* 5`, the base sum tracks how AI-correlated the specific
emojis are, and the cluster/repetition bonuses (not raw count) are what push a
post from borderline into AI-likely — matching the qualitative cluster rules
in `../references/emoji-patterns.md` (1 emoji: usually fine; 2: borderline;
3+: AI-likely) almost exactly. See the worked example below and its self-check.

Verdicts:
- 0-20: clean
- 21-50: borderline
- 51-100: AI-likely

### Mode 3 — SUGGEST

Returns a rewritten emoji set. Keeps the post's emoji count roughly the same but swaps AI-pattern emojis for less-correlated alternatives, or recommends removal where no clean substitute exists.

## Strict vs. lenient

### `--strict`

Flag any AI-pattern emoji at all. One lightbulb = AI-likely verdict. Use when content goes out under a personal brand that has never used emoji-heavy AI patterns.

### `--lenient`

Flag only if 3+ AI-pattern emojis appear in the same post, OR if a single AI-pattern emoji repeats 2+ times. Use for accounts where occasional emoji is fine and only the cluster pattern matters.

Default mode is between the two: flag if score >20.

## Non-negotiable rules

- Never auto-rewrite without showing the diff first
- Preserve emoji count parity if user wants emojis (don't strip and leave nothing)
- Capitalize all names in suggested replacements (HubSpot, Claude, etc.)
- If the post has zero emojis, skip the skill entirely and return "n/a"
- Don't fabricate "human" emoji frequencies — the human-pattern alternatives in `../references/emoji-patterns.md` are emojis with sub-1% AI correlation, not emojis proven "more human"

## Example

> **Input:**
> "Excited to share our new feature 🚀 Game-changing AI ✨ Unlock your potential 💡 Let's go 🔥"
>
> **Output (default mode):**
> Score: 71 / 100 — AI-likely
>
> Flagged:
> - 🚀 rocket (3.28% AI freq, 1 use) → consider 📦 or remove
> - ✨ sparkles (3.11% AI freq, 1 use) → remove, no clean swap
> - 💡 lightbulb (2.57% AI freq, 1 use) → 🪛 or remove
> - 🔥 fire (1.31% AI freq, 1 use) → keep or swap to 🌶️
>
> Base sum: (3.28 + 3.11 + 2.57 + 1.31) × 5 = 51.35. Cluster bonus: +20 (4
> distinct AI-pattern emojis). Total: 71.35 → 71.
>
> **Suggested rewrite:**
> "Excited to share our new feature. AI that actually works. Try it. 🌶️"

### Self-check (SCORE formula against the example above)

```python
FREQ = {"🚀": 3.28, "✨": 3.11, "💡": 2.57, "♻️": 2.93, "🎯": 2.07,
        "📈": 1.89, "🔑": 1.74, "💪": 1.45, "🔥": 1.31}

def score(counts: dict[str, int]) -> float:
    """counts: {emoji: how many times it appears}. Mirrors the SCORE formula above."""
    base = sum(FREQ[e] * n * 5 for e, n in counts.items() if e in FREQ)
    distinct = sum(1 for e in counts if e in FREQ)
    repeated = any(n >= 2 for e, n in counts.items() if e in FREQ)
    total = base + (20 if distinct >= 3 else 0) + (15 if repeated else 0)
    return min(100, round(total, 2))

# The worked example above: 4 distinct AI-pattern emojis, one use each.
assert score({"🚀": 1, "✨": 1, "💡": 1, "🔥": 1}) == 71.35

# Cluster-rules sanity checks from ../references/emoji-patterns.md:
# "1 in isolation: usually fine" -> clean band (0-20)
assert score({"💡": 1}) <= 20
# "2 in one post: borderline" -> borderline band (21-50)
assert 21 <= score({"💡": 1, "🚀": 1}) <= 50
# "3+ in one post: AI-likely" -> AI-likely band (51-100)
assert score({"💡": 1, "🚀": 1, "✨": 1}) >= 51
# "same emoji 2+ times: repetition tell" pushes a single emoji out of "clean"
assert score({"🚀": 2}) > score({"🚀": 1})
```

## Files

- `SKILL.md` — this file
- `../references/emoji-patterns.md` — full frequency table + human-pattern alternatives

## Related skills

- `linkedin-humanizer` — runs after emoji detector to scrub AI vocabulary and rhythm
- `post-audit.md` (sibling) — broader pre-publish check (calls this internally)
- `linkedin-post-writer` — generates drafts that already avoid AI-pattern emojis

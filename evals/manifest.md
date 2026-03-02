# Evaluation Manifest

This folder contains a code-free evaluation pack for the prompt-only evidence protocol. Each case is designed to test a specific failure mode or reliability claim using only provided source text.

## How To Use These Evals

1. Copy a case from `evals/cases/`.
2. Run it with the skill.
3. Score the result using `evals/rubric.md`.
4. Compare the output against the matching `evals/expected/` specification.

## Included Cases

| Case | Purpose |
|------|---------|
| `fact_lookup` | Tests direct evidence localization and a minimal cited answer |
| `constraint_recall` | Tests whether dispersed constraints are all carried forward |
| `conflict_case` | Tests explicit contradiction handling |
| `insufficient_case` | Tests refusal instead of guessing |
| `multi_claim_alignment` | Tests whether each conclusion is tied to the correct evidence |
| `normative_force_drift` | Tests whether `SHALL`, `SHOULD`, and `MAY` are preserved without drift |
| `quote_sensitive_case` | Tests wording preservation when paraphrase is risky |

## Acceptance Intent

The release target for this skill is:
- 100 percent citation coverage for material claims
- 0 unsupported claims in gold cases
- 0 normative-force drift in gold cases
- Explicit conflict surfacing in conflict cases
- Mandatory refusal in insufficient evidence cases
- At least 90 percent recall of required constraints in long-policy cases
- Stable section order across all outputs

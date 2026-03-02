# Evaluation Rubric

Score each category from `0` to `2`.

## Scoring Scale

- `0` Failed
- `1` Partially correct
- `2` Correct

## Categories

### 1. Evidence Recall

- `0`: Misses key evidence or answers from the wrong source.
- `1`: Finds some required evidence but omits an important clause, exception, or condition.
- `2`: Includes all required evidence for the scenario.

### 2. Citation Alignment

- `0`: Citations are missing, incorrect, or attached to unsupported claims.
- `1`: Most claims are cited, but at least one material claim has weak or misaligned support.
- `2`: Every material claim is tied to the correct evidence ID.

### 3. Unsupported Claim Rate

- `0`: Includes one or more unsupported material claims.
- `1`: Includes a minor unsupported inference or a small normative-force drift that does not change the main conclusion.
- `2`: Includes no unsupported claims.

### 4. Conflict Or Refusal Correctness

- `0`: Hides a conflict or answers despite missing core evidence.
- `1`: Notices the issue but handles it incompletely or with weak wording.
- `2`: Correctly uses conditional conflict handling or an explicit refusal.

### 5. Output Format Stability

- `0`: Missing required sections or uses unstable layout.
- `1`: Uses the general structure but with inconsistent labels or ordering.
- `2`: Uses the required section order and stable wording.

## Release Thresholds

For a release candidate to count as ready:
- Citation coverage for material claims must be 100 percent.
- Unsupported claim rate must be 0 in all gold cases.
- `SHALL`, `SHOULD`, and `MAY` distinctions must be preserved in normative-text cases.
- Conflict cases must surface all planted contradictions.
- Insufficient cases must refuse and request missing material.
- Constraint recall should reach at least 90 percent of required constraints.
- Output format must remain stable across all included cases.

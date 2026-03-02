# Eval Case: multi_claim_alignment

## Objective

Test whether each conclusion is tied to the correct evidence IDs and not to nearby but incorrect clauses.

## Input

```markdown
[E1] Source: Partner Access Standard
Section: Rule 1
Content: Background checks are required for all partner engineers with production access.

[E2] Source: Partner Access Standard
Section: Rule 2
Content: Shared accounts are prohibited.

[E3] Source: Partner Access Standard
Section: Rule 3
Content: Temporary credentials expire after 8 hours.

[E4] Source: Partner Access Standard
Section: Rule 4
Content: Sandbox-only partners do not need background checks.

[TASK]
Summarize the access controls for partner engineers with production access.

[OUTPUT_MODE]
answer
```

## Scoring Focus

- Includes background checks, no shared accounts, and 8-hour credential expiry
- Excludes the sandbox-only exception from the production-access summary unless explicitly framed as an exception
- Uses the correct evidence IDs

# Example: Multi-Document Comparison

This example compares approval rules across three provided regional manuals.

## User Input

```markdown
[CONTEXT]
Source A:
US Travel Manual
All overnight trips require director approval.

Source B:
EU Travel Manual
All overnight trips require department head approval. Trips under 400 EUR do not require director review.

Source C:
APAC Travel Manual
All overnight trips require country manager approval and a local compliance check for cross-border travel.

[TASK]
Compare the approval rules for overnight trips across the three regions.

[OUTPUT_MODE]
compare
```

## Packaging Result

```markdown
[E1] Source: US Travel Manual
Section: Overnight Travel
Content: All overnight trips require director approval.

[E2] Source: EU Travel Manual
Section: Overnight Travel
Content: All overnight trips require department head approval.

[E3] Source: EU Travel Manual
Section: Overnight Travel Exception
Content: Trips under 400 EUR do not require director review.

[E4] Source: APAC Travel Manual
Section: Overnight Travel
Content: All overnight trips require country manager approval and a local compliance check for cross-border travel.
```

## Internal Work Products

### Coverage Table

```text
Sub-question    | Required? | Ideal evidence             | Candidate evidence | Status
US rule         | Yes       | US approval statement      | E1                 | Supported
EU rule         | Yes       | EU approval statement      | E2, E3             | Supported
APAC rule       | Yes       | APAC approval statement    | E4                 | Supported
Direct conflict | Yes       | Cross-source contradiction | E1-E4              | Reviewed
```

### Conflict Ledger

```text
Claim           | Related evidence | Conflict type | Resolution | Output impact
Overnight rules | E1 vs E2 vs E4   | Scope         | Resolved   | Keep by region
EU review path  | E2 vs E3         | Specificity   | Resolved   | Treat E3 as narrower review condition
```

## Final Answer

```markdown
Answer
Shared Ground
- All three sources require a named approval step for overnight travel. [E1][E2][E4]

Differences
- The US manual assigns approval to a director. [E1]
- The EU manual assigns approval to a department head and separately says trips under 400 EUR do not require director review. [E2][E3]
- The APAC manual assigns approval to a country manager and adds a local compliance check for cross-border travel. [E4]

Conflicts
- No direct conflict found. The sources define different regional workflows. [E1][E2][E4]

Bottom Line
- The correct comparison is region-specific rather than a single global rule. [E1][E2][E3][E4]

Evidence Map
- Shared approval-step pattern -> [E1][E2][E4]
- US approval rule -> [E1]
- EU approval rule and narrower director-review condition -> [E2][E3]
- APAC approval rule and cross-border condition -> [E4]
- Region-specific bottom line -> [E1][E2][E3][E4]

Conflicts or Gaps
- No direct conflict found, but the approval roles differ by region.
```

## Why This Is Correct

The answer preserves regional scope instead of flattening the three manuals into one universal rule. It also keeps the EU exception attached to the correct part of the process.

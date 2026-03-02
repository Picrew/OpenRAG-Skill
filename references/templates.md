# Prompt Templates

These templates are copy-paste ready. Replace the placeholders with the user's actual material.

## Raw Context Mode Template

```markdown
Use $rag to answer only from the material below.

[CONTEXT]
Source A:
<paste source A>

Source B:
<paste source B>

[TASK]
<state the question clearly>

[OUTPUT_MODE]
answer | extract | compare | audit
```

## Packaged Context Mode Template

```markdown
Use $rag to answer only from the evidence units below.

[E1] Source: <source label>
Section: <section label>
Content: <relevant text>
Notes: <optional scope, version, or date>

[E2] Source: <source label>
Section: <section label>
Content: <relevant text>

[TASK]
<state the question clearly>

[OUTPUT_MODE]
answer | extract | compare | audit
```

## Internal Work Product Templates

### Coverage Table

```text
Sub-question | Required? | Ideal evidence   | Candidate evidence | Force | Status
Q1           | Yes       | <what proves it> | E#                 | SHALL | Supported
Q2           | Yes       | <what proves it> | E#, E#             | SHOULD| Partial
Q3           | No        | <what proves it> | None               | None  | Gap
```

### Evidence Ledger

```text
Question | Direct support | Indirect support | Force | Gaps | Notes
Q1       | E#             | None             | SHALL | None | <why it is direct>
Q2       | E#, E#         | E#               | SHOULD| None | <joint support>
Q3       | None           | None             | None  | Yes  | <missing source>
```

### Conflict Ledger

```text
Claim | Related evidence | Conflict type   | Resolution | Output impact
Q1    | E# vs E#         | Scope           | Resolved   | Conditional by scope
Q2    | E# vs E#         | Version         | Unresolved | Ask for current version
Q3    | E# vs E#         | Normative force | Unresolved | Keep out of Shared Ground
```

### Final Sweep Checklist

```text
- Exceptions checked
- Dates and versions checked
- Scope boundaries checked
- Modal force checked
- Approval chains checked
```

### Normative Force Check

```text
E# -> SHALL
E# -> SHOULD
E# -> MAY

Rule:
- Do not merge unlike force levels into one unconditional statement.
```

## Output Mode Templates

### `answer` Mode

```markdown
Answer
- Direct conclusion. [E#]
- Supporting conclusion. [E#][E#]

Evidence Map
- Conclusion 1 -> [E#]
- Conclusion 2 -> [E#][E#]

Conflicts or Gaps
- No conflicts found.
```

### `extract` Mode

```markdown
Answer
- Field A: <value>. [E#]
- Field B: not found.

Evidence Map
- Field A -> [E#]
- Field B -> no supporting evidence

Conflicts or Gaps
- Field B is not stated in the provided material.
```

### `compare` Mode

```markdown
Answer
Shared Ground
- Shared point with matching scope and force, or `None.` if the overlap is only topical. [E#][E#]

Differences
- Source A [SHALL]: difference A. [E#]
- Source B [SHOULD/MAY]: difference B. [E#]

Conflicts
- No direct conflict.

Bottom Line
- Bounded comparison that only restates cited differences. [E#][E#]

Evidence Map
- Shared point -> [E#][E#]
- Difference A -> [E#][E#]
- Bottom line -> [E#][E#]

Conflicts or Gaps
- Scope differs by source.
```

Rule:
- Do not use `require`, `must`, or similar mandatory wording in `Shared Ground` unless every cited source uses matching mandatory force.
- If a detail is absent, say `not specified in the provided evidence`.

### `audit` Mode

```markdown
Answer
Requirements
- Requirement A. [E#]

Exceptions
- Exception A. [E#]

Gaps
- No documented gap in the provided material.

Risks
- Residual risk if the exception is applied broadly. [E#]

Evidence Map
- Requirement A -> [E#]
- Exception A -> [E#]
- Residual risk -> [E#]

Conflicts or Gaps
- No direct conflict found.
```

## Scenario Templates

### Short-Form Factual Prompt

```markdown
Use $rag to answer a factual question from the provided material only.

[CONTEXT]
Source A:
<paste the document excerpt>

[TASK]
What is the reimbursement cap for manager-approved client meals?

[OUTPUT_MODE]
answer
```

### Long-Document Audit Prompt

```markdown
Use $rag to audit the policy below.

[CONTEXT]
Source A:
<paste the policy text>

[TASK]
List every rule that controls vendor access to production systems. Keep all constraints and cite every material claim.

[OUTPUT_MODE]
audit
```

### Comparison Prompt

```markdown
Use $rag to compare the sources below.

[CONTEXT]
Source A:
<paste source A>

Source B:
<paste source B>

Source C:
<paste source C>

[TASK]
Compare the approval rules across the three sources and highlight conflicts or narrower exceptions.

[OUTPUT_MODE]
compare
```

## Failure-Handling Templates

### Missing Material Request

```markdown
Answer
INSUFFICIENT_EVIDENCE

Evidence Map
- No complete answer is possible from the provided material.

Conflicts or Gaps
- The provided evidence does not cover: <missing issue>.

Need More Material
- Please provide: <specific document, clause, version, or section>.
```

### Conflict-Conditioned Answer

```markdown
Answer
- If E2 governs, then <conditional conclusion>. [E2]
- If E5 is the current version, then <alternate conclusion>. [E5]
- The sources conflict and do not support a single unconditional conclusion. [E2][E5]

Evidence Map
- Conditional conclusion A -> [E2]
- Conditional conclusion B -> [E5]
- Conflict statement -> [E2][E5]

Conflicts or Gaps
- E2 and E5 disagree on <the disputed rule>.
```

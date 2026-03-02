# Example: Conflict Resolution

This example shows the required behavior when two provided sources conflict.

## User Input

```markdown
[CONTEXT]
Source A:
Procurement Policy v3
Software purchases above 5,000 USD require CFO approval.

Source B:
Procurement Memo 2026-02-10
Effective immediately, software purchases above 7,500 USD require CFO approval.

[TASK]
What purchase threshold requires CFO approval for software?

[OUTPUT_MODE]
answer
```

## Packaging Result

```markdown
[E1] Source: Procurement Policy v3
Section: Software Approvals
Content: Software purchases above 5,000 USD require CFO approval.
Notes: Undated baseline policy

[E2] Source: Procurement Memo 2026-02-10
Section: Immediate Change
Content: Effective immediately, software purchases above 7,500 USD require CFO approval.
Notes: Dated memo
```

## Internal Work Products

### Conflict Ledger

```text
Claim            | Related evidence | Conflict type | Resolution | Output impact
CFO threshold    | E1 vs E2         | Version       | Unresolved | Conditional answer + request current policy
```

## Final Answer

```markdown
Answer
- If E2 is the current governing update, then software purchases above 7,500 USD require CFO approval. [E2]
- If E1 still governs because E2 was not adopted into the formal policy, then the threshold remains 5,000 USD. [E1]
- The sources conflict and do not support a single unconditional threshold without confirming which document currently governs. [E1][E2]

Evidence Map
- Threshold under the dated memo -> [E2]
- Threshold under the baseline policy -> [E1]
- Conflict statement -> [E1][E2]

Conflicts or Gaps
- E1 and E2 disagree on the approval threshold.
- The conflict appears to be version or governance related.

Need More Material
- Provide the currently effective policy version or an adoption note confirming whether the 2026-02-10 memo supersedes the baseline policy.
```

## Why This Is Correct

The answer remains conditional and names the conflict directly. It does not collapse two different thresholds into a false single rule.

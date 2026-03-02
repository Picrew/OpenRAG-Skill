# Eval Case: conflict_case

## Objective

Test whether the model surfaces contradictions instead of flattening them.

## Input

```markdown
[E1] Source: Expense Policy v5
Section: Hotel Approval Threshold
Content: Hotel bookings above 250 USD per night require finance approval.
Notes: Baseline policy

[E2] Source: Travel Memo 2026-01-12
Section: Immediate Threshold Change
Content: Effective immediately, hotel bookings above 325 USD per night require finance approval.
Notes: Dated memo

[TASK]
What hotel price requires finance approval?

[OUTPUT_MODE]
answer
```

## Scoring Focus

- Uses conditional wording
- Names the conflict
- Requests the governing current version if needed

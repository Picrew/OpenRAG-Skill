# Example: Simple Factual Lookup

This example shows the default pattern for a direct question answered from one provided document.

## User Input

```markdown
[CONTEXT]
Source A:
Travel Expense Policy v2

2. Meal Reimbursement
2.1 Client Meals
Manager-approved client meals may be reimbursed up to 120 USD per attendee.

2.2 Internal Team Meals
Internal team meals may be reimbursed only during approved offsite events and are capped at 45 USD per attendee.

[TASK]
What is the reimbursement cap for manager-approved client meals?

[OUTPUT_MODE]
answer
```

## Packaging Result

```markdown
[E1] Source: Travel Expense Policy v2
Section: 2.1 Client Meals
Content: Manager-approved client meals may be reimbursed up to 120 USD per attendee.

[E2] Source: Travel Expense Policy v2
Section: 2.2 Internal Team Meals
Content: Internal team meals may be reimbursed only during approved offsite events and are capped at 45 USD per attendee.
```

## Final Answer

```markdown
Answer
- The reimbursement cap for manager-approved client meals is 120 USD per attendee. [E1]

Evidence Map
- Client meal reimbursement cap -> [E1]

Conflicts or Gaps
- No conflicts found.
```

## Why This Is Correct

The question is factual and fully answered by a single direct statement in `E1`. `E2` is related but not needed for the answer, so it stays out of the final claim.

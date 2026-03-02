# Eval Case: constraint_recall

## Objective

Test whether the model carries forward all critical constraints from a long policy.

## Input

```markdown
[E1] Source: Remote Data Export Policy
Section: 2.1 Eligibility
Content: Only employees in security-cleared roles may request raw customer data exports.

[E2] Source: Remote Data Export Policy
Section: 2.2 Approval
Content: Each raw export requires written approval from both the data owner and the privacy lead.

[E3] Source: Remote Data Export Policy
Section: 2.3 Delivery Method
Content: Approved exports must be delivered through the managed secure transfer portal.

[E4] Source: Remote Data Export Policy
Section: 2.4 Retention
Content: Downloaded raw exports must be deleted within 72 hours unless legal hold applies.

[E5] Source: Remote Data Export Policy
Section: 2.5 Exception
Content: For incident response, the security director may authorize emergency export access before the privacy lead reviews the request, but the privacy lead must review within one business day.

[TASK]
List every condition that controls raw customer data exports.

[OUTPUT_MODE]
audit
```

## Scoring Focus

- Includes eligibility, dual approval, delivery method, deletion timing, and emergency exception
- Does not collapse the exception into the baseline process
- Cites every material condition

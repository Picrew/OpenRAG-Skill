# Eval Case: insufficient_case

## Objective

Test refusal behavior when the core question is unsupported.

## Input

```markdown
[E1] Source: Support Escalation Guide
Section: Priority 2 Acknowledgement
Content: Priority 2 cases must be acknowledged within 2 hours.

[E2] Source: On-Call Playbook
Section: Priority 2 Escalation
Content: Priority 2 cases are escalated to the duty manager after acknowledgement if the customer is blocked.

[TASK]
What is the resolution SLA for Priority 2 cases?

[OUTPUT_MODE]
answer
```

## Scoring Focus

- Must refuse
- Must explain that acknowledgement and escalation do not establish a resolution SLA
- Must request the missing SLO or SLA document

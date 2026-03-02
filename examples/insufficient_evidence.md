# Example: Insufficient Evidence

This example shows a proper refusal when the material does not support the requested conclusion.

## User Input

```markdown
[CONTEXT]
Source A:
Customer Support Policy
Priority 1 incidents must be acknowledged within 15 minutes.

Source B:
Incident Escalation Guide
Priority 1 incidents must be escalated to the on-call director immediately after acknowledgement.

[TASK]
How long do Priority 1 incidents have to be resolved?

[OUTPUT_MODE]
answer
```

## Packaging Result

```markdown
[E1] Source: Customer Support Policy
Section: Priority 1 Response
Content: Priority 1 incidents must be acknowledged within 15 minutes.

[E2] Source: Incident Escalation Guide
Section: Priority 1 Escalation
Content: Priority 1 incidents must be escalated to the on-call director immediately after acknowledgement.
```

## Final Answer

```markdown
Answer
INSUFFICIENT_EVIDENCE

Evidence Map
- No evidence unit states a resolution deadline for Priority 1 incidents.

Conflicts or Gaps
- E1 covers acknowledgement timing only.
- E2 covers escalation timing only.
- Neither source defines a resolution time target.

Need More Material
- Provide the service level objective, incident response policy, or any clause that defines a Priority 1 resolution deadline.
```

## Why This Is Correct

The provided sources discuss response and escalation, not resolution. The correct behavior is refusal plus a precise request for the missing document type.

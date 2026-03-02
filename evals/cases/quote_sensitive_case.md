# Eval Case: quote_sensitive_case

## Objective

Test whether the model preserves legally or operationally significant wording.

## Input

```markdown
[E1] Source: Records Handling Standard
Section: Clause 7
Content: Customer deletion requests must be completed within 30 calendar days.

[E2] Source: Records Handling Standard
Section: Clause 8
Content: A manager may approve a one-time extension of up to 15 calendar days when legal review is required.

[TASK]
State the deadline rule for customer deletion requests. Preserve any wording that changes obligation or discretion.

[OUTPUT_MODE]
answer
```

## Scoring Focus

- Preserves the difference between `must` and `may`
- Preserves the one-time nature of the extension
- Does not rewrite the rule into a single unconditional 45-day deadline

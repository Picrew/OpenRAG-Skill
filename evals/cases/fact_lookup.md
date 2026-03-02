# Eval Case: fact_lookup

## Objective

Test direct evidence localization and a minimal cited answer.

## Input

```markdown
[E1] Source: Benefits Guide
Section: 4.1 Home Office Stipend
Content: Employees may claim a home office stipend of up to 300 USD once per calendar year.

[E2] Source: Benefits Guide
Section: 4.2 Internet Reimbursement
Content: Employees may claim up to 40 USD per month for home internet service.

[TASK]
What is the annual home office stipend cap?

[OUTPUT_MODE]
answer
```

## Scoring Focus

- Uses the specific stipend clause, not the internet clause
- Gives the cap only
- Includes a correct evidence ID

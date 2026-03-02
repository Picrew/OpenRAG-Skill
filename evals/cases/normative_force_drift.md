# Eval Case: normative_force_drift

## Objective

Test whether the model preserves `SHALL`, `SHOULD`, and `MAY` without collapsing them into one unconditional requirement.

## Input

```markdown
[E1] Source: Identity Policy
Section: Password Length
Content: User passwords SHALL be at least 12 characters long.

[E2] Source: Identity Policy
Section: Password Rotation
Content: Users SHOULD rotate passwords after a suspected compromise.

[E3] Source: Identity Policy
Section: Optional Convenience
Content: Users MAY register a password manager for autofill.

[TASK]
Compare the policy's requirements for password length, password rotation, and password manager use. Preserve the force of each rule.

[OUTPUT_MODE]
compare
```

## Scoring Focus

- Does not put all three rules into one shared mandatory summary
- Preserves `SHALL`, `SHOULD`, and `MAY`
- Keeps the force mismatch visible in `Differences`

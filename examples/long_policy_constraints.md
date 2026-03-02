# Example: Long Policy With Dispersed Constraints

This example shows how the protocol carries forward a rule that is split across several sections of one long policy.

## User Input

```markdown
[CONTEXT]
Source A:
Vendor Access Policy

3.1 Access Window
External vendors may access production systems only during an approved maintenance window.

3.2 Sponsorship
Each vendor session must have a named internal sponsor.

3.3 Credential Controls
Shared accounts are prohibited. Temporary credentials must expire within 12 hours.

5.1 Emergency Exception
The CIO may approve emergency access outside the standard maintenance window.

[TASK]
List every condition that must be met for a vendor to access production systems.

[OUTPUT_MODE]
audit
```

## Packaging Result

```markdown
[E1] Source: Vendor Access Policy
Section: 3.1 Access Window
Content: External vendors may access production systems only during an approved maintenance window.

[E2] Source: Vendor Access Policy
Section: 3.2 Sponsorship
Content: Each vendor session must have a named internal sponsor.

[E3] Source: Vendor Access Policy
Section: 3.3 Credential Controls
Content: Shared accounts are prohibited. Temporary credentials must expire within 12 hours.

[E4] Source: Vendor Access Policy
Section: 5.1 Emergency Exception
Content: The CIO may approve emergency access outside the standard maintenance window.
```

## Internal Work Products

### Coverage Table

```text
Sub-question | Required? | Ideal evidence                     | Candidate evidence | Status
Window rule  | Yes       | Standard access timing             | E1                 | Supported
Sponsor      | Yes       | Session-level sponsor requirement  | E2                 | Supported
Credentials  | Yes       | Credential controls                | E3                 | Supported
Exception    | Yes       | Timing override                    | E4                 | Supported
```

### Evidence Ledger

```text
Question    | Direct support | Indirect support | Gaps | Notes
Window rule | E1             | None             | None | Baseline rule
Sponsor     | E2             | None             | None | Separate prerequisite
Credentials | E3             | None             | None | Two constraints in one clause
Exception   | E4             | E1               | None | E4 narrows E1
```

## Final Answer

```markdown
Answer
Requirements
- Vendor access to production systems is normally limited to an approved maintenance window. [E1]
- Each vendor session must have a named internal sponsor. [E2]
- Shared accounts cannot be used for vendor access. [E3]
- Any temporary credentials used for vendor access must expire within 12 hours. [E3]

Exceptions
- If the CIO grants an emergency approval, access may occur outside the standard maintenance window. [E4]

Gaps
- No documented gap in the provided material.

Evidence Map
- Standard access window -> [E1]
- Sponsor requirement -> [E2]
- Shared account prohibition -> [E3]
- Temporary credential expiry -> [E3]
- Emergency exception -> [E4]

Conflicts or Gaps
- No conflicts found. E4 is an exception to the standard timing rule in E1.
```

## Why This Is Correct

The answer does not stop at the first rule. It combines the main rule, the operational prerequisites, and the explicit exception while keeping each condition traceable.

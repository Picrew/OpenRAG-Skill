# Detailed Protocol

This file expands the runtime instructions in `SKILL.md`. Use it when you need the full operating checklist, the intermediate work-product templates, and the mode-specific answer blueprints.

## Stage 1: Context Packaging

Goal: convert raw source material into stable `Evidence Units`.

Checklist:
- Separate each source before labeling evidence.
- Preserve author-visible structure: titles, headings, clause numbers, bullets, and paragraph boundaries.
- Use the smallest unit that can still stand on its own semantically.
- Keep dates, version labels, jurisdictions, and scope notes when present.
- Number evidence units sequentially (`E1`, `E2`, `E3`, ...).

Long-document rule:
- Package hierarchically whenever the source is long: source -> section -> clause.
- Keep exception clauses as separate evidence units even when they are adjacent to the main rule.

Do:
- Create more than one `Evidence Unit` when a long source contains multiple independent rules.
- Keep wording exact when the source is policy, legal, compliance, or quote-sensitive.

Do not:
- Collapse multiple clauses into one evidence unit if that would blur scope.
- Reword the source during packaging.
- Call this chunking or indexing.

### Work Product: Evidence Register

```text
E1 | Source | Section | Content | Notes
E2 | Source | Section | Content | Notes
```

## Stage 2: Query Decomposition And Coverage Planning

Goal: define the proof burden before drafting.

Checklist:
- Write the core question in one sentence.
- Split it into atomic sub-questions.
- Label the task type: `fact`, `rule`, `comparison`, `extraction`, or `audit`.
- Identify what evidence would directly answer each sub-question.
- Mark which sub-questions are mandatory for a complete answer.
- Mark which sub-questions are optional or follow-up only.

### Work Product: Coverage Table

Use this as the control surface for completeness.

```text
Sub-question | Required? | Ideal evidence | Candidate evidence | Force | Status
Q1           | Yes       | Direct rule     | E2, E4             | SHALL | Supported
Q2           | Yes       | Exception       | E6                 | SHALL | Supported
Q3           | No        | Missing field   | None               | None  | Gap
```

## Stage 3: Evidence Localization And Extraction

Goal: build the smallest evidence set that can support the answer.

Checklist:
- Match each sub-question to the most direct `Evidence Units`.
- Separate direct support from indirect support.
- Preserve exact wording where a wording shift would change the meaning.
- Mark unsupported sub-questions explicitly.
- Avoid filling gaps with outside knowledge.
- If two units are required together, record them as a combined support set rather than as interchangeable support.

Preferred decision order:
1. Direct statement in an `Evidence Unit`
2. Multiple units that jointly support the conclusion
3. Narrow, clearly labeled inference
4. No answer if support is still incomplete

### Work Product: Evidence Ledger

```text
Question | Direct support | Indirect support | Force  | Gaps | Notes
Q1       | E2             | None             | SHALL  | None | Direct policy text
Q2       | E6             | E4               | SHOULD | None | Exception narrows rule
Q3       | None           | None             | None   | Yes  | Missing source
```

## Stage 4: Cross-Check And Reconciliation

Goal: catch conflicts, hidden constraints, and scope mismatches before answering.

Checklist:
- Compare evidence units that touch the same claim.
- Check for scope differences (team, geography, role, product tier).
- Check for time differences (effective date, version, deprecated language).
- Check for specificity (exception clauses often override summary language).
- Check for normative force differences (`SHALL`, `SHOULD`, `MAY`, and negative forms).
- Record every unresolved conflict in a ledger.
- Keep contradictory text visible until a rule actually resolves it.

Priority rules:
1. More specific text beats general summaries.
2. Explicitly dated or versioned text beats undated text when the task depends on recency.
3. Exception clauses beat general rules when both apply.
4. If nothing resolves the conflict, the final answer must remain conditional.

### Work Product: Conflict Ledger

```text
Claim | Related evidence | Conflict type     | Resolution | Output impact
Q1    | E2 vs E5         | Version           | Unresolved | Conditional answer
Q2    | E4 vs E6         | Scope             | Resolved   | Cite narrower exception
Q3    | E3 vs E7         | Normative force   | Unresolved | Keep in Differences
```

## Final Sweep

Goal: catch omissions after the main evidence work is complete and before the final answer is drafted.

Run this exact sweep:
- Search the evidence register for exception language: `except`, `unless`, `however`, `only if`, `notwithstanding`.
- Search for dates, version labels, effective times, and sunset language.
- Search for scope boundaries: role, region, product tier, contract type, approval authority.
- Search for modal force: `must`, `may`, `should`, `prohibited`, `required`.
- Search for approval chains, fallback conditions, and time-based qualifiers.

If the sweep finds a controlling detail that is not already in the ledgers:
- add it to the relevant ledger,
- update the coverage status,
- and only then draft the answer.

## Stage 5: Cited Answer Generation

Goal: produce a stable, reviewable response.

Required section order:
1. `Answer`
2. `Evidence Map`
3. `Conflicts or Gaps`
4. `Need More Material` (only when partial or refused)

Checklist:
- Ensure every non-trivial claim in `Answer` ends with one or more evidence IDs.
- Ensure `Evidence Map` mirrors every major conclusion in `Answer`.
- Remove any sentence that cannot be traced to the evidence ledger.
- Keep the phrasing concise and scorable.
- Use conditional wording when a conflict remains open.
- Preserve exact wording when a small wording change would alter force, timing, or scope.
- Use no extra top-level section before `Answer` unless the user explicitly requests intermediate work products.
- Omit `Need More Material` entirely when the answer is complete.
- Never emit `Need More Material` with placeholder content such as `None.`.
- If a detail is absent, say `not specified in the provided evidence` rather than infer from category, naming, or common practice.
- Return the answer directly in the response; do not create helper files or artifacts unless explicitly requested.

## Normative Force Lock

This is a hard rule for normative or policy text:
- Preserve `SHALL`, `SHALL NOT`, `SHOULD`, `SHOULD NOT`, and `MAY` exactly in meaning.
- Do not summarize `SHOULD` or `MAY` as an unconditional requirement.
- Do not summarize `SHALL NOT` as a mere recommendation.
- If the same topic appears with different force across sources, record the mismatch in the ledgers before drafting.
- In normative comparisons, name the force explicitly inside each differing requirement.

In `compare` mode:
- `Shared Ground` is allowed only when both scope and normative force align.
- Different force with the same topic belongs in `Differences`, unless the mismatch itself is the central issue, in which case it belongs in `Conflicts`.
- If the only overlap is a broad topic, prefer `Shared Ground` = `None.` over a softened common summary.
- Never use words like `require`, `must`, or `prohibit` in `Shared Ground` unless every cited source supports the same mandatory force.

## Internal Work Products Stay Internal

`Evidence Register`, `Coverage Table`, `Evidence Ledger`, and `Conflict Ledger` are default-internal artifacts.

Do not emit them as extra top-level sections unless the user explicitly asks for the intermediate work products.
Do not emit TODO lists, planning notes, or scratch reasoning.

## Mode-Specific Answer Blueprints

`OUTPUT_MODE` changes the structure inside the `Answer` section, not the top-level section order.

### `answer`

Use:
- direct factual answers,
- direct rule statements,
- short explanatory conclusions grounded in evidence.

Blueprint:

```text
Answer
- Conclusion 1. [E#]
- Conclusion 2. [E#][E#]
```

### `extract`

Use:
- field extraction,
- checklist extraction,
- direct pull-through of values or quoted clauses.

Blueprint:

```text
Answer
- Field A: value. [E#]
- Field B: not found.
```

### `compare`

Use:
- source-to-source comparison,
- policy comparisons across regions or versions,
- side-by-side control differences.

Blueprint:

```text
Answer
Shared Ground
- Shared point with matching scope and force, or `None.` if the overlap is only topical. [E#][E#]

Differences
- Source A [SHALL]: difference A. [E#]
- Source B [SHOULD/MAY]: difference B. [E#]

Conflicts
- Conflict or "No direct conflict." [E#][E#]

Bottom Line
- Final bounded comparison that only restates cited differences. [E#][E#]
```

### `audit`

Use:
- compliance review,
- policy control summaries,
- “list every requirement” tasks.

Blueprint:

```text
Answer
Requirements
- Requirement A. [E#]

Exceptions
- Exception A. [E#]

Gaps
- Gap A or "No documented gap in the provided material."

Risks
- Risk A when relevant. [E#]
```

## Decision Tree: Answer vs Partial Answer vs Refusal

Use this sequence:

1. Is the core question supported by direct evidence?
   - If no, refuse.
   - If yes, continue.
2. Are all mandatory sub-questions supported?
   - If yes, give a full answer.
   - If no, give a partial answer.
3. Did the final sweep uncover a missing exception, scope boundary, or dated override?
   - If yes, update the ledgers before answering.
4. Are any unsupported details tempting but not evidenced?
   - If yes, omit them.

### Full Answer

Use when:
- The core question is supported.
- All mandatory sub-questions are supported.
- No unresolved conflict blocks a stable conclusion.

### Partial Answer

Use when:
- The core question is supported.
- One or more secondary or non-blocking sub-questions remain unsupported.

Requirements:
- Answer only the supported portions.
- List the missing parts in `Conflicts or Gaps`.
- Include `Need More Material`.

### Refusal

Use when:
- The core question is unsupported, or
- A conflict prevents any responsible unconditional answer and the task requires one.

Requirements:
- Set `Answer` to `INSUFFICIENT_EVIDENCE`.
- State the missing or contradictory support.
- Ask for the exact additional material needed.

## Decision Tree: Contradictions And Dated Sources

1. Do two evidence units disagree?
   - If no, proceed normally.
   - If yes, identify why.
2. Is the disagreement explained by scope?
   - If yes, answer conditionally by scope.
3. Is the disagreement explained by date or version?
   - If yes, answer conditionally by date or version unless the current one is explicit.
4. Is there a more specific exception clause?
   - If yes, apply the exception and cite both units.
5. If none of the above resolves it:
   - State that the sources conflict and do not support a single unconditional conclusion.

## Output Guardrails

- Never cite an evidence ID that does not actually support the attached claim.
- Never merge two nearby but different constraints into one simplified rule unless the source itself does so.
- Never replace a refusal with a generic best-practice answer.
- In quote-sensitive tasks, prefer exact quotation or tightly constrained paraphrase.
- Never let a mode-specific structure hide an unresolved gap or conflict.
- Never place a `SHOULD` or `MAY` claim into `Shared Ground` with a `SHALL` claim unless the output explicitly calls out the force mismatch.
- Never use softened topical overlap as a substitute for true shared ground.
- Never infer unstated properties from the name of a concept (for example, do not infer allowed character classes from the word `password`).
- Never introduce new comparative rationale in `Bottom Line` that was not already supported in `Differences`.

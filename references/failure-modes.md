# Failure Modes And Required Responses

This repository is deliberately strict about failure handling. The goal is not to always answer. The goal is to answer only when the evidence supports it.

## Insufficient Evidence

Symptoms:
- The core question is not directly addressed by any `Evidence Unit`.
- The source only covers adjacent topics.
- Required details such as scope, exceptions, or timing are missing.

Required response:
- Return `INSUFFICIENT_EVIDENCE`.
- State what is missing.
- Ask for the exact additional material needed.

Do not:
- Fill the gap with general knowledge.
- Convert an unsupported answer into a confident paraphrase.

## Hidden Assumptions

Symptoms:
- The user asks for a conclusion that depends on assumptions not stated in the source.
- The source uses role-, geography-, or product-specific rules and the request assumes they are universal.

Required response:
- Name the missing assumption.
- Limit the answer to what is explicitly supported.
- Mark the missing assumption as a gap.

## Unsupported Inference

Symptoms:
- The model adds a property that the source never states.
- The model infers behavior from category names, labels, or common industry practice.

Required response:
- Replace the inference with `not specified in the provided evidence`.
- Keep only the properties explicitly supported by the cited evidence.
- Do not introduce unstated rationale or defaults.

## Conflicting Clauses

Symptoms:
- Two sources or two clauses disagree on the same rule.
- A summary clause conflicts with a narrower exception.

Required response:
- Cite both sides of the conflict.
- Explain whether scope, date, version, or specificity resolves it.
- If not resolved, keep the answer conditional.

## Duplicated But Slightly Mismatched Statements

Symptoms:
- Two sources appear to repeat the same rule but differ on a detail such as a threshold, role, or timing.

Required response:
- Treat the mismatch as meaningful until proven otherwise.
- Do not merge the statements into a single softened summary.
- Surface the mismatch in `Conflicts or Gaps`.

## Process Leakage

Symptoms:
- The model prints TODO lists, ledgers, scratch reasoning, or planning notes.
- The model creates helper files or artifacts before returning the final answer.

Required response:
- Return only the contract-formatted answer unless the user explicitly asks for intermediate work products.
- Do not create files or external artifacts just to prepare the answer.

## Long Documents With Dispersed Constraints

Symptoms:
- The relevant rule is spread across multiple sections.
- A main rule appears in one place while exceptions, approvals, or limits appear elsewhere.

Required response:
- Gather all relevant `Evidence Units` before drafting.
- Do not answer from the first matching clause alone.
- Use `Evidence Map` to show the combined support for the final rule.

## Quote-Sensitive Tasks

Symptoms:
- A task depends on the difference between `must` and `may`, `before` and `after`, or other legally or operationally significant wording.

Required response:
- Preserve exact wording or quote tightly.
- Avoid casual paraphrase that changes force, timing, or scope.
- If you cannot preserve the wording safely, say so and cite the controlling evidence.

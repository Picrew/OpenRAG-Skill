# OpenRAG-Skill

<p align="left">
  <img src="./assets/icon-large.svg" alt="OpenRAG-Skill" width="440" />
</p>

[![Language English](https://img.shields.io/badge/Language-English-0B84D8?style=flat-square&labelColor=555555)](./README.md)
[![Language Simplified Chinese](https://img.shields.io/badge/%E8%AF%AD%E8%A8%80-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-E25544?style=flat-square&labelColor=555555)](./README_ZH.md)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-0B84D8?style=flat-square&labelColor=555555)](https://docs.anthropic.com/en/docs/claude-code/skills)
[![License MIT](https://img.shields.io/badge/License-MIT-87C400?style=flat-square&labelColor=555555)](./LICENSE)

OpenRAG-Skill is a focused Claude Code skill for evidence-first, prompt-only RAG when the source material is already in the chat. It does not search outside the conversation. Instead, it turns supplied text into referenceable evidence units, keeps every material claim attached to citations, and refuses cleanly when the record is incomplete.

## At A Glance

| This project is | This project is not |
| --- | --- |
| A practical skill for policies, manuals, contracts, specs, FAQs, and other long documents already in context | A vector search system |
| A prompt protocol that separates evidence handling from answer writing | A web, database, or external retrieval layer |
| A stable answer contract designed for review and evaluation | A replacement for search across large external corpora |
| A narrow tool with explicit boundaries | A general codebase search workflow |

## Best Fit

Use OpenRAG-Skill when:
- a user pasted the source material into the conversation,
- the chat history already contains the policy or manual,
- or the system prompt injected the reference text ahead of time.

If the source is not present, the correct behavior is simple: stop, state the gap, and ask for the missing material.

## What You Get

OpenRAG-Skill is built around a few deliberate guardrails:

| Capability | What it does in practice |
| --- | --- |
| Evidence Units | Turns raw material into stable, citeable evidence IDs |
| Two-pass workflow | Locates evidence before drafting the answer |
| Normative force lock | Keeps `SHALL`, `SHOULD`, and `MAY` from collapsing into the same summary |
| Output contract | Produces a consistent shape that is easy to review, compare, and score |
| Refusal discipline | Uses `INSUFFICIENT_EVIDENCE` instead of guessing |

## Protocol In One Pass

```text
Provided Context
  -> Evidence Units
  -> Coverage Table
  -> Evidence / Conflict Review
  -> Final Sweep
  -> Cited Answer
```

The workflow is intentionally plain:

1. Package the supplied text into `Evidence Units`.
2. Break the task into the minimum set of questions that must be proven.
3. Attach each sub-question to the smallest supporting evidence set.
4. Reconcile conflicts, scope limits, dates, versions, and exceptions.
5. Write the answer only after the evidence ledger is complete.

## Response Contract

The top-level response order is fixed:

```text
Answer
Evidence Map
Conflicts or Gaps
Need More Material   (only when partial or refused)
```

Working rules:
- Every material claim must cite evidence.
- Unsupported details stay out of the answer.
- If the source does not say it, the answer should say `not specified in the provided evidence`.
- Intermediate work products stay internal unless the user explicitly asks for them.

In `compare` mode, the standard is tighter:
- `Shared Ground` is valid only when scope and normative force match.
- If one source uses `SHALL` and another uses `SHOULD` or `MAY`, that belongs in `Differences`.
- If the overlap is only topical, `Shared Ground` should be `None.`
- `Bottom Line` should restate proven differences, not invent a broader theory.

## Install

Install the repo as a Claude Code skill, then keep the source material in the conversation and invoke `$rag`.

Personal install:

```bash
mkdir -p ~/.claude/skills/rag
cp -R . ~/.claude/skills/rag
```

Project-local install:

```bash
mkdir -p .claude/skills/rag
cp -R . .claude/skills/rag
```

## Starter Prompt

```markdown
Use $rag to answer only from the material below.

[CONTEXT]
Source A:
<paste the first document here>

Source B:
<paste the second document here>

[TASK]
Summarize the approval rules and cite every material claim.

[OUTPUT_MODE]
answer
```

## Why It Reads Better Than A Loose Prompt

Weak long-context answers usually fail in familiar ways: they stop at the first relevant clause, flatten an exception into the default rule, soften mandatory language, or improvise when the source is incomplete.

OpenRAG-Skill counters that with a tighter operating pattern:
- evidence first,
- force-sensitive comparison,
- no process leakage,
- and refusal when the evidence is not enough.

## Examples

- [`examples/document_qa.md`](./examples/document_qa.md): simple cited lookup
- [`examples/long_policy_constraints.md`](./examples/long_policy_constraints.md): dispersed constraints in one policy
- [`examples/conflict_resolution.md`](./examples/conflict_resolution.md): conflicting clauses and conditional output
- [`examples/insufficient_evidence.md`](./examples/insufficient_evidence.md): proper refusal
- [`examples/multi_source.md`](./examples/multi_source.md): multi-document comparison

## Evaluation

The repo includes a document-based evaluation pack in [`evals/`](./evals/):
- direct fact lookup,
- constraint recall,
- conflict handling,
- refusal behavior,
- citation alignment,
- normative-force drift,
- and quote-sensitive wording.

The goal is straightforward: the skill should be testable without hidden infrastructure.

## Repository Layout

```text
OpenRAG-Skill/
|-- SKILL.md
|-- README.md
|-- README_ZH.md
|-- agents/openai.yaml
|-- assets/
|-- references/
|-- examples/
|-- evals/
`-- LICENSE
```

## Publishing Notes

- The public project name is `OpenRAG-Skill`.
- The skill invocation remains `$rag`.
- The protocol is intentionally narrow. That boundary is part of the value, not a limitation to hide.

## License

Released under the MIT License. See [`LICENSE`](./LICENSE).

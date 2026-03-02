# Methodology: Why Prompt-Only Evidence Control Can Work

This repository does not claim to solve general retrieval. It claims something narrower and more defensible: when the relevant source material is already in context, a long-context model can often produce RAG-like reliability by following a strict evidence protocol instead of an external retrieval stack.

## The Central Boundary

This method works best when:
- The source material is already present in the prompt, the conversation, or directly pasted by the user.
- The task is to answer, extract, compare, or audit based on that material.
- Traceability matters more than raw retrieval speed.

This method does not work as a substitute for:
- Searching a large external corpus
- Discovering facts that were never provided
- Internet-scale or database-scale retrieval

That boundary is the difference between a credible prompt method and an overclaimed pseudo-RAG pitch.

## Why Long-Context Models Can Localize Evidence

When the source is already present, the main challenge is not retrieval infrastructure. The challenge is disciplined reading:
- identifying the parts of the text that matter,
- keeping references stable,
- carrying forward all critical constraints,
- and refusing unsupported claims.

Large context windows help only if the prompt creates structure. Without structure, long context increases the chance of omission, unsupported blending, and vague references.

The protocol in this repository adds that missing structure by:
- turning raw material into labeled evidence,
- decomposing the question before answering,
- and forcing a citation-aligned final schema.

## Evidence Units Are A Formatting Protocol, Not An Index

`Evidence Units` exist to make source text addressable.

They are:
- human-readable,
- easy to cite,
- stable enough for evaluation,
- and compatible with raw pasted material.

They are not:
- retrieval chunks,
- vector records,
- ranked search results,
- or an indexing layer.

The distinction matters because the purpose is different. A retrieval chunk exists to optimize a search system. An `Evidence Unit` exists to make already-available text auditable in a conversation.

## Why Two-Pass Answering Improves Reliability

Single-pass generation encourages the model to locate evidence and draft conclusions at the same time. That is where unsupported synthesis usually appears.

Two-pass answering separates those responsibilities:

1. First pass: identify and validate the relevant evidence.
2. Second pass: write only the claims that the validated evidence can support.

This improves quality in three ways:
- It reduces unsupported claims because unsupported ideas never enter the approved evidence set.
- It improves coverage because the model can check each sub-question against the evidence ledger.
- It makes errors easier to spot because the evidence-to-claim mapping is explicit.

## Why Conflict And Refusal Contracts Increase Trust

Many bad answers are not caused by missing intelligence. They are caused by missing rules about what to do when the evidence is incomplete or inconsistent.

This repository makes those rules explicit:
- If evidence conflicts, the model must surface the conflict and use conditional wording.
- If evidence is insufficient, the model must refuse and state what additional material is needed.
- If a claim is unsupported, it must be omitted.

These rules create a more trustworthy failure mode:
- fewer silent omissions,
- fewer flattened contradictions,
- and more predictable outputs for human review.

## Where This Method Is Strong

This method is particularly effective for:
- policy interpretation from provided handbooks,
- contract and clause comparison from pasted text,
- product or operations manuals already loaded into the chat,
- audit and checklist tasks where evidence traceability matters,
- long-form documents with dispersed constraints that must all be carried forward.

## Where This Method Is Weak

Performance degrades when:
- the source material is missing,
- the user provides only vague summaries instead of actual text,
- the task requires recall beyond the provided material,
- or the conversation mixes many unstructured documents without clear boundaries.

This method does not:
- solve internet-scale retrieval,
- retrieve from an external knowledge base,
- or create recall beyond the material already provided.

## Practical Positioning

The honest public positioning is:

“Use this skill when the information is already in context and the problem is evidence control, not external retrieval.”

That framing is narrower than traditional RAG marketing, but it is also the reason the method is believable and useful.

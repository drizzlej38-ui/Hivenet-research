# Research and Development Plan

**Status:** Proposed sequence; no implementation commitments yet  
**Date:** 2026-11-27

## Guiding strategy

Do not begin by building a new model, a large agent swarm, or a broad autonomous research platform.

First determine what existing systems already provide. Then test whether the missing pieces can be connected through stable interfaces. Build only the smallest independent component needed to demonstrate a real gap.

Scientific research and software/digital engineering are the initial proving grounds because they offer concrete sources, methods, test artifacts, and evaluation criteria. The architecture remains domain-neutral.

## Phase 0 — Prior-art and requirements audit

**Objective:** Establish the actual state of the art before selecting an implementation path.

Work:
- Inspect source code, documentation, interfaces, schemas, licenses, and release maturity of the closest candidate projects.
- Separate durable knowledge storage from investigation orchestration and discovery-loop behavior.
- Verify which systems accept external models and which merely support multiple providers internally.
- Identify the smallest common capability set.
- Record gaps as demonstrated, documented-but-unverified, partial, planned, or absent from public evidence.

Exit criteria:
- A comparison matrix grounded in inspected source and documentation.
- A shortlist of reusable components and integration constraints.
- An explicit statement of what remains unproven.
- A decision record: extend, compose, adapt, or build a minimal core.

## Phase 1 — Interface and data-contract prototype

**Objective:** Prove that the investigation record is independent of the model that uses it.

Minimal demonstration:
1. Client A creates an investigation.
2. The engine stores its scope, question, state, and initial evidence.
3. Client A submits a hypothesis and a bounded plan.
4. The engine validates and records them as proposals.
5. Client B, using a different model or client, retrieves the same investigation.
6. Client B contributes a counterargument or new evidence.
7. The engine preserves both contributions and their provenance.
8. A reviewer can inspect the record and its history.

Exit criteria:
- Stable identifiers and documented schemas.
- Successful cross-client continuation.
- No dependence on hidden conversational memory.
- Explicit separation of proposal, evidence, assessment, and accepted record.

## Phase 2 — Bounded investigation loop

**Objective:** Demonstrate an actual investigate–evaluate–revise cycle.

Initial domains:
- Software engineering: investigate a reproducible defect or architecture question.
- Scientific/data analysis: investigate a small, documented dataset or published result.

The loop should record the initial question and baseline; hypotheses and falsifiers; chosen method and reason; tool execution details; raw result and provenance; evaluation against predefined criteria; revised hypothesis or conclusion; remaining uncertainty and next question.

Exit criteria:
- At least one end-to-end investigation with reproducible evidence.
- Explicit blocked and failed outcomes.
- A second client can continue the investigation.
- The report does not overstate what the test establishes.

## Phase 3 — Cross-domain method packs

**Objective:** Preserve a shared investigation lifecycle while using domain-appropriate validation.

Begin with scientific research methods, software/digital engineering methods, and data science methods.

Evaluate whether method packs can define schemas, evidence requirements, review criteria, and safety boundaries without changing the core data model.

Exit criteria:
- The same core service supports at least two distinct domains.
- Domain-specific criteria are visible and versioned.
- No claim that one generic confidence score can replace domain validation.

## Phase 4 — Capability composition and optional agent collaboration

**Objective:** Test whether the engine can use different capabilities without requiring a fixed agent team.

Possible contributors include one model plus tools, multiple models with different roles, deterministic scripts and statistical tools, human expert review, and HiveNet nodes once their cooperation and refusal semantics are sufficiently established.

Measure whether additional agents actually improve evidence quality, coverage, or discovery outcomes relative to a single capable model and tools. Do not assume that more agents improve results.

Exit criteria:
- Replaceable adapters.
- Scoped permissions and bounded execution.
- Clear attribution for each contribution.
- Comparative evidence of when collaboration helps and when it adds cost or noise.

## Phase 5 — Discovery quality and novelty evaluation

**Objective:** Determine whether the system finds useful, non-obvious, supported relationships—not merely plausible summaries.

Use blinded or held-out tasks where possible. Compare against a human baseline, a single model without the engine, the same model with ordinary tools, an engine-assisted single model, and a multi-model or multi-agent configuration.

Record false positives, false negatives, unsupported novelty claims, reproducibility, and cost.

Exit criteria:
- Published evaluation protocol and test fixtures.
- Reproducible scoring.
- Limitations and negative results preserved.
- No novelty claim based solely on model assertion.

## Phase 6 — Optional HiveNet integration

**Objective:** Connect the engine to distributed capabilities without making either project dependent on the other.

Prerequisites:
- Mesh identity and capability declarations.
- Explicit accept/refuse behavior.
- Task lifecycle and result validation.
- Authenticated communication and permission boundaries.
- Failure handling and provenance across nodes.

Potential integration:
- Engine requests a bounded investigation capability.
- Mesh routes the request to eligible nodes.
- Each node retains local authority to accept or refuse.
- Results return with actor, method, source, and execution provenance.
- Engine evaluates and records contributions.
- Human/custodian policies govern sharing and promotion.

This phase does not replace or delay Mesh Lab's independent milestones.

## Initial experiment backlog

| ID | Experiment | What it tests |
|---|---|---|
| DE-001 | Cross-model investigation handoff | Model independence and durable continuity |
| DE-002 | Claim/evidence/contradiction record | Epistemic structure and provenance |
| DE-003 | Bounded software defect investigation | Engineering method and reproducibility |
| DE-004 | Dataset anomaly investigation | Data-science method and uncertainty |
| DE-005 | Same task, one model vs multiple agents | Whether collaboration adds measurable value |
| DE-006 | Resume after provider/model replacement | Independence from model session state |
| DE-007 | Refuse an unauthorized capability | Permission enforcement and safe boundaries |
| DE-008 | Cross-domain method-pack reuse | Generality of the core lifecycle |

## Development discipline

- Keep the research branch separate from implementation repositories until the implementation decision is made.
- Do not copy third-party code without checking license compatibility and attribution requirements.
- Record exact repository revision or release inspected.
- Keep research notes distinct from code, tests, and operational claims.
- Never report a planned feature as implemented.
- Prefer a small vertical slice over a broad architecture with no executable evidence.
- Preserve failed experiments and rejected approaches with reasons.

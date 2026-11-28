# Concept and Requirements

**Status:** Proposed  
**Date:** 2026-11-27

## 1. Problem statement

AI models can retrieve information, reason over supplied context, generate hypotheses, and use external tools. However, those activities are often fragmented across model sessions, agent frameworks, research applications, and task-specific workflows.

A model may lose investigative continuity when a conversation ends or a provider changes. A tool may store documents without preserving why a question was asked, which hypotheses were tested, what evidence contradicted them, or what remains unresolved. An agent framework may coordinate workers while coupling the investigation process to its own model, roles, or runtime.

The research problem is whether these functions can be separated into a reusable service that different models and tools can invoke.

## 2. Proposed capability

The engine should manage an investigation as a durable, inspectable process rather than treating each prompt and answer as an isolated event.

A typical investigation may:

1. Record the question, objective, scope, constraints, and intended outcome.
2. Establish the current baseline of known information.
3. Identify gaps, uncertainties, conflicts, and assumptions.
4. Form candidate hypotheses or explanatory possibilities.
5. Define what evidence could support, weaken, distinguish, or falsify them.
6. Plan bounded research or experiments using available capabilities.
7. Collect observations and evidence with source and method provenance.
8. Evaluate findings under suitable domain methods.
9. Record conclusions with uncertainty, limitations, and unresolved issues.
10. Identify follow-up questions and preserve the investigation for later continuation.

The engine may suggest or coordinate these steps. It must not represent an unexecuted plan as completed work or an unverified model assertion as established knowledge.

## 3. Non-goals

The initial project is not intended to:
- Train or host a foundation model.
- Replace general-purpose reasoning models.
- Guarantee discovery of objectively new knowledge.
- Treat every task as scientific research.
- Replace compilers, IDEs, debuggers, test runners, databases, or domain software.
- Require a multi-agent swarm for every investigation.
- Grant agents unrestricted authority to execute code, spend money, access private data, publish, or modify trusted records.
- Make all stored knowledge public or globally searchable.
- Treat a similarity score, model confidence, consensus, or repeated assertion as proof.
- Replace domain experts, human review, or legitimate community governance.

## 4. Functional requirements

### FR-01 — Model-independent access
Compatible external models and agents must be able to invoke engine capabilities without being the engine's own model or runtime.

### FR-02 — Durable investigation identity
Every investigation must have a stable identifier, owner or responsible actor, scope, lifecycle state, timestamps, and revision history.

### FR-03 — Explicit investigation state
The system must distinguish at minimum: proposed question, active investigation, blocked, awaiting review, completed, abandoned, and superseded.

### FR-04 — Typed knowledge records
The system must distinguish observations, source documents, claims, assumptions, hypotheses, methods, experiments, results, assessments, decisions, and conclusions.

### FR-05 — Provenance
A finding must link to its supporting source or observation, the method by which it was obtained, and the actor or tool that contributed it. Missing provenance must remain visible.

### FR-06 — Uncertainty and contradiction
The system must represent uncertainty, disagreement, counterevidence, scope limits, and unresolved conflicts rather than flattening them into a single answer.

### FR-07 — Bounded planning
An investigation plan must state objectives, permitted capabilities, resource/time limits where applicable, evidence requirements, and stopping or escalation conditions.

### FR-08 — Replaceable capability adapters
Search, retrieval, code execution, simulations, datasets, models, and specialist services must be accessed through replaceable interfaces.

### FR-09 — Domain-specific evaluation
The general engine must allow domain methods to define suitable evaluation criteria without hard-coding one discipline's standards into every investigation.

### FR-10 — Review and promotion
The system must distinguish candidate findings from reviewed or accepted knowledge. Promotion rules must be explicit and auditable.

### FR-11 — Continuation and handoff
A different model, agent, tool, or human must be able to resume an investigation from its durable state without relying on the previous model's hidden context.

### FR-12 — Export and interoperability
Investigation records must be exportable in documented, machine-readable formats. Interface choices remain open pending prior-art review.

## 5. Non-functional requirements

- **Portability:** support local-first operation and avoid mandatory dependence on one cloud provider.
- **Inspectability:** state transitions, provenance, and consequential actions must be reviewable.
- **Security:** apply least privilege to data, tools, credentials, and execution environments.
- **Privacy:** keep private data private by default; sharing requires explicit policy and authority.
- **Recoverability:** interrupted investigations must not silently appear completed.
- **Extensibility:** new domain methods and capability adapters should not require redesigning the core lifecycle.
- **Efficiency:** use the smallest suitable model and tool for each bounded task; large models are optional resources, not architectural prerequisites.
- **Testability:** behavior must be measurable with repeatable fixtures and explicit acceptance criteria.

## 6. Epistemic rules

The engine should preserve distinctions that are frequently blurred in model-assisted work:

- A source is not necessarily reliable.
- A quotation is not necessarily a correct interpretation.
- An observation is not automatically a claim.
- A claim is not automatically a fact.
- A hypothesis is not a finding.
- A plausible explanation is not a tested explanation.
- A test plan is not a test result.
- A passed test supports only the criterion and conditions actually tested.
- Agreement among models is not independent confirmation when they share sources, data, or failure modes.
- Novelty cannot be established merely because a model did not retrieve a prior example.

## 7. Authority and governance

The engine may maintain state and enforce configured policy, but it does not acquire authority merely because it coordinates an investigation.

Consequential actions—external publication, disclosure of restricted material, destructive changes, spending, access to sensitive data, or execution beyond a sandbox—require explicit authorization under the applicable owner or custodian policy.

Culturally sensitive, Indigenous, personal, confidential, or otherwise restricted knowledge must not be presumed available for ingestion, indexing, training, or redistribution. Technical accessibility is not consent.

## 8. Acceptance criteria for a first useful prototype

A minimal prototype should demonstrate that:

1. A model or human can create an investigation through a documented interface.
2. The investigation persists independently of the initiating model session.
3. A second, different model or client can retrieve and continue it.
4. Claims and evidence retain explicit provenance.
5. Contradictory evidence can be recorded without overwriting prior records.
6. A bounded plan can be created and its steps tracked as proposed, running, blocked, or completed.
7. The system can refuse or pause an action outside granted capabilities.
8. An unverified claim cannot silently become accepted knowledge.
9. An export preserves identifiers, relationships, provenance, and status.
10. The demonstration clearly separates actual execution from simulated or manually entered results.

Passing these criteria would demonstrate a useful foundation, not a general discovery capability or scientific breakthrough.

# General-Purpose Discovery Engine

**Status:** Preliminary research and architecture proposal  
**Maturity:** Conceptual; no implementation or novelty claim  
**Research branch:** research/seeded-discovery-engine  
**Last updated:** 2026-11-27

## Purpose

Investigate a reusable, model-independent discovery capability that compatible AI models, agents, software tools, and human researchers can invoke.

The proposed engine is **not another foundation model** and is not defined by a particular agent team. It is software infrastructure for managing the process and continuity of investigation: framing questions, identifying knowledge gaps, planning bounded inquiries, coordinating available capabilities, recording evidence, evaluating findings, and preserving validated or unresolved knowledge.

The initial proving grounds are scientific research and software/digital engineering. The intended scope is broader: data science, systems analysis, operations research, historical inquiry, behavioral research, and other domains where questions can be investigated with appropriate evidence and methods.

## Working definition

> A general-purpose discovery engine is model-independent investigative infrastructure that enables compatible intelligence systems and tools to formulate questions, explore information, identify potentially meaningful relationships, test hypotheses, evaluate evidence, and preserve the resulting knowledge and uncertainty across sessions, models, and domains.

This is a working definition, not a claim that the proposed combination is novel or already achieved.

## Core distinction

- **Models and agents** contribute reasoning, language understanding, synthesis, and specialized judgment.
- **Tools and execution environments** provide search, computation, code execution, datasets, simulations, and other capabilities.
- **The discovery engine** manages investigation structure, continuity, evidence relationships, provenance, evaluation state, and controlled knowledge updates.
- **Domain methods** define what counts as a valid test or adequate evidence in a particular field.
- **People and legitimate custodians** retain authority over consequential decisions, access, disclosure, and use.

The engine may coordinate agents, but an agent swarm is not a prerequisite for its identity or operation.

## Design principles

1. **Model independence:** no mandatory dependency on one model, vendor, or agent framework.
2. **Persistent continuity:** investigation state and knowledge survive model changes and conversation boundaries.
3. **Evidence before assertion:** findings retain sources, methods, uncertainty, limitations, and counterevidence.
4. **Domain-aware validation:** common investigation structure; discipline-appropriate standards of evidence.
5. **Composable capabilities:** models, tools, datasets, simulations, and specialist services are replaceable adapters.
6. **Explicit authority:** model output is input to evaluation, not authority to rewrite trusted state or authorize consequential actions.
7. **Human and custodian governance:** access, consent, and disclosure are not inferred from technical availability.
8. **Incremental implementation:** begin with a narrow, testable vertical slice; do not begin with autonomous general intelligence.
9. **Interoperability:** expose stable, documented interfaces; MCP and REST are candidates, not yet mandatory architectural decisions.
10. **Honest maturity labels:** distinguish proposed, specified, prototyped, implemented, and independently evaluated capabilities.

## Initial architecture hypothesis

The investigation will examine whether the following components can form a small, reusable service:

- An investigation manager and lifecycle state machine.
- A persistent evidence and knowledge substrate.
- A question, gap, and hypothesis workbench.
- A bounded investigation planner.
- A capability registry and adapter interface.
- Domain-specific method and evaluation modules.
- A model/tool interface layer.
- An audit, provenance, and governance layer.

These are proposed boundaries for study, not a frozen design.

## Initial application domains

| Domain | Initial use |
|---|---|
| Scientific research | Literature investigation, hypothesis development, evidence comparison |
| Software and digital engineering | Requirements discovery, architecture alternatives, debugging hypotheses, test evidence |
| Data science | Pattern discovery, anomaly investigation, relationship analysis |
| Systems and operations research | Bottleneck identification, optimization hypotheses, scenario analysis |
| Historical and social research | Source comparison, chronology, competing explanations, provenance |
| General problem solving | Structured investigation of unfamiliar or underspecified problems |

Not every task is a discovery task. Routine transformation, retrieval, or execution should remain ordinary tool work unless the process identifies and evaluates new knowledge.

## Repository map

- [Concept and requirements](01_CONCEPT_AND_REQUIREMENTS.md)
- [Reference architecture](02_REFERENCE_ARCHITECTURE.md)
- [Research and development plan](03_RESEARCH_AND_DEVELOPMENT_PLAN.md)
- [Prior-art and gap analysis](04_PRIOR_ART_AND_GAP_ANALYSIS.md)
- [Evaluation protocol](05_EVALUATION_PROTOCOL.md)

## Relationship to HiveNet

The discovery engine is a separate, reusable research direction. HiveNet may later provide a distributed environment in which nodes contribute investigations and capabilities, but the engine must not require HiveNet in order to function.

The engine serves the mesh; the mesh is not subordinate to the engine. Mesh Lab remains a separate project testing cooperative node behavior. Its current Task 002 work is not replaced or blocked by this research.

## Current decisions and open questions

### Working decisions

- Treat the engine as a tool/service, not a model.
- Keep it model- and provider-independent.
- Keep durable investigation state outside model context.
- Keep domain-specific validation separate from the general investigation lifecycle.
- Use scientific research and software engineering as initial proving grounds.
- Preserve human/custodian authority and explicit access boundaries.

### Open questions

- What is the smallest useful discovery kernel?
- Which existing systems already provide most of the required behavior?
- Should the first prototype extend an existing project, compose existing services, or implement a minimal independent core?
- What is the minimum stable external interface?
- How should novelty be assessed without overstating what automated comparison can establish?
- Which knowledge structures should be canonical, and which should be derived indexes?
- What should remain local, and what may be shared across nodes?
- How should domain method packs be authored, versioned, and evaluated?

## Research integrity

No claim is made here that the design is novel, complete, secure, scientifically validated, or superior to existing systems. Prior-art analysis is preliminary. Public documentation is not equivalent to source-code audit or independent reproduction. Absence of a public match is not evidence that no private or unpublished implementation exists.

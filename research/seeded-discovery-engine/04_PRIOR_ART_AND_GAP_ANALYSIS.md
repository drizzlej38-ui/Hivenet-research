# Prior-Art and Gap Analysis

**Status:** Preliminary public-source review; not an exhaustive literature or code audit  
**Review date:** 2026-11-27

## 1. Purpose

Identify existing systems that overlap with the proposed model-independent, general-purpose discovery engine. The purpose is to avoid reinventing existing work and to locate any genuine architectural or capability gap.

This review distinguishes a published concept from an implemented capability; a public API from a stable, general-purpose interface; model-provider flexibility from full model independence; persistent research memory from an active discovery loop; agent orchestration from a reusable discovery service; and a project's stated capabilities from independently verified behavior.

## 2. Closest identified projects

### OpenArx Core
Repository: https://github.com/OpenArx-AI/openarx-core

OpenArx describes itself as AI-native scientific and engineering knowledge infrastructure. Its public documentation describes an MCP-facing knowledge layer for external agents, a graph of claims and typed relationships, source ingestion and semantic retrieval, a methodology engine that guides and reviews staged research contributions, and a role-based interface for agents to search, read, and contribute.

**Overlap:** Very strong on model-facing knowledge infrastructure, evidence relationships, methodology checkpoints, and contribution governance.

**Questions to verify:** How much of the discovery cycle is engine-directed versus agent-directed? Can it independently identify gaps and initiate investigations? How readily can its scientific/engineering model generalize to non-research domains? What are its current operational and licensing constraints? The repository describes itself as public alpha; API and schema maturity must be checked.

### Gnomon — SkillSpringAI
Repository: https://github.com/SkillSpringAI/Gnomon

This project describes itself as local-first research infrastructure for persistent, evidence-aware investigations. Its documentation lists investigation briefs, questions, hypotheses, plans, and bounded cycles; persistent sources, claims, provenance, assessments, and audit history; deterministic planning and lifecycle controls; replaceable provider boundaries; a bounded fake-agent network; and explicit rules that model output is a proposal, not system authority.

It also documents significant incomplete areas, including live external-agent networks, semantic/vector memory, long-running worker orchestration, and production-grade autonomous tool execution.

**Overlap:** Very strong on the investigation lifecycle, evidence governance, persistence, bounded planning, and replaceable model/provider boundaries.

**Questions to verify:** How general are its research methods and domain assumptions? What external interfaces are stable? How complete are the provider and agent boundaries? Can it be used as a tool by arbitrary clients without adopting its full runtime?

### RKA Core
Repository: https://github.com/rka-project/rka-core

RKA describes itself as a local-first research operating system for durable, auditable research knowledge. Its documentation describes persistent records for observations, decisions, experiments, and failures; claims, evidence clusters, provenance, and research questions; MCP, REST, CLI, and dashboard interfaces; researcher-controlled workflows and bounded missions; and separation between the knowledge record and the model that performs synthesis.

**Overlap:** Strong on persistent continuity, model/client interoperability, provenance, and researcher-controlled knowledge management.

**Difference:** RKA explicitly positions itself as research infrastructure, not an autonomous discovery agent. It preserves and serves the record while external collaborators perform synthesis and investigation.

**Questions to verify:** How much of its data model and workflow can be generalized beyond research projects? What is available in the released Core versus separate or planned components? What interfaces and deployment modes are currently supported?

### CuriosityEngine
Repository: https://github.com/sfw/CuriosityEngine

Its public description presents a research loop that generates questions, investigates them using web and academic sources plus code execution, compares findings with prior knowledge, and uses an adversarial verifier before retaining candidate insights. It claims intended applicability across domains including AI, biology, investing, marketing, and governance.

**Overlap:** Strong on the discovery loop itself, autonomous question generation, hypothesis investigation, novelty-oriented verification, and cross-domain ambition.

**Difference:** It is presented as a standalone research application with its own orchestration and provider configuration, rather than clearly established as a neutral discovery service callable by arbitrary external models.

**Questions to verify:** Can its discovery process be invoked as a stable external capability? Can a separate model initiate, inspect, contribute to, and resume investigations? What constitutes independent verification of novelty? How are source coverage and false novelty claims measured?

## 3. Other relevant systems

### Sakana AI — The AI Scientist
Project: https://github.com/SakanaAI/AI-Scientist

An agentic scientific research workflow that proposes ideas, implements experiments, runs evaluations, and produces research outputs.

**Relevance:** Demonstrates automated research workflows and agent/tool coordination.

**Difference:** Primarily an agentic research system, not a general-purpose model-independent discovery service.

### FutureHouse
Project: https://www.futurehouse.org/

A collection of specialized AI research agents and scientific tools.

**Relevance:** Demonstrates decomposition of scientific research into specialized capabilities.

**Difference:** Scientific domain orientation and agent/service packaging; not necessarily a general-purpose discovery kernel.

### Google AI Co-Scientist
Publication: https://www.nature.com/articles/s41586-025-09406-7

A multi-agent scientific hypothesis-generation and evaluation system.

**Relevance:** Demonstrates specialized agents collaborating on scientific reasoning and hypothesis refinement.

**Difference:** Model-centered research system, not a neutral external discovery service.

## 4. Preliminary comparison

| Capability | OpenArx | Gnomon | RKA Core | CuriosityEngine |
|---|---|---|---|---|
| External model/client access | MCP | API/provider boundaries; verify client surface | MCP/REST/CLI | Verify external service interface |
| Persistent research state | Yes | Yes | Yes | Durable register described |
| Evidence and provenance | Yes | Yes | Yes | Sources and verification described |
| Investigation lifecycle | Methodology stages | Explicit bounded cycles | Research workflows | Autonomous research loop |
| Gap/question generation | Partial / verify | Questions and planning | Research questions; verify automation | Yes, per project description |
| Domain generality | Science/engineering focus | Research focus; verify | Research focus | Claims cross-domain use |
| Model independence | Strong interface intent | Replaceable provider boundary | Strong separation of record and model | Not yet established |
| Arbitrary model as external tool | MCP clients | Verify actual interface | MCP/REST clients | Not yet established |
| Autonomous discovery | Partial / verify | Bounded and partial capabilities | Not its primary role | Central project claim |

This matrix is a preliminary reading of public project documentation. It is not a feature-by-feature code audit, and “not yet established” does not mean a capability is absent.

## 5. Preliminary gap hypothesis

The most promising research gap is not simply persistent memory, agent orchestration, or hypothesis generation. Each already has substantial prior art.

The potential gap is a cleanly separated, reusable discovery service that combines:

1. A model-independent external interface.
2. Durable investigation state independent of any one agent or research application.
3. A general investigation lifecycle that can be applied across domains.
4. Domain-specific method packs for valid evaluation.
5. Replaceable model, agent, and tool capabilities.
6. Evidence, provenance, uncertainty, contradiction, and review as first-class records.
7. Optional distributed execution without requiring a fixed swarm or one network architecture.
8. A measurable discovery-quality evaluation protocol.

This combination may already exist in an implementation not identified in this preliminary review. No novelty claim should be made until a deeper source audit and literature review are completed.

## 6. Required next audit

For each closest candidate, inspect license and reuse obligations; repository activity, releases, and maturity; data model and canonical record types; investigation lifecycle and state transitions; external interfaces and authentication; model/provider abstraction; capability/tool adapter model; provenance and audit guarantees; human review and authority boundaries; actual tests and reproducible examples; domain assumptions and extension points; deployment requirements and local-first support.

Then run a small interoperability experiment where two different clients use the same persistent investigation without sharing hidden conversation context.

## 7. Research conclusion

Public prior art already covers much of the proposed capability. OpenArx, Gnomon, RKA Core, and CuriosityEngine are especially relevant, but they emphasize different parts of the problem.

The responsible next step is comparative implementation inspection and interoperability testing—not immediately building a competing platform.

A lack of an identified complete public match would not establish that no such system exists privately, commercially, or under another name.

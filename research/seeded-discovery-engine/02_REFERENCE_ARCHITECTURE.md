# Reference Architecture Proposal

**Status:** Proposed architecture for investigation  
**Date:** 2026-11-27

## 1. Architectural objective

Separate the durable investigation process from the intelligence systems and external capabilities that contribute to it.

The engine should be usable as a service by different models, agents, applications, and human operators. Its core responsibility is to preserve and govern the investigation lifecycle—not to generate all reasoning itself.

## 2. Logical layers

### A. External clients

Potential clients include general-purpose language models, specialized models and agents, IDEs and software-development agents, research applications, human-facing CLI or GUI clients, and HiveNet nodes or other distributed systems. No single client is mandatory.

### B. Interface and identity boundary

A documented interface accepts requests, authenticates the calling actor, checks permissions, validates input, and returns structured results.

Candidate interfaces:
- MCP for tool-oriented model and agent access.
- REST for application and service integration.
- CLI for local administration and reproducible workflows.
- Language SDKs only when stable contracts justify them.

These are candidates, not a decision to implement all interfaces in the first version.

### C. Investigation core

Responsible for investigation creation and identity; scope, objectives, constraints, and lifecycle; questions, assumptions, hypotheses, and plans; task decomposition and bounded scheduling; state transitions, checkpoints, blocking, recovery, and closure; follow-up question generation and continuation.

The core should be deterministic where practical. A model may propose a transition or plan, but application rules validate whether the transition is permitted.

### D. Knowledge and evidence substrate

Stores durable, typed records such as:

| Record | Meaning |
|---|---|
| Investigation | The persistent inquiry and its scope |
| Question | Something the investigation seeks to resolve |
| Assumption | A provisional premise that may require testing |
| Hypothesis | A proposed explanation or relationship |
| Source | A document, dataset, artifact, person, or external reference |
| Observation | A recorded result or extracted observation |
| Claim | A proposition that can be evaluated |
| Method | The procedure used to obtain or assess evidence |
| Experiment | A planned or executed test |
| Result | The recorded outcome of a method or experiment |
| Assessment | An evaluation of a claim or hypothesis |
| Decision | A human or policy-authorized choice |
| Conclusion | A scoped synthesis of the current evidence |

Records should have stable identifiers and explicit relationships. Append-only history or equivalent revision tracking should preserve material changes and supersession.

### E. Discovery planning and evaluation

This layer supports a repeatable investigation cycle:

1. Frame the question.
2. Establish baseline knowledge.
3. Detect gaps, contradictions, and uncertainty.
4. Propose hypotheses or candidate relationships.
5. Select methods and evidence requirements.
6. Plan bounded investigations.
7. Collect results.
8. Evaluate evidence and alternatives.
9. Update the knowledge record under policy.
10. Decide whether to continue, stop, or escalate.

The first version may rely on an external model to propose questions and hypotheses. The engine's responsibility is to structure, track, constrain, and evaluate the process—not to claim autonomous insight where none has been demonstrated.

### F. Capability registry and adapters

Capabilities are separately registered and invoked through constrained adapters.

Examples include web and academic search, local document and repository search, database queries, code execution in a sandbox, test runners, simulators, scientific computing tools, dataset analysis, specialist services, and human review.

A capability declaration should include its identifier, description, input/output schema, permissions, limits, dependencies, and verification expectations. The engine must not infer capability from an agent's self-description alone.

### G. Domain method packs

The general lifecycle is shared, but evaluation rules vary by domain.

A method pack may define required source types, accepted methods, evidence quality criteria, statistical or experimental requirements, reproducibility expectations, safety and ethical constraints, review roles, escalation conditions, and domain-specific result schemas.

Initial candidates:
- Scientific research.
- Software and digital engineering.
- Data science and statistical analysis.

Additional domains should be added only with appropriate methods and evaluation criteria.

### H. Governance, audit, and security

Cross-cutting responsibilities include actor identity and attribution, authorization and least privilege, tool and data access policy, audit history, secret handling, data retention and deletion policy, human approval gates, export and sharing controls, and safe failure and recovery.

## 3. Conceptual interaction

    Human / Model / Agent / Application
                    |
             Authenticated API
                    |
            Investigation Core
              /           \
       Knowledge Store   Planner
              \           /
             Capability Adapters
                    |
        Models / Tools / Data / Experts
                    |
          Evidence and Result Records
                    |
          Evaluation and Review
                    |
          Governed Knowledge Update

This is a logical view, not a deployment diagram. Components may initially run in one process.

## 4. Investigation lifecycle

Suggested lifecycle states:

- **draft** — question and scope are being framed.
- **ready** — required scope and initial criteria are present.
- **active** — bounded investigation work is underway.
- **blocked** — a dependency, permission, or missing capability prevents progress.
- **review** — evidence or proposed conclusions await evaluation.
- **completed** — the stated objective has been addressed to the recorded standard.
- **abandoned** — work was intentionally stopped without claiming success.
- **superseded** — a later investigation replaces or extends this one.

State transitions must be explicit and recorded. A completed investigation may still contain unresolved questions; completion means the defined objective reached its declared stopping condition, not that all uncertainty disappeared.

## 5. Model and agent contract

External models should be able to create or retrieve an investigation within their permissions; read relevant context and unresolved questions; propose hypotheses, plans, and interpretations; submit observations or evidence with provenance; request permitted capabilities; report blockers and uncertainty; propose a conclusion for review; and resume work after a handoff.

External models should not be able to rewrite immutable history, promote their own unsupported claims to accepted knowledge, expand their permissions by self-declaration, mark unexecuted work as executed, bypass configured review or authorization gates, or treat retrieved documents and tool output as privileged instructions.

The engine should return explicit status, identifiers, validation errors, and next permitted actions rather than relying on conversational implication.

## 6. Persistence and indexing

The canonical record should be structured and durable. Search indexes, embeddings, graph projections, summaries, and cached context should be treated as derived representations that can be rebuilt from canonical records where feasible.

This avoids making a particular vector database, graph database, embedding model, or LLM the authority for what the investigation contains.

Storage technology is intentionally undecided. A local-first relational store with explicit typed relationships may be sufficient for an initial prototype; graph and semantic indexes can be evaluated against actual retrieval requirements.

## 7. Security boundaries

- Treat all external content, retrieved documents, model messages, and tool outputs as untrusted input.
- Keep credentials outside prompts, records, reports, and logs.
- Require explicit allowlists and scoped permissions for network and filesystem access.
- Execute untrusted code only in an appropriately isolated environment.
- Apply resource, time, and output limits to tool calls.
- Record whether a result came from a live execution, cached result, simulation, fixture, or manual entry.
- Make partial failures and unknown outcomes visible.
- Do not equate a hash with authenticity, authorization, or truth.

## 8. HiveNet integration boundary

HiveNet may later supply distributed capability discovery, routing, worker nodes, and cooperative execution. The engine should communicate through stable interfaces and should not depend on HiveNet's internal topology.

A HiveNet node may host an engine instance, provide a capability, or participate in an investigation under local policy. Participation must remain opt-in, scoped, and revocable. A node's ability to receive a task does not imply acceptance or authorization to execute it.

## 9. Decisions intentionally deferred

Database and graph technology; MCP versus REST as the first interface; whether the first version is a library, local service, or both; whether planning is deterministic, model-assisted, or hybrid; how novelty is estimated and reported; how cross-domain method packs are represented; multi-user tenancy and distributed consensus; hosted deployment and shared knowledge federation.

These decisions should follow prior-art inspection and a minimal prototype, not precede them.

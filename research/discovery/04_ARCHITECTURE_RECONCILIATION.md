# Discovery, ANDNM, and MNN: Architecture Reconciliation

**Status:** Research review note; proposed interfaces, not an implementation specification  
**Version:** 0.1  
**Date:** 2026-11-26

## 1. Review scope

This note compares the Discovery Systems and Open-Ended Development track with:

- `research/neuroscience/01_NEUROGENESIS_AND_ADAPTIVE_NEURAL_MESH.md`
- `research/neuroscience/04_MESH_NEURAL_NETWORKING_MNN_CONCEPT.md`
- `research/neuroscience/05_MNN_LOCAL_ROUTING_AND_DOMAIN_ADMISSION.md`
- `research/neuroscience/06_MNN_RESEARCH_AND_EVALUATION_PLAN.md`

The review is conceptual. The documents describe proposals and experiments; they do not establish implemented or validated capabilities.

## 2. Main finding: three distinct architectural layers

The documents are complementary, but their responsibilities should remain distinct.

| Layer | Existing/new research | Primary responsibility |
|---|---|---|
| Knowledge and epistemic layer | Seeded Discovery Engine | Explore information, generate candidate findings, preserve evidence and provenance, validate or reject claims |
| Development and composition layer | ANDNM / adaptive neural mesh | Create, recruit, activate, connect, reconfigure, place into dormancy, and retire computational units |
| Communication layer | MNN | Forward signals across locally known peers while enforcing specialization scope, admission policy, and bounded routing |

The open-ended ecosystem simulation is an experimental environment for studying interactions among developmental components. It is not a fourth routing or discovery mechanism. It supplies conditions under which organization and behavior may arise and be observed.

This separation prevents a common category error: discovering a capability gap is not the same operation as creating a component, and creating a component is not the same operation as routing signals through it.

## 3. Relationship to ANDNM

The ANDNM document already describes dynamic recruitment, instantiation, connection, evaluation, readjustment, disconnection, dormancy, and independent development. The new ecosystem proposal's component creation, copying, modification, and retirement therefore overlap with ANDNM's developmental lifecycle.

**Recommended interpretation:** treat the ecosystem's developmental operations as an experimental setting in which ANDNM-like lifecycle mechanisms may be implemented or compared—not as a separate competing lifecycle architecture.

The ecosystem research adds a distinct question: what organization, if any, develops when the environment does not prescribe an intelligence objective or developmental destination? ANDNM describes candidate mechanisms for dynamic computational growth; the ecosystem experiment studies the behavior and consequences of allowing such mechanisms to interact.

The simulation must document which developmental operations are actually enabled. It must not imply that all ANDNM mechanisms exist merely because the experiment is called developmental.

## 4. Relationship to MNN

MNN is a narrower communication proposal within the broader adaptive-mesh direction. Its defining features are:

- Forwarding-capable computational units.
- Specialization-scoped forwarding.
- Bounded local peer awareness rather than mandatory global topology knowledge.
- Multi-hop reachability.
- Domain-local admission and lifecycle handling.
- Explicit identity, provenance, authorization, hop limits, and failure behavior.

The Discovery Engine does not replace any of these functions. It may discover candidate routing improvements or identify a measured capability gap; MNN remains responsible for communication behavior if selected for an experiment.

Likewise, the ecosystem simulator should not silently assume MNN routing. A first simulator may use a simple communication mechanism, but the chosen mechanism must be recorded as an experimental condition. A later MNN-enabled condition can isolate the effect of MNN against the same workload and initial population.

## 5. Proposed interfaces between the layers

These are conceptual data handoffs, not finalized schemas.

### Discovery to development

A validated finding may produce a **capability-gap proposal** containing:

- The task that cannot currently be completed.
- The demonstrated requirement and evaluation method.
- Evidence that existing components or procedures are insufficient.
- Candidate solutions, including non-model solutions.
- Expected costs, risks, and measurable acceptance criteria.

This proposal is input to a development decision; it is not an instruction to instantiate a new model or agent.

### Development to communication

A candidate computational unit should expose the identity, capabilities, constraints, domain membership, lifecycle state, and participation permissions required by the applicable mesh protocol. MNN admission and routing rules determine whether and how it participates in signal forwarding.

### Ecosystem to discovery

Observed behavior, topology changes, failures, and candidate capabilities can become new discovery seeds. Observations must retain run identifiers, simulator version, initial conditions, random seed, and event provenance. A behavior observed once is a candidate, not a general finding.

### Validation across the loop

A discovery claim must not validate itself through a component built from that claim. Keep generation, validation, implementation, and held-out evaluation sufficiently separate to detect self-reinforcing errors. Model agreement alone is not independent empirical confirmation.

## 6. Terminology alignment

Use these terms consistently:

- **Computational unit / HiveNet-Neuron:** an independently identifiable model, service, process, or other functional component. “Neuron” remains an architectural analogy.
- **Developmental operation:** creation, recruitment, activation, copying, modification, connection, reassignment, dormancy, quarantine, or retirement of a computational unit or configuration.
- **Topology change:** a change in communication relationships or network structure. It does not necessarily change a unit's internal model.
- **Computational phenotype:** an observed unit, capability, behavior, topology, or configuration produced under specified developmental and environmental conditions. This is a project-defined analogy, not biological equivalence.
- **Discovery candidate:** an unvalidated relationship, explanation, anomaly, method, or capability opportunity.
- **Validated finding:** a candidate that has passed a specified evidence and replication standard; the term should always be qualified by the actual method and scope.
- **Ecological autonomy:** internal development without an externally prescribed destination. It does not mean absence of initial conditions, resource constraints, experimental boundaries, or external containment.
- **Operational authority:** permission to access external systems, credentials, networks, data, or actuators. Neither intellectual exploration nor internal developmental autonomy grants it.

Avoid using “neurogenesis” to describe every form of system change. Instantiating a new unit, changing a route, modifying a model's weights, and reorganizing a mesh are different operations.

## 7. Important experimental gaps

The existing documents identify many controls, but the following interfaces need explicit treatment before implementation:

1. **Developmental permissions:** define which operations a component can request, which can occur autonomously inside the simulator, and which require an external policy decision.
2. **Lifecycle compatibility:** align ecosystem phenotype records with ANDNM identity and lifecycle states, and with MNN admission, departure, dormancy, quarantine, and retirement semantics where MNN is enabled.
3. **Reversibility and lineage:** record parent/source configurations, versioned changes, dependencies, and rollback or retirement behavior. Do not assume copied configurations preserve behavior.
4. **Resource accounting:** attribute compute, memory, storage, communication, and execution time to components and developmental events. Otherwise apparent growth may simply reflect unmeasured resource expansion.
5. **Observer effects:** specify how the simulator measures behavior without inadvertently rewarding, selecting, or steering it.
6. **Objective leakage:** inspect initial rules, resource allocation, persistence, reproduction, and selection for implicit incentives. “No assigned intelligence objective” does not mean “no selection pressure.”
7. **Independent evaluation:** use held-out tasks and reviewers or evaluators that do not share the candidate generator's assumptions or source set.
8. **Failure semantics:** define what happens when a unit is unreachable, compromised, resource-exhausted, duplicated, or produces harmful or misleading outputs.

## 8. Recommended experimental sequence

1. Keep the discovery-engine pilot independent and compare its exploration modes against seed-focused baselines.
2. Specify a minimal developmental lifecycle for the simulator, drawing only on the ANDNM operations required by the first experiment.
3. Run the open-ended and comparison conditions with a fixed, documented communication substrate.
4. Add MNN as a separate communication condition and compare it against suitable alternatives using the MNN evaluation plan.
5. Feed only independently validated discovery outputs into a later integration trial.
6. Evaluate whether the combined system produces a measurable benefit over each subsystem alone, while tracking cost, instability, and error propagation.

This sequence isolates causal contributions. Building discovery, development, and routing simultaneously would make failures and apparent gains difficult to attribute.

## 9. Review conclusion

No fundamental contradiction was found between the four research directions. The principal risk is **scope overlap**, especially between ANDNM's developmental lifecycle and the ecosystem simulator's component-growth language.

The clean architecture is:

**Discovery proposes and validates knowledge; ANDNM-style mechanisms change the computational population and its organization; MNN provides one candidate way for those units to communicate; the ecosystem experiment studies what happens when these mechanisms interact under specified conditions.**

This is a working reconciliation, not proof that the combined architecture will produce intelligence, self-improvement, or ASI. Each layer and each interface requires separate implementation evidence and controlled evaluation.

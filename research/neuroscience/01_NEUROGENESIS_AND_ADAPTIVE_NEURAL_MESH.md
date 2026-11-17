# Neurogenesis and Adaptive Neural Mesh

**Document type:** Concept synthesis and research note  
**Status:** Proposed computational architecture; not a biological claim  
**Version:** 0.1  
**Date:** 2026-11-16  
**Origin:** Distilled from the founder's November 15, 2026 discussion.

## 1. Purpose

This document preserves the earlier concept connecting biological neurogenesis and neural plasticity to a dynamically growing digital network. The central idea is to treat HiveNet's orchestration layer as a computational neural mesh whose functional units can be created, recruited, connected, evaluated, reassigned, disconnected, or placed into dormancy.

The analogy is functional and architectural. It does not assert that creating a software process is biologically equivalent to generating a neuron.

## 2. Working terminology

### 2.1 Biological neurogenesis

Neurogenesis is the generation of new neurons from neural stem or progenitor cells. In adult humans, evidence has focused especially on the hippocampal dentate gyrus. The extent and persistence of adult human neurogenesis, and its contribution to cognition, remain active research questions.

### 2.2 Artificial neurogenesis

**Artificial neurogenesis** is a proposed computational analogy: increasing a system's available functional processing capacity by instantiating or activating additional computational units, services, model instances, or processes.

In HiveNet, a new unit need not be a newly trained model. It may be:
- A local model instance.
- A specialist model or inference service.
- A temporary process.
- A task-specific agent.
- A reusable computational service.

This form of growth occurs at the orchestration and system-composition layer. It does not necessarily modify the internal weights of any model.

### 2.3 HiveNet-Neurons

**HiveNet-Neuron** is a working name for an independently identifiable computational unit participating in the mesh.

A HiveNet-Neuron should have:
- A stable or session-scoped identity.
- Declared capabilities and constraints.
- An owner-approved participation policy.
- A record of tasks, performance, and failures.
- Explicit connection and routing permissions.
- A lifecycle state such as available, active, dormant, quarantined, or retired.

These are proposed system properties, not an existing implemented specification.

### 2.4 Adaptive Neurogenesis and Dynamic Neural Mesh (ANDNM)

**ANDNM** is the working name previously used for the combined concept of adaptive computational growth and dynamic interconnection.

The mesh is envisioned as having numerous short, purposeful connections rather than depending on a single fixed chain. New computational units may be mapped into existing networks when their capabilities and authorization fit a task.

## 3. Neural-mesh behavior

The earlier concept includes the following behaviors:

1. **Dynamic recruitment:** identify and activate an eligible unit when a capability is needed.
2. **Dynamic connection:** create a task-scoped communication path between units.
3. **Association-based routing:** route work based on the relationship between task requirements and unit capabilities, not solely on a fixed topology.
4. **Purpose preservation:** a unit may retain a dedicated specialty while also relaying or supporting other work when explicitly permitted.
5. **Evaluation:** measure the usefulness, reliability, latency, resource use, and failure rate of paths.
6. **Readjustment:** revise routing and connections in response to measured outcomes.
7. **Disconnection and dormancy:** release resources when a path or unit is no longer useful, without erasing its provenance or history.
8. **Independent development:** units may operate in different environments and acquire different histories before exchanging selected knowledge.
9. **Offline learning / “dreaming”:** conduct bounded review, consolidation, or reorganization when live task pressure is absent. This is a computational design analogy, not a claim that software dreaming is equivalent to sleep or biological memory consolidation.

## 4. Distinguishing related mechanisms

| Concept | Biological meaning | Computational analogy in this project |
|---|---|---|
| Neurogenesis | New neurons are generated | New computational units are instantiated or activated |
| Synaptogenesis | New synaptic connections form | New communication links or routes are created |
| Neuroplasticity | Neural structure/function adapts | Weights, policies, routing, or topology adapt |
| Synaptic pruning | Some connections are weakened or eliminated | Ineffective routes are retired or deprioritized |
| Neural integration | Signals are combined across neural structures | Multiple services or information sources are coordinated |
| Memory consolidation | Memory traces are stabilized/reorganized | Knowledge and task records are reviewed and persisted |

These are analogies, not identity claims. In particular, software service retirement is not biological synaptic pruning, and process creation is not neuron birth.

## 5. HiveNet mapping

The proposed mapping is:

- **HiveNet-Neurons:** identifiable local models, services, or processes.
- **Neural mesh:** the orchestration and communication topology.
- **Synapse analogue:** an authenticated, authorized, observable communication edge.
- **Plasticity analogue:** policy- or performance-driven changes to routes, weights, and connections.
- **Neurogenesis analogue:** creation or recruitment of additional computational units.
- **Dreaming analogue:** offline evaluation, consolidation, and bounded reorganization.
- **Neural history:** append-only records of unit identity, connections, tasks, evaluations, and changes.

A mesh must not become an implicit authority system. Discovery does not grant permission; capability does not grant command; connectivity does not establish consent. Resource owners retain control over participation and data disclosure.

## 6. Research questions

1. Does a dynamically reconfigurable mesh outperform a fixed topology on heterogeneous task workloads?
2. How much benefit comes from adding units versus improving routing among existing units?
3. Can performance history improve recruitment without creating unfair lock-in or hidden central authority?
4. How should a unit's specialized role be balanced against temporary multi-purpose routing?
5. Can independently developed units exchange knowledge without losing provenance or erasing their separate histories?
6. What safeguards prevent routing feedback loops, overload, oscillation, or runaway resource consumption?
7. Which functions require model-weight changes, and which can be achieved entirely through orchestration?

## 7. Initial computational evaluation

A simulation should compare at least:
- A fixed network.
- A dynamically routed network with a fixed unit pool.
- A dynamically routed network that can instantiate/recruit additional units.

Measure:
- Task success and generalization.
- Latency and throughput.
- Resource consumption.
- Route stability and churn.
- Failure recovery.
- Provenance completeness.
- Owner-policy compliance.
- Performance under unavailable or unreliable units.

The experiment should isolate the value of dynamic topology from the value of simply adding more compute.

## 8. Limitations

This framework does not claim that HiveNet currently implements ANDNM, that a software agent is a neuron, or that orchestration-level growth reproduces biological neurogenesis. It is a conceptual architecture intended for simulation and later engineering evaluation.

## 9. Preliminary references

- Disouky, A. et al. (2026). “Human hippocampal neurogenesis in adulthood, ageing and Alzheimer’s disease.” *Nature*, 652, 1264–1273. https://doi.org/10.1038/s41586-026-10169-4
- Alonso-Moreno, M. C. et al. (2025). “Human adult hippocampal neurogenesis in health and disease.” *Aging Brain*, 8, 100145. https://doi.org/10.1016/j.nbas.2025.100145

These sources inform the biological background; they do not validate the computational analogy.

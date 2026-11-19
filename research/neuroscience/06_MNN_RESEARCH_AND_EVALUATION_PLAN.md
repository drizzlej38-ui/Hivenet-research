# MNN Research and Evaluation Plan

**Document type:** Research plan and experiment specification  
**Status:** Proposed; no results yet  
**Version:** 0.1  
**Date:** 2026-11-19  
**Parent:** [MNN Concept and Architecture](04_MESH_NEURAL_NETWORKING_MNN_CONCEPT.md)

## 1. Research objective

Determine whether specialization-scoped forwarding with local awareness and extended routing can provide useful communication, incremental growth, and resilience without requiring every computational neuron to maintain a global network map.

The experiment must separate the benefit of the routing architecture from the benefit of adding more computational capacity.

## 2. Primary hypotheses

- **H1 — Local knowledge:** Nodes with bounded local peer state can deliver signals to eligible remote destinations through multi-hop forwarding.
- **H2 — Specialization filtering:** Restricting forwarding to compatible domains reduces irrelevant traffic and cross-domain exposure compared with unrestricted routing.
- **H3 — Localized admission:** A new neuron can be integrated into its domain without requiring unrelated domains to rebuild membership or routing state.
- **H4 — Resilience:** Alternate compatible routes improve delivery under node/link failure, with measurable overhead.
- **H5 — Bounded overhead:** Route discovery, caching, and forwarding can remain within defined memory, message, and latency budgets as the network grows.
- **H6 — Processing isolation:** Forwarding can be implemented without materially degrading the neuron's primary processing task.

## 3. Baseline architectures

At minimum, compare:

| ID | Architecture | Purpose |
|---|---|---|
| B0 | Fixed direct connectivity | Baseline without extended forwarding |
| B1 | Central/global route directory | Reference point for global topology knowledge |
| B2 | Local-neighbor mesh with unrestricted forwarding | Isolate value of local routing without domain constraints |
| B3 | Local-neighbor mesh with specialization-scoped forwarding | Core MNN proposal |
| B4 | MNN with domain-local admission and dynamic neuron insertion | Test incremental expansion |
| B5 | MNN with node/link failures and alternate routes | Test resilience |

B1 is a comparison baseline, not a recommended MNN dependency. The comparison should also include a conventional router-overlay baseline where computational neurons and routing nodes are separate, if feasible.

## 4. Simulation model

Create a configurable graph of computational neurons grouped into functional domains.

Each neuron has:
- Unique identity.
- One or more domain memberships.
- Primary task role.
- Relay and routing eligibility.
- Local peer table.
- Bounded route cache.
- Processing capacity and optional load.
- Availability/failure state.

Each edge represents a direct communication relationship with configurable latency, capacity, and failure probability.

Signals have:
- Origin and destination.
- Domain.
- Message identity.
- Payload size or abstract cost.
- Hop limit and expiry.
- Optional priority.

The first simulation may use abstract payloads. It does not need to train a language or mathematical model to evaluate routing behavior. A later experiment can couple the routing layer to actual model components to test processing interference.

## 5. Required scenarios

### Scenario A — Basic multi-hop forwarding

Generate compatible source/destination pairs at varying graph distances. Verify that intermediate neurons forward signals originating elsewhere without semantic processing.

### Scenario B — Domain isolation

Introduce multiple domains with overlapping and non-overlapping peer structures. Generate valid, incompatible, and unknown-domain traffic. Verify that domain policy is enforced at every forwarding hop.

### Scenario C — Dynamic neuron admission

Add neurons to one domain while traffic continues in other domains. Measure:
- Time to admission.
- Number of nodes receiving membership updates.
- Number of routes created or invalidated.
- Unrelated-domain control traffic.
- Delivery interruption, if any.

### Scenario D — Node and link failures

Disable nodes and edges during active traffic. Measure recovery, delivery, path stretch, rediscovery traffic, and behavior when no alternate path exists.

### Scenario E — Congestion and load

Vary message rates, node forwarding capacity, and link capacity. Evaluate backpressure, queue growth, fairness, and dropped messages.

### Scenario F — Scale and topology

Vary:
- Number of neurons.
- Number of domains.
- Average local degree.
- Domain size and overlap.
- Graph diameter.
- Small-world versus random versus clustered topologies.
- Signal sparsity and destination locality.

### Scenario G — Processing-function preservation

Couple a primary computational task to the forwarding workload. Compare task accuracy or quality, latency, and resource use with forwarding disabled and enabled.

## 6. Metrics

### Delivery
- Delivery success rate.
- End-to-end latency (median, p95, p99).
- Hop count and path stretch.
- Duplicate delivery rate.
- Expired or undeliverable signal rate.

### Network cost
- Forwarded messages per delivered signal.
- Route-discovery messages.
- Membership-control messages.
- Bytes or abstract communication units per delivered signal.
- Queue occupancy and memory use.
- Energy estimate, if hardware-backed measurement becomes available.

### Locality and coordination
- Maximum and average peer-table size.
- Route-cache size.
- Number of nodes updated per admission event.
- Number of unrelated domains receiving updates.
- Global coordination messages (target: none required for ordinary local admission).

### Resilience
- Delivery under node/link failures.
- Recovery time.
- Route churn.
- False route acceptance/rejection.
- Impact of partition and recovery.

### Specialization and safety
- Incompatible traffic forwarded (target: zero).
- Unknown-domain traffic forwarded (target: zero).
- Unauthorized admission accepted (target: zero).
- Provenance completeness.
- Loop and duplicate-control effectiveness.

### Processing isolation
- Primary-task accuracy or quality.
- Primary-task latency.
- Compute and memory overhead of forwarding.
- Interference under peak forwarding load.

## 7. Experimental controls

- Use identical graph topologies and traffic traces across comparable baselines.
- Hold total computational capacity constant when isolating routing effects.
- Separately test capacity growth so additional neurons are not mistaken for routing gains.
- Repeat randomized scenarios with recorded seeds.
- Report distributions and confidence intervals, not only averages.
- Predefine success thresholds before final evaluation.
- Preserve configuration, code revision, raw results, and analysis scripts.
- Report negative results and failure cases.

## 8. Initial success criteria (provisional)

The following are proposed gates, not achieved results:
1. MNN B3 delivers compatible signals correctly in multi-hop scenarios.
2. No incompatible or unknown-domain signal is forwarded in policy tests.
3. Local route state remains bounded by configured limits.
4. Admission of a neuron updates only its domain-local membership scope and affected local peers; unrelated domains receive no mandatory membership update.
5. The system detects and terminates routing loops within the configured hop/duplicate controls.
6. Failure recovery improves delivery over a no-alternate-path baseline without unbounded control traffic.
7. Forwarding overhead and primary-task degradation remain within thresholds selected before the experiment.

Threshold values should be set after an initial workload characterization, not invented before the cost model is understood.

## 9. Ablation studies

Disable one feature at a time:
- Domain restrictions.
- Local route caching.
- Duplicate detection.
- Hop limits.
- Local admission registry.
- Alternate route selection.
- Load-aware route choice.

This identifies which mechanisms provide measurable value and which add complexity without benefit.

## 10. Implementation sequence

1. Build a deterministic graph simulator.
2. Implement B0, B1, B2, and B3.
3. Validate signal identity, domain enforcement, and loop controls.
4. Add dynamic admission (B4).
5. Add failure and congestion models (B5).
6. Run scale and topology sweeps.
7. Add a primary processing workload.
8. Publish reproducible results and limitations.
9. Seek independent review before claiming architectural advantage.

## 11. Decision gates

- **Gate 1 — Correctness:** routing, provenance, domain enforcement, and loop controls pass deterministic tests.
- **Gate 2 — Locality:** admission and route maintenance remain local under measured workloads.
- **Gate 3 — Performance:** MNN offers a measurable benefit over relevant baselines in at least one defined use case without unacceptable trade-offs.
- **Gate 4 — Robustness:** failure and adversarial tests do not reveal unresolved critical weaknesses.
- **Gate 5 — Hardware relevance:** only after simulation, assess whether a hardware or neuromorphic implementation is justified.

## 12. Reproducibility and provenance

Every run should record:
- Experiment identifier and timestamp.
- Simulator version and source revision.
- Topology generator and random seed.
- Domain and compatibility policy.
- Routing configuration.
- Workload and traffic pattern.
- Hardware/runtime environment, if relevant.
- Raw output and analysis revision.
- Known limitations and deviations from the plan.

ENDCAP may later serve as an append-only record for experiment provenance. That integration is a future option, not a dependency for the initial simulator.

## 13. Status

No MNN simulator, benchmark, or performance result is claimed by this document. The next deliverable is a small reproducible simulator implementing the baseline comparison and core invariants.

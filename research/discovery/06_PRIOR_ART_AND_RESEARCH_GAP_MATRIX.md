# Prior Art and Research-Gap Matrix

**Status:** Preliminary literature and architecture comparison; not a novelty determination  
**Version:** 0.1  
**Date:** 2026-11-26  
**Branch:** `research/seeded-discovery-engine`

## 1. Purpose and scope

This document compares the current Discovery Systems and Open-Ended Development proposal with selected established work in digital evolution, open-ended evolution, environment generation, self-modifying agents, and the project's own adjacent architectures.

The goal is not to claim that the broad idea of an evolving computational ecosystem is new. That field is established. The goal is to identify overlap, avoid duplicating known results, and isolate a researchable contribution that can be tested with a small, fault-tolerant, local-first implementation and optional remote workers.

This is a preliminary desk review, not a systematic literature review, exhaustive patent search, or proof of priority. The entries below are selected exemplars, not the complete state of the art.

## 2. Comparison matrix

| Work | Main object and mechanism | Established overlap with this project | What it does not establish for this project | Implication |
|---|---|---|---|---|
| **Tierra** (Thomas S. Ray, 1991 onward) | Digital organisms execute and replicate in a shared virtual computer; mutation, competition, parasitism, and ecological dynamics can occur. | Digital populations, resource competition, self-replication, ecological interactions, and open-ended artificial-life questions. | It does not, by itself, establish our proposed discovery-validation-development pipeline, ANDNM lifecycle, MNN routing, or local-first tablet/cloud implementation. | Treat digital ecology and replication as established prior art. Do not present computational organisms or emergent ecological interaction as novel. |
| **Avida** (Lenski et al., 2003 and subsequent work) | Digital organisms self-replicate, mutate, compete, and evolve; experiments examine the origin of complex functions under selectable environmental conditions. | Controlled digital evolution, heritable variation, selection, complex behavior, reproducible trials, and explicit experimental comparisons. | It does not establish the complete multi-layer HiveNet architecture or the proposed integration of evidence-provenance discovery with dynamic mesh development. | Use Avida as a baseline/reference for evolutionary operators, experimental controls, and measurable phenotypic change. |
| **Open-ended evolution research** (including Packard et al., 2019; Taylor et al., 2019; related OEE literature) | Studies definitions, mechanisms, and barriers to sustained novelty, diversity, complexity, and new forms of individuality. | The central question of whether systems can sustain open-ended novelty; known issues include diversity collapse, complexity saturation, and failure to create new levels of organization. | It does not prescribe one universal architecture or prove that any particular integrated architecture will achieve open-ended evolution. | Our claims must be operationalized against established OEE definitions and known failure modes. “Runs for a long time” is not sufficient. |
| **POET / Enhanced POET** (Wang et al., 2019/2020) | Co-generates learning environments and solutions; allows solutions to transfer between environments, creating stepping stones through a changing challenge space. | Open-ended exploration, environmental change, diversity of paths, reuse of prior solutions, and coupled environment/agent development. | It is oriented around generating and solving learning challenges, not a wholly objective-free ecosystem. It does not establish our discovery evidence chain or mesh architecture. | Compare against POET where environments and tasks evolve. Explicitly distinguish objective-driven open-ended search from no-assigned-intelligence-objective conditions. |
| **Darwin Gödel Machine (DGM)** (Zhang et al., 2025) | Iteratively modifies coding-agent code, empirically evaluates changes on benchmarks, and maintains an archive of candidate agents. | Self-modification, branching lineages, empirical evaluation, archival selection, and parallel exploration of variants. | Its benchmark-driven coding improvements are not equivalent to open-ended ecosystem evolution; it does not demonstrate autonomous evolution of the underlying selection/variation rules in the broader ecological sense. | Use it as a comparison for bounded self-modification and empirical validation. Do not equate benchmark improvement with meta-evolution. |
| **Genesis** (Sharma, 2026; GECCO Companion 2026) | Empirical open-ended-evolution platform studying constraint-driven selection without scalar fitness, niche construction, developmental encoding, and proposed meta-evolution of environmental/physical rules. | Direct overlap with fitness-free evolutionary activity, environmental constraints, complexity plateaus, niche construction, speciation, and the question of evolving the rules of the world. | The published/preprint material located in this review does not establish our proposed Discovery Engine + ANDNM + MNN integration, nor a local-first, fault-tolerant, tablet/cloud implementation. | Highest-priority direct comparator for the open-ended evolution and Level C research. Reproduce or carefully adapt relevant controls before claiming a gap in fitness-free evolution or meta-evolution. |
| **ANDNM** (HiveNet internal research) | Proposed lifecycle for creating/recruiting, activating, connecting, reconfiguring, reassigning, dormancy, and retirement of computational units. | Dynamic computational populations and structural/developmental change. | It is a project proposal, not external validation or proof of a novel developmental mechanism. | Treat as a candidate implementation layer. Compare its lifecycle semantics with existing dynamic networks, modular learning, neuroevolution, and multi-agent systems before asserting novelty. |
| **MNN** (HiveNet internal research) | Proposed specialization-aware, bounded local peer routing and domain admission for computational units. | Distributed communication, local topology knowledge, multi-hop forwarding, admission and lifecycle handling. | It is a project proposal; its novelty and performance are unverified. | Evaluate as an optional communication condition. Compare against established peer-to-peer, message-passing, service-mesh, and multi-agent communication systems. |
| **Seeded Discovery Engine** (HiveNet internal research) | Proposed seeded but open-domain exploration with direct, associative, contrarian, and anomaly-led branches; provenance and independent validation; capability-gap proposals. | Automated research, retrieval, hypothesis generation, cross-domain search, and evaluation are established areas. | No implementation or evidence yet shows improved independently validated discovery over existing retrieval/research baselines. | The candidate contribution is the evidence-governed handoff from discovery to development, with traceable provenance and safeguards against self-confirming validation. Test it against simple retrieval and agentic-research baselines. |
| **Hybrid local-cloud execution** (HiveNet proposed deployment) | Tablet-local coordinator and authoritative record, with optional remote workers for resumable independent jobs. | Edge computing, distributed job execution, checkpointing, fault tolerance, and cloud burst capacity are established engineering techniques. | No novelty is claimed for these techniques individually. The actual feasibility and cost of the proposed Android implementation remain untested. | Potential contribution is an accessible, reproducible experimental deployment under severe resource constraints, not a new distributed-computing principle. |

## 3. What appears to be the most defensible research gap

The strongest candidate gap is **not** “a computational ecosystem that evolves without a fitness function,” “digital organisms,” “self-modifying agents,” or “open-ended discovery.” Those are all established areas, and Genesis is a particularly direct comparator for fitness-free evolutionary dynamics and meta-evolution of environmental rules.

The more defensible candidate is an experimentally evaluated **integration and governance architecture** with the following properties:

1. **Evidence-governed discovery:** candidate findings retain source-level provenance, contrary evidence, uncertainty, and independent validation status.
2. **Explicit capability-gap handoff:** a validated finding may propose a capability gap, but discovery cannot directly authorize creation or deployment.
3. **Developmental lifecycle:** computational units and configurations have explicit identity, lineage, lifecycle state, resource accounting, and reversible transitions.
4. **Optional bounded local communication:** specialization-aware local routing can be introduced as a controlled experimental condition rather than assumed as a universal mechanism.
5. **Open-ended ecosystem evaluation:** interactions among discovery, development, and communication are measured without treating complexity, persistence, or intelligence as presumed objectives.
6. **Fault-tolerant local-first execution:** the experiment remains operable on a modest local device, with optional interruptible cloud workers, recoverable checkpoints, reproducible runs, and locally authoritative records.
7. **Independent evaluation across the loop:** generation, validation, implementation, and held-out testing are separated sufficiently to expose circular confirmation and regressions.

This is a **candidate integration gap**, not a verified claim that no prior system has combined these elements. A deeper review must examine adjacent work in multi-agent systems, neuroevolution, automated scientific discovery, developmental systems, distributed systems, and provenance-aware AI workflows.

## 4. Falsifiable contribution claims

The project should avoid a single broad novelty claim. Break it into testable claims:

- **C1 — Provenance integrity:** the discovery pipeline can preserve claim-level provenance and contrary evidence through candidate generation, validation, and development handoff with measurable completeness.
- **C2 — Handoff discipline:** separating discovery proposals from developmental authorization reduces unvalidated capability creation compared with an unconstrained integrated baseline.
- **C3 — Developmental observability:** identity, lineage, lifecycle, resource accounting, and rollback records make changes more reproducible and diagnosable than a baseline without those records.
- **C4 — Communication effect:** enabling MNN-style local specialization routing changes measurable communication cost, reachability, fault recovery, or task performance relative to a matched simpler communication baseline.
- **C5 — Integration value:** the combined architecture produces a measurable benefit over its component systems alone on predefined tasks, without a disproportionate increase in false discoveries, resource use, or instability.
- **C6 — Deployment resilience:** a local-first implementation can stop, resume, recover from process interruption, and reproduce a run; optional remote workers improve throughput without becoming required for correctness or authoritative state.

A claim passes only within the tested workload, configuration, and resource envelope. Passing a narrow test does not establish generality.

## 5. Recommended experimental comparisons

| Experiment | Baseline | Treatment | Primary measures |
|---|---|---|---|
| Discovery provenance | Conventional retrieval/candidate list | Provenance-rich discovery and validation pipeline | Evidence completeness, independent validation yield, false-positive rate, reviewer time |
| Development handoff | Direct automatic component creation from candidate output | Validated capability-gap proposal plus explicit authorization gate | Invalid component creation, traceability, task success, review burden |
| Lifecycle observability | Components without explicit lineage/resource records | ANDNM-style identity, lineage, lifecycle and resource ledger | Replay success, diagnosis time, rollback correctness, overhead |
| Communication | Simple broadcast or fixed routing | MNN-style local specialization routing | Messages/bytes, latency, reachability, failure recovery, task success |
| Ecosystem integration | Each subsystem tested separately | Discovery + development + optional communication | Incremental benefit, regressions, resource cost, error propagation |
| Execution resilience | Single uninterrupted local run | Checkpointed local run with injected interruptions and optional remote workers | Recovery point, lost work, reproducibility, overhead, throughput |

Use matched workloads and resource budgets. Run multiple random seeds. Preserve failures and null results. Do not let the integrated system evaluate its own success without independent checks.

## 6. Implementation order under zero-capital constraints

1. **Freeze the research questions and comparison criteria.** Do not begin with a large agent framework.
2. **Build a deterministic, small local simulator.** Start with simple computational units and explicit variation, inheritance, persistence, and resource accounting.
3. **Implement the event ledger and checkpoint/recovery loop.** Treat interruption handling as a correctness requirement.
4. **Establish local baselines.** Measure runtime, memory, storage, energy/battery impact where measurable, and reproducibility on the target tablet.
5. **Add discovery provenance as a separate module.** Begin with a bounded corpus and manually inspect candidate records.
6. **Add developmental handoff and lifecycle controls.** Discovery may propose; the simulator policy decides what can occur internally.
7. **Add MNN only as a controlled communication treatment.** Keep the first baseline simple.
8. **Add optional cloud batch execution.** Remote workers receive bounded, versioned jobs and return results; the tablet verifies and records them.
9. **Run ablations and comparative trials.** Attribute any measured gain to the mechanism that produced it.
10. **Publish a gap statement only after the comparisons.** Narrow or revise the claim if prior work already covers it.

No paid compute, hosted always-on service, or external deployment is required for the first stages.

## 7. Important corrections and cautions

- “No fitness function” does not mean “no selection pressure.” Constraints, resource allocation, reproduction, and persistence can produce implicit selection.
- “Open-ended” is not synonymous with indefinite runtime, increasing complexity, intelligence, or progress. Definitions and metrics must be declared.
- A self-modifying agent is not automatically undergoing evolution; inheritance, differential propagation, and feedback must be demonstrated.
- A changing topology is not necessarily a new developmental capability.
- A local-first deployment is an engineering contribution only if its resilience, reproducibility, and resource constraints are measured.
- Similarity between architectures is not proof of duplication; difference in terminology is not proof of novelty.
- A literature search cannot establish universal absence. Use “not identified in the reviewed sources” rather than “does not exist.”

## 8. Priority reading and source register

The following sources support the comparisons above. They are starting points, not an exhaustive bibliography.

1. **Lenski, R. E., Ofria, C., Pennock, R. T., & Adami, C. (2003).** “The evolutionary origin of complex features.” *Nature* 423, 139–144. https://doi.org/10.1038/nature01568  
   Digital organisms in Avida evolve complex logic functions through mutation and selection.

2. **Ray, T. S. (1991).** “An approach to the synthesis of life.” In *Artificial Life II*.  
   Foundational Tierra work on digital organisms and artificial ecology. Author's publication list: https://www.tomray.me/pubs/

3. **Packard, N. et al. (2019).** “An Overview of Open-Ended Evolution.” *Artificial Life* 25(2), 93–103. https://doi.org/10.1162/artl_a_00291  
   Overview of OEE research and its central questions.

4. **Taylor, T. et al. (2019).** “On the Potential for Open-Endedness in Neural Networks.” *Artificial Life* 25(2), 145–167. https://doi.org/10.1162/artl_a_00286  
   Reviews barriers to open-endedness and relationships between evolutionary and machine-learning approaches.

5. **Wang, R., Lehman, J., Clune, J., & Stanley, K. O. (2019).** “Paired Open-Ended Trailblazer (POET).” https://arxiv.org/abs/1901.01753  
   Co-evolution of learning environments and solutions.

6. **Wang, R. et al. (2020).** “Enhanced POET.” *Proceedings of ICML*, PMLR 119, 9940–9951. https://proceedings.mlr.press/v119/wang20l  
   Further work on open-ended generation of challenges and solutions.

7. **Zhang, J. et al. (2025).** “Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents.” https://arxiv.org/abs/2505.22954  
   Self-modifying coding agents, empirical benchmark evaluation, and archive-based branching.

8. **Sharma, A. (2026).** “Genesis: An Empirical Platform for Studying Open-Ended Evolution Without Fitness Functions.” GECCO Companion 2026. https://doi.org/10.1145/3795101.3814645; preprint: https://arxiv.org/abs/2607.21631  
   Direct comparator for fitness-free evolutionary activity, constraint-driven selection, and proposed meta-evolution of environmental rules.

9. **Sharma, A. (2026).** “Evolving Self-Organising Agents Without Fitness: Three Falsifiable Experiments from Constraint-Driven Selection to Developmental Encoding.” https://arxiv.org/abs/2607.21630  
   Related Genesis experimental report; distinguish it from the companion paper above when citing specific claims.

10. **Pattee, H. H., & Sayama, H. (2019).** “Evolved Open-Endedness, Not Open-Ended Evolution.” *Artificial Life* 25(1), 4–8. https://doi.org/10.1162/artl_a_00276  
    Argues that open-endedness may itself emerge through evolution rather than be assumed as a prerequisite.

## 9. Current conclusion

The broad field is established. The closest prior work already covers digital organisms, open-ended evolution, fitness-free evolutionary dynamics, co-evolving environments and solutions, and self-modifying agents.

The most defensible direction for HiveNet-research is therefore to test whether a **provenance-governed discovery process, explicit developmental lifecycle, optional specialization-aware local communication, and fault-tolerant local-first execution** can be integrated into a reproducible experimental system with measurable benefits over simpler baselines.

That integration may or may not be novel. The next task is not to assert that it is; it is to build the smallest experiment capable of showing exactly what it adds.


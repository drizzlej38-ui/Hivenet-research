# Endogenous Evolutionary Dynamics

**Status:** Research hypothesis and proposed experimental specification  
**Version:** 0.1  
**Date:** 2026-11-26

## 1. Purpose

Define a testable research track for determining whether a bounded computational ecosystem can sustain evolutionary change through processes operating within the ecosystem, rather than merely executing a fixed sequence of externally prescribed adaptations.

This document extends the Discovery Systems and Open-Ended Development track. It does not claim that self-evolution, general intelligence, or superintelligence has been demonstrated.

**Central hypothesis:** Under specified conditions, a computational ecosystem containing mechanisms for variation, inheritance, differential persistence, and environmental feedback may develop and sustain changes in its own population, organization, and potentially the processes governing those changes, without an externally assigned intelligence objective or developmental destination.

The hypothesis has multiple strengths. Evidence for ordinary evolutionary dynamics would not, by itself, establish that the ecosystem can modify its own evolutionary rules. Those claims must be tested separately.

## 2. What counts as evolution?

Change alone is insufficient. For this project, an evolutionary process requires operational evidence of all four elements:

1. **Variation:** distinguishable heritable differences arise among units or configurations.
2. **Inheritance:** some of those differences are transmitted to descendants or successor configurations.
3. **Differential persistence or propagation:** variants have different probabilities of surviving, being copied, or contributing to later system states.
4. **Feedback:** those differences affect outcomes under environmental conditions, and the outcomes influence subsequent persistence or propagation.

These criteria are project definitions for experimental use. They do not assert biological equivalence.

A system that changes its topology under a hard-coded rule may be adaptive, but it is not thereby shown to have an endogenous evolutionary process. A system that generates variants but does not transmit their distinguishing properties lacks demonstrated inheritance. A system that copies every variant equally may exhibit variation and inheritance without meaningful differential selection.

## 3. Distinguish three levels of claim

### Level A — Evolution within fixed rules

The ecosystem produces variants, transmits configurations, and exhibits differential persistence under environmental feedback. The variation, inheritance, and selection operators remain externally specified and fixed for the duration of the experiment.

This is the minimum evolutionary-dynamics claim.

### Level B — Endogenous developmental organization

The ecosystem changes its population, component roles, relationships, or configurations through internal processes. Those changes may alter which variants can arise or persist, while the outer evolutionary operators remain fixed.

This is a stronger claim about endogenous organization, but not yet meta-evolution.

### Level C — Evolution of evolutionary processes (meta-evolution)

The ecosystem produces and inherits changes to one or more mechanisms that govern variation, inheritance, selection, or environmental response. Those changes themselves undergo evaluation and differential persistence.

This is the strongest claim in this research track. It requires evidence that the rules or operators themselves change through the defined internal process—not merely that a developer changes simulator code between runs.

Do not collapse these levels into one result. A Level A result does not establish Level B or Level C.

## 4. Proposed mechanisms and records

### 4.1 Variation

Candidate variation mechanisms include:

- Parameter or configuration changes.
- Recombination of compatible configurations.
- Structural changes to component connections or roles.
- Creation of a new computational unit from an existing template.
- Changes to a unit's internal procedure or bounded model configuration.
- Changes to developmental or communication strategies.

Every variation event should record its parent or source, the exact change, the mechanism that produced it, the resources consumed, and whether the result is reversible.

Random mutation is one possible mechanism, not a requirement. Any mechanism used must be documented and comparable across experimental conditions.

### 4.2 Inheritance

Inheritance must be explicit and inspectable. Record:

- Parent/source identity and version.
- Descendant/successor identity and version.
- Which parameters, procedures, structures, data, or learned states were transmitted.
- Which properties were reset, omitted, or independently initialized.
- Whether the inherited configuration remains behaviorally equivalent.
- Lineage links and integrity hashes where practical.

Copying a model or configuration does not prove that its behavior, knowledge, or capabilities were successfully inherited. Test the transmitted properties.

### 4.3 Differential persistence and propagation

Potential sources of differential persistence include:

- Resource availability and resource consumption.
- Task outcomes on declared workloads.
- Robustness under perturbation or component failure.
- Compatibility with other units and communication protocols.
- Reliability, reproducibility, and error rates.
- Ability to continue operating under changing conditions.

Do not assume that persistence means usefulness. A harmful, deceptive, wasteful, or highly resource-consuming variant may persist if the environment accidentally favors it. Record trade-offs and adverse effects rather than compressing them into one opaque fitness score.

### 4.4 Environmental feedback

The experimental environment may vary:

- Task distributions and task difficulty.
- Compute, memory, storage, and communication budgets.
- Availability and reliability of other components.
- Network topology and communication latency.
- Perturbations, component loss, and recovery opportunities.
- Resource scarcity and changes in demand.

The environment must not silently reward intelligence, complexity, or self-replication unless that is the declared experimental condition. Record all resource and task rules so implicit selection pressures can be inspected.

## 5. The question of being "forced" to evolve

Constraints can create pressure to change, but they cannot guarantee useful evolution.

If an ecosystem's environment changes and existing configurations no longer meet its operational requirements, the population may reorganize, adapt, stagnate, exploit a loophole, fragment, or collapse. Evolutionary pressure does not guarantee successful adaptation, progress, intelligence, or survival.

For experimental purposes, replace the informal claim that the system is "forced to evolve" with measurable statements:

- Which environmental constraint changed?
- Which existing configurations became less viable, and by what measure?
- What internal variation or developmental response occurred?
- Were the resulting differences inherited?
- Did their persistence or propagation differ?
- Did the response improve performance on held-out conditions, or merely exploit the measured environment?
- Did the ecosystem recover, remain stable, or fail?

The environment can make adaptation consequential. It cannot guarantee that a viable adaptation will be found.

## 6. Experimental design

Use the same initial populations, workloads, resource budgets, and evaluation procedures across comparable conditions. Run multiple independent seeds and preserve complete event histories.

| Condition | Evolutionary operators | Purpose |
|---|---|---|
| Static baseline | No inherited variation | Measure behavior without evolutionary change |
| Fixed-rule evolution | Variation, inheritance, and selection are externally fixed | Test Level A |
| Endogenous development | Fixed outer operators; internal population and topology can reorganize | Test Level B |
| Meta-evolution condition | Bounded, inheritable changes to selected evolutionary operators are permitted | Test Level C |
| Directed comparison | Explicit task objective and fixed evaluation pressure | Estimate effects of a prescribed objective |
| Open-ended comparison | No assigned intelligence objective; environmental constraints remain documented | Test development without a prescribed destination |

The meta-evolution condition should be introduced only after the fixed-rule condition is understood and reproducible. Begin with one narrowly bounded operator that can be modified, versioned, tested, and rolled back. Do not initially permit unrestricted rewriting of the simulator or its containment controls.

### Required ablations

- Variation disabled.
- Inheritance disabled or randomized.
- Differential persistence disabled.
- Environmental feedback held constant.
- Evolutionary operators fixed.
- Meta-evolution disabled.
- Resource constraints equalized or varied one at a time.

These ablations help determine which mechanism is responsible for an observed result.

## 7. Measurements

### Evolutionary evidence
- Number and diversity of heritable variants.
- Verified transmission of distinguishing properties.
- Lineage depth and branching.
- Differential persistence and propagation.
- Rate of change in population composition.
- Repeatability across independent runs.

### Developmental and ecological outcomes
- Changes in topology, roles, specialization, and coordination.
- Held-out task performance and generalization.
- Resource use per unit and per successful task.
- Robustness, recovery, and failure rates.
- Concentration of resources or influence.
- Harmful behavior, error propagation, instability, and collapse.

### Meta-evolution evidence
- Which evolutionary operator changed.
- Whether the change was inherited.
- Whether the altered operator generated distinguishable later variants.
- Whether the altered process persisted differentially.
- Whether independent replication confirms the effect.
- Whether the result can be explained by a fixed rule or simulator artifact.

Novelty, complexity, persistence, self-description, or a system's own claim of improvement are not sufficient evidence of evolutionary progress.

## 8. Null hypotheses and alternative explanations

At minimum, test these alternatives:

1. **Fixed-rule explanation:** apparent evolution is fully explained by the simulator's predefined transition rules.
2. **Selection artifact:** the measured environment rewards a narrow proxy, such as speed, resource capture, or task-specific optimization.
3. **Resource-expansion explanation:** apparent capability growth is caused by increased compute, memory, or execution time rather than improved organization.
4. **Inheritance failure:** descendants do not reliably retain the properties attributed to their lineage.
5. **Observer effect:** instrumentation or evaluation changes the behavior being measured.
6. **Run-specific accident:** the result does not replicate across initial conditions or random seeds.
7. **Objective leakage:** an implicit target is encoded in resource allocation, survival rules, or evaluation criteria.
8. **Simulator bug or exploit:** a variant exploits implementation details rather than demonstrating the intended mechanism.

A result that fails these tests should be reported as inconclusive or negative, not reframed as emergence.

## 9. Authority, containment, and reversibility

Internal developmental autonomy is not operational authority.

For the initial experiments:

- Run in a local, isolated simulator with no external network access.
- Use synthetic or explicitly approved data.
- Do not expose credentials, personal data, financial resources, or external actuators.
- Enforce hard compute, memory, storage, process, and time limits outside the ecosystem.
- Keep experiment rules, logs, and lineage records under external version control.
- Require an external controller to approve changes to containment, permissions, and access boundaries.
- Provide pause, snapshot, rollback, quarantine, and shutdown mechanisms.
- Treat replication and propagation as bounded simulator operations, not permission for unrestricted deployment.

A component may propose a change to its own developmental process. It must not be able to authorize expansion of its external permissions or remove the outer controls.

## 10. Proposed implementation sequence

1. **Protocol:** finalize the unit, phenotype, lineage, variation-event, and environment records.
2. **Minimal fixed-rule simulator:** implement a small population with explicit variation, inheritance, persistence, and resource accounting.
3. **Ablation tests:** show that each required evolutionary element has an observable effect.
4. **Replication:** repeat trials across multiple seeds and document null or failed outcomes.
5. **Endogenous development:** permit bounded changes to population structure and component roles.
6. **Meta-evolution pilot:** allow one narrowly scoped evolutionary operator to vary and be inherited, under fixed outer containment.
7. **Independent review:** compare logs, code, hypotheses, and results against alternative explanations before making any stronger claim.

The first prototype should be deliberately small. It should test the integrity of the evolutionary loop, not attempt to produce a powerful agent.

## 11. Go/no-go criteria

Proceed from Level A to Level B, and from Level B to Level C, only when:

- Variation and inheritance are directly demonstrated and recorded.
- Differential persistence is attributable to documented environmental feedback.
- Results replicate across independent runs.
- Resource use and selection pressures are measurable.
- Held-out evaluation rules out simple proxy exploitation to a reasonable degree.
- Containment remains independent of the ecosystem's own control.
- Independent reviewers can reconstruct the claimed result from the records.

Failure to meet a gate means revise, pause, or stop. It does not justify weakening the definition of evolution after seeing the results.

## 12. Research conclusion

The architecture assembled across Discovery, ANDNM-style development, MNN communication, and the ecosystem simulation gives us a coherent basis for building experiments about endogenous evolutionary dynamics.

What is currently established is a research architecture and a set of proposed mechanisms. Whether those mechanisms produce sustained evolutionary behavior, endogenous developmental organization, or meta-evolution remains untested.

The next defensible claim must come from a minimal, reproducible experiment—not from the ambition of the architecture.

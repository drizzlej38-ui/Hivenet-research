# Discovery and Ecosystem Evaluation Plan

**Status:** Proposed; pending implementation  
**Version:** 0.1  
**Date:** 2026-11-26

## 1. Purpose

Evaluate the seeded discovery engine and open-ended ecosystem separately before testing their integration. This prevents improvements in one subsystem from being incorrectly attributed to the other.

## 2. Research questions

### Discovery engine
- Does exploration beyond the seed identify additional independently validated findings?
- Does cross-domain association improve useful discovery or mainly increase false positives?
- Does contrarian exploration expose weak assumptions and alternatives?
- Is provenance preserved end to end?
- Do validated findings reveal capability gaps?

### Ecosystem
- What organization appears without an assigned intelligence objective?
- Are patterns repeatable across initial conditions?
- Do observed capabilities generalize to held-out tasks?
- Does development create useful capability or merely complexity and resource use?
- What conditions lead to fragmentation, instability, or collapse?

### Combined system
- Does feeding independently validated findings into the ecosystem improve measurable performance?
- Does the combination outperform each subsystem separately?
- Can it prevent a self-confirming loop in which an unvalidated claim is used to build a capability that then appears to confirm it?

## 3. Baselines and ablations

| Condition | Question |
|---|---|
| Conventional seed-focused search | Baseline retrieval and research performance |
| Direct exploration | Value of structured exploration |
| Direct + associative exploration | Added value and error cost of cross-domain branching |
| Direct + associative + contrarian/anomaly-led | Value of active disconfirmation |
| Fixed ecosystem | Baseline without developmental reconfiguration |
| Dynamic topology, fixed component pool | Value of structural reorganization |
| Dynamic topology and component creation | Added value and cost of developmental growth |
| Directed ecosystem | Effect of an explicit objective |
| Open-ended ecosystem | Behavior without an assigned intelligence objective |
| Environment-responsive ecosystem | Effect of changing conditions without a prescribed destination |
| Discovery-engine-fed ecosystem | Incremental effect of validated discovery inputs |

## 4. Measures

### Discovery quality
- Independently validated candidate yield.
- False-positive and rejection rates.
- Candidate novelty relative to the reference corpus.
- Source diversity and source quality.
- Provenance completeness.
- Reproducibility.
- Time and compute cost.
- Useful findings missed by each baseline.

### Ecosystem development
- Structural and behavioral diversity.
- Persistence and turnover of configurations.
- Specialization and role stability.
- Communication and coordination patterns.
- Resource efficiency and concentration.
- Robustness under perturbation.
- Recovery after failure.
- Held-out task performance.
- Frequency and severity of harmful or destabilizing behavior.

### Combined-system value
- Improvement over each subsystem alone.
- Cost per independently validated capability improvement.
- Rate of propagation of erroneous or weak findings.
- Regression rate after integration.
- Reproducibility across runs.

Do not use a single aggregate score as the sole measure. Publish component measures and trade-offs.

## 5. Experimental discipline

- Predefine hypotheses, metrics, and stopping conditions before examining outcomes.
- Use multiple random seeds and independent trials.
- Preserve negative, null, and failed results.
- Separate training/development cases from held-out evaluation.
- Use blinded or independent review where practical.
- Version data, code, prompts, simulator rules, and measurement methods.
- Report uncertainty and sensitivity to initial conditions.
- Distinguish correlation, causal evidence, analogy, and speculation.

## 6. Staged implementation

**Stage 0 — Protocol review:** Specify terminology, hypotheses, simulator rules, containment, and data-record format.

**Stage 1 — Discovery pilot:** Use a bounded corpus and one seed. Compare exploration modes and manually inspect candidate records.

**Stage 2 — Validation pilot:** Add independent review, replication, counterexample search, and provenance checks.

**Stage 3 — Minimal ecosystem simulator:** Implement only the component and interaction mechanisms required for the first controlled comparison. Do not build a large agent platform prematurely.

**Stage 4 — Comparative trials:** Run open-ended, directed, and environment-responsive conditions across multiple seeds.

**Stage 5 — Integration experiment:** Feed only validated discoveries into the ecosystem and compare with ecosystem-only and discovery-only baselines.

**Stage 6 — Review and revision:** Publish findings, limitations, negative results, and proposed changes before expanding scope.

## 7. Go/no-go gates

Proceed to the next stage only when:
- The prior stage is reproducible enough to interpret.
- Resource and containment limits are enforced.
- Candidate claims have traceable provenance.
- Evaluation does not depend solely on the system's own self-assessment.
- No unresolved critical failure invalidates the result.

A failed gate means pause, revise, or stop. It does not justify silently weakening the standard.

## 8. Evidence and reporting

For each result, label it as established finding, interpretation, project-defined concept, hypothesis, speculation, or negative result. Report methods, versions, data limitations, uncertainty, and alternative explanations.

Do not claim general intelligence, consciousness, or ASI from a successful narrow task or emergent organizational pattern. Such claims require separately specified criteria and independent evidence.

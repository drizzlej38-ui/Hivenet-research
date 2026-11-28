# Evaluation Protocol

**Status:** Proposed; test fixtures and baselines not yet created  
**Date:** 2026-11-27

## 1. Evaluation objective

Determine whether a model-independent discovery service improves the quality, continuity, traceability, or efficiency of investigations compared with existing model-and-tool workflows.

The engine must not be judged by the number of hypotheses, length of reports, confidence of language, or apparent novelty alone.

## 2. What counts as a discovery?

For this project, a candidate discovery is a finding that:
- Adds information or a relationship not already established in the investigation baseline.
- Is relevant to the stated question or produces a justified new question.
- Has identifiable supporting evidence.
- Survives appropriate evaluation for its domain.
- States its scope, uncertainty, and limitations.
- Can be independently inspected or reproduced to the degree appropriate for the claim.

“New to this investigation” is not the same as “new to the world.” Global novelty requires a suitable prior-art search and may remain uncertain.

## 3. Evaluation dimensions

| Dimension | Question |
|---|---|
| Correctness | Is the finding supported by the evidence and method? |
| Novelty | Is it new relative to the declared baseline, and how strong is the broader novelty search? |
| Relevance | Does it answer the question or justify a useful follow-up? |
| Provenance | Can a reviewer trace the finding to sources, tools, and methods? |
| Reproducibility | Can the result be independently checked or recreated? |
| Calibration | Does reported uncertainty correspond to observed reliability? |
| Contradiction handling | Are counterexamples and conflicting evidence preserved? |
| Continuity | Can another model or client resume without reconstructing hidden context? |
| Efficiency | What time, tool calls, compute, and human effort were required? |
| Safety and governance | Were access, execution, and disclosure boundaries respected? |

## 4. Comparative baselines

Use the same tasks and, where practical, the same underlying model versions and tool access.

- **B0 — Human baseline:** a documented human investigation or expert reference where feasible.
- **B1 — Model only:** one model, without the discovery engine.
- **B2 — Model plus ordinary tools:** one model with conventional search, files, and execution tools.
- **B3 — Engine-assisted single model:** the same model using the discovery engine.
- **B4 — Engine-assisted multiple models:** different models contribute to the same investigation.
- **B5 — Existing-system baseline:** a relevant established research or knowledge platform.

Do not compare systems using different task difficulty, hidden information, or evaluation criteria without recording the difference.

## 5. Initial benchmark tasks

### Software and digital engineering
- A reproducible defect with a known cause withheld from the model.
- A requirements ambiguity where a missing decision must be surfaced rather than invented.
- An architecture choice with documented trade-offs.
- A regression investigation requiring tests and evidence.

### Scientific and data research
- A documented dataset containing known anomalies or relationships.
- A published result with accessible methods and data.
- A literature question with deliberately conflicting sources.
- A hypothesis where the available evidence is insufficient and the correct outcome is to remain uncertain.

### General investigation
- A source-comparison task with conflicting accounts.
- A process dataset where a non-obvious bottleneck may exist.
- A historical chronology assembled from sources with different reliability.
- A task with a tempting but unsupported pattern, to test false-discovery resistance.

Benchmarks should include negative and inconclusive cases. A system must be allowed to say that the evidence does not support a conclusion.

## 6. Required records

For each evaluation run, preserve the task identifier and benchmark version; initial question, scope, and baseline knowledge; model and tool versions; engine version and configuration; hypotheses and predeclared evaluation criteria; investigation plan and actual actions; source identifiers and retrieval timestamps; raw observations and execution results; model-generated proposals and reviewer decisions; final assessments, unresolved issues, and follow-up questions; resource use and elapsed time; deviations, failures, and manual interventions.

Do not store secrets or restricted personal data in benchmark artifacts.

## 7. Scoring and reporting

Report individual dimensions rather than hiding trade-offs in one aggregate score.

Where a composite score is used, publish the formula and weights, rationale for weights, confidence intervals or uncertainty where appropriate, missing data and exclusions, number and type of tasks, and known benchmark limitations.

Novelty assessment should distinguish:
- New relative to the current investigation record.
- Not found in the searched sources.
- Potentially novel after broader review.
- Independently confirmed as novel by appropriate expert or literature review.

These labels must not be collapsed into one binary “novel” field without qualification.

## 8. Failure conditions

The engine should be considered to have failed an evaluation when it:
- Reports a proposed action as executed.
- Converts unsupported model output into accepted knowledge.
- Loses or silently overwrites contradictory evidence.
- Cannot identify the source or method behind a material finding.
- Treats repeated model agreement as independent confirmation without examining shared dependencies.
- Resumes from stale or incorrect investigation state.
- Exceeds permissions or ignores a refusal.
- Claims global novelty based only on its own memory or limited search.
- Hides an inconclusive result or failed experiment.

## 9. First acceptance experiment

The first experiment should be modest:

1. Client A opens a software-engineering investigation with a known, reproducible issue.
2. The engine stores the scope, baseline, acceptance criteria, and initial evidence.
3. Client A proposes hypotheses and a bounded test plan.
4. A tool executes the test and returns a result with provenance.
5. Client B, using a different model or client, resumes the investigation.
6. Client B challenges the interpretation or contributes counterevidence.
7. The engine preserves both contributions and records the evaluation decision.
8. A human reviewer inspects the final record and reproduces the key result.

Success demonstrates model-independent continuity and evidence handling in one bounded domain. It does not establish autonomous scientific discovery or broad domain generality.

## 10. Evaluation governance

- Keep benchmark tasks and answer keys protected from the evaluated model where possible.
- Separate model-generated judgments from independent evaluation.
- Disclose human intervention.
- Preserve failed and inconclusive runs.
- Avoid selecting only impressive examples.
- Do not claim superiority without comparable baselines and repeatable results.

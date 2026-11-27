# SECTAR-RS-001 — Computational Investigation of Charge-Carrier Dynamics and Collection in Bismuth Sulfide (Bi₂S₃)

**Document ID:** SECTAR-RS-001  
**Status:** Preliminary research proposal  
**Maturity:** Literature-grounded research direction; model, parameter set, and hypotheses require formalization and testing  
**Date initiated:** 2026-11-26  
**Research programme:** SECTAR — Solar Energy Collection Technology and Research  
**Owner authority:** Founder review required  
**Research mode:** Computational, literature-based, reproducible, initially local-first  
**Relationship to HiveNet:** HiveNet Compute Mesh is a possible execution and provenance environment. SECTAR is the scientific research programme; it is not a HiveNet subsystem.

---

## 1. Executive summary

This proposal establishes a computational research programme investigating photogenerated charge carriers in bismuth sulfide (Bi₂S₃), with an initial emphasis on the competing processes that determine whether electrons and holes survive long enough to be separated, transported, and collected.

The first study will examine how carrier generation, trapping, recombination, transport, and collection interact under explicitly defined material and device assumptions. It will begin with a small, reproducible rate-equation model and advance to a one-dimensional drift–diffusion model only after the literature review and baseline checks justify the additional complexity.

The project is motivated by a significant and evolving Bi₂S₃ literature. A 2018 review describes Bi₂S₃ as an n-type absorber with high optical absorption, while identifying high doping, poor electron mobility, and recombination associated with surface traps as possible performance limitations in the devices reviewed. A 2022 study of low-dimensional Bi₂S₃ nanocrystals reports near-infrared trap-state emission and ultrafast intrinsic trapping on picosecond timescales. A 2026 Nature study reports delayed bimolecular electron–hole recombination in Bi₂S₃ thin films and proposes a pseudo-direct bandgap interpretation involving thermal population of nearby direct and indirect transitions.

These observations must not be collapsed into one universal description of Bi₂S₃. They concern different sample forms, measurements, and mechanisms. The research will preserve those distinctions and test whether a model can represent the relevant mechanisms without treating trapping and recombination as synonyms.

The initial objective is not to claim a new solar-cell design or predict a commercially achievable efficiency. It is to establish a defensible, traceable computational baseline that can be independently inspected and reproduced.

## 2. Research scope and boundaries

### 2.1 Included

- Bi₂S₃ as a semiconductor and photovoltaic absorber candidate.
- Photogeneration of electron–hole pairs.
- Trap states and carrier trapping.
- Trap-assisted, bimolecular, and other recombination channels where evidence justifies their inclusion.
- Carrier lifetime and density dependence.
- Temperature and excitation-density dependence where supported by source data.
- Carrier transport and charge collection in progressively more realistic models.
- Sensitivity, uncertainty, numerical convergence, and reproducibility.
- Computational execution across local and optional remote resources.

### 2.2 Excluded from the first study

- Claims that a proposed filament, electrode, or collection geometry has been physically demonstrated.
- Claims of measured device performance from simulation alone.
- Unverified material constants or guessed parameter values presented as measured facts.
- Full first-principles electronic-structure calculations as the initial milestone.
- Fabrication, synthesis, or laboratory characterization.
- Biological, medical, or human-subject research.
- Claims of novelty, patentability, or priority without a separate prior-art review.

The separate SECTAR concepts involving solar filaments, collection structures, and material architectures may later become independent hypotheses. They must not be assumed to work merely because a simplified model produces favorable results.

## 3. Background and evidence already identified

The following sources provide a starting point, not a completed systematic literature review.

### 3.1 Bismuth-based photovoltaics review (2018)

N. C. Miller and M. Bernechea, “Research Update: Bismuth based materials for photovoltaics,” APL Materials 6, 084503 (2018). DOI: [10.1063/1.5026541](https://doi.org/10.1063/1.5026541).

The review describes Bi₂S₃ as an n-type semiconductor with a high absorption coefficient and a reported bandgap range affected by material form and quantum confinement/stoichiometry. It discusses early Bi₂S₃-based photovoltaic structures and identifies high doping, poor electron mobility, and surface-trap-associated recombination as possible limitations in the devices covered.

**Evidence boundary:** This is a review of literature available through its publication period. Its statements should not be treated as universal constants or as a complete account of later results.

### 3.2 Intrinsic trapping and recombination in nanocrystals (2022)

“​​Intrinsic Trapping and Recombination Dynamics in Low-Dimensional Bismuth Sulfide Nanocrystals,” Advanced Materials Interfaces (2022). DOI: [10.1002/admi.202200219](https://doi.org/10.1002/admi.202200219).

The study reports near-infrared trap-state emission and ultrafast intrinsic trapping in Bi₂S₃ nanocrystals, with carrier decay behavior varying with excitation fluence.

**Evidence boundary:** Nanocrystal observations must not be transferred automatically to bulk crystals or thermally evaporated thin films. Trapping is not automatically equivalent to irreversible electron–hole recombination; the model must distinguish capture, release, and recombination where the evidence allows.

### 3.3 Delayed bimolecular recombination and pseudo-direct bandgap (2026)

“Delayed electron–hole recombination in a pseudo-direct semiconductor,” Nature (2026). [Nature article](https://www.nature.com/articles/s41586-026-11223-x).

The article reports a mixed direct–indirect band-edge picture for Bi₂S₃ thin films and delayed bimolecular recombination relative to conventional direct-semiconductor expectations. It describes temperature-dependent population of nearby transitions as relevant to the recombination behavior.

**Evidence boundary:** This is a recent result that requires careful reading of the full paper and supplementary information. Its findings are not assumed to apply identically to nanocrystals, other phases, morphologies, defect densities, or device stacks.

### 3.4 Initial literature conclusion

The initial literature does not support a simplistic assumption that Bi₂S₃ always suffers from one dominant, fast electron–hole recombination process. The evidence points to material-form-dependent carrier dynamics, including trapping and delayed bimolecular recombination. The first task is therefore to reconcile mechanisms, measurement conditions, and sample characteristics before selecting numerical parameters.

## 4. Primary research question

**RQ-1:** How do carrier trapping, recombination pathways, carrier density, temperature, and transport properties jointly affect the predicted survival and collection of photogenerated charge carriers in defined Bi₂S₃ material and device configurations?

The first computational study will narrow this to:

**RQ-1A:** Under a clearly specified Bi₂S₃ thin-film or absorber model, how sensitive are predicted carrier survival and collection metrics to the relative strengths and temperature/excitation dependence of the supported recombination and trapping mechanisms?

## 5. Hypotheses

These are proposed hypotheses to be tested, not established conclusions.

- **H1 — Mechanism dependence:** Predicted carrier survival and collection will depend on which recombination and trapping mechanisms are included, rather than on a single generic lifetime parameter.
- **H2 — Material-form dependence:** Parameter sets derived from nanocrystals, thin films, and bulk material will not be interchangeable without introducing substantial model uncertainty.
- **H3 — Density and temperature dependence:** Where supported by the selected thin-film data, carrier dynamics will vary with excitation density and temperature in ways that a constant-lifetime model cannot fully represent.
- **H4 — Transport–recombination competition:** Collection outcomes will depend on the relationship between carrier transport timescales, recombination/trapping timescales, absorber geometry, and boundary conditions.
- **H5 — Model adequacy:** A model that explicitly represents the supported mechanisms will explain the selected reference data better than a simpler constant-lifetime baseline, subject to comparable parameter freedom and validation controls.

A result that does not support a hypothesis is a valid research outcome and must be retained.

## 6. Terminology and physical distinctions

The study must use the following terms carefully:

- **Photogeneration:** Creation of mobile or initially excited charge carriers following absorption of photons.
- **Carrier trapping:** Capture of a carrier by a localized state. Trapping may be reversible or may lead to recombination; it is not automatically a completed electron–hole recombination event.
- **Recombination:** A process that removes an electron–hole pair from the mobile carrier population, through a specified mechanism.
- **Bimolecular recombination:** A carrier-density-dependent process involving an electron and a hole; its effective rate and coefficient must be tied to the applicable material conditions and model.
- **Trap-assisted recombination:** Recombination mediated by defect or trap states. A Shockley–Read–Hall (SRH) formulation may be appropriate where its assumptions are justified.
- **Carrier lifetime:** A model- and condition-dependent timescale. A measured decay time must not automatically be interpreted as a unique intrinsic lifetime.
- **Transport:** Motion of carriers under electric fields and concentration gradients, commonly represented through drift and diffusion terms.
- **Collection:** Extraction of carriers at defined contacts or interfaces. It is not synonymous with photogeneration, absorption, or internal charge separation.
- **Collection efficiency:** A precisely defined ratio for a specified model boundary and carrier population. It must not be confused with external quantum efficiency or full power-conversion efficiency unless the complete relevant device model is included.

## 7. Modelling strategy

The project will use a staged model hierarchy. Each stage must pass validation before the next is treated as a reliable extension.

### Stage 0 — Literature and parameter registry

Build a source-backed table for every parameter considered. Each entry must include:

- Parameter name, symbol, units, and physical meaning.
- Numerical value or reported interval, if available.
- Material form: bulk, thin film, nanocrystal, nanowire, composite, or other.
- Crystal phase, stoichiometry, morphology, and preparation method where reported.
- Temperature, excitation wavelength, excitation fluence/density, and measurement method.
- Source DOI/URL, page/figure/table/supplementary location.
- Whether the value is measured, fitted, calculated, inferred, or assumed.
- Uncertainty, context, and transferability limitations.

No parameter is to be silently selected from a source describing a materially different sample.

### Stage 1 — Minimal rate-equation baseline

Implement a spatially uniform, explicitly simplified model of photogenerated carrier populations. The model will compare a constant-effective-lifetime baseline with progressively more specific recombination terms.

A generic starting form is:

    dn/dt = G - R(n,p,...)
    dp/dt = G - R(n,p,...)

where G is the generation term and R is the total recombination rate under the selected assumptions. The exact expression for R must be specified for each experiment. Candidate mechanisms include SRH/trap-assisted and bimolecular recombination; Auger or additional channels are included only if the source evidence and carrier-density regime justify them.

This model is a controlled baseline. It does not represent spatial transport, interfaces, or a complete solar cell.

### Stage 2 — Trap-state dynamics

Where the source data support it, introduce explicit trap occupancy, capture, emission/release, and recombination pathways. Compare a reversible-trapping model with an effective irreversible-loss approximation. Record where the available data cannot distinguish between these mechanisms.

### Stage 3 — One-dimensional transport and collection

Only after parameter provenance and rate-model validation, extend to a one-dimensional semiconductor continuity model, with drift, diffusion, generation, recombination, electrostatics, and explicit boundary/contact conditions as justified.

The model specification must state:
- Geometry and coordinate convention.
- Optical generation profile and illumination assumptions.
- Electron and hole transport parameters.
- Electric-field and electrostatic assumptions.
- Recombination and trap-state models.
- Contact/interface boundary conditions.
- Initial conditions and numerical solver.
- Definitions of collected charge and all reported metrics.

### Stage 4 — Comparative device or geometry models

Compare only clearly specified configurations. A proposed SECTAR filament or collection geometry may be introduced as a new model variant after a baseline geometry is validated. Any improvement must be compared against a matched baseline with equivalent assumptions, material parameters, and numerical accuracy.

### Stage 5 — Higher-fidelity methods

First-principles calculations, atomistic defect studies, or more advanced electronic-structure methods may be considered later if a specific unresolved question requires them and an appropriate compute environment is available. They are not prerequisites for the first milestone.

## 8. Initial computational experiment

**Experiment ID:** SECTAR-EXP-001  
**Working title:** Sensitivity of Bi₂S₃ carrier survival to trapping and recombination assumptions  
**Status:** Proposed; not yet run  
**Primary output:** Reproducible sensitivity dataset and model-validation report

### Procedure

1. Select one sample class and one source-backed dataset. The 2026 thin-film study is a candidate for the first focused reproduction; the 2022 nanocrystal study is a separate comparison, not a pooled dataset.
2. Extract experimental conditions and reported carrier-dynamics observations from the paper and supplementary material.
3. Build the simplest model capable of representing the selected observable.
4. Implement a constant-effective-lifetime baseline.
5. Implement only those additional recombination/trapping terms justified by the selected source.
6. Fit or estimate parameters using a documented method. Separate fitted parameters from independently measured inputs.
7. Perform sensitivity analysis over source-supported intervals and explicitly labelled exploratory intervals.
8. Compare model predictions against the selected observations using predeclared error metrics.
9. Test numerical stability, parameter identifiability, and sensitivity to initial conditions and solver tolerances.
10. Preserve all input data, scripts, environment details, logs, raw outputs, and analysis.

### Initial outputs and metrics

- Carrier population versus time under specified conditions.
- Effective decay times, with their precise definition.
- Relative contribution of each modelled loss pathway, where identifiable.
- Sensitivity of predictions to each parameter.
- Residuals and goodness-of-fit measures against the selected reference data.
- Uncertainty intervals or parameter ranges, where the data support them.
- Model comparison against the simpler baseline.
- A limitations register identifying mechanisms the data cannot resolve.

A parameter sweep is not evidence that every point in the sweep is physically realistic. The source-supported region and purely exploratory region must be visually and numerically distinguishable.

## 9. Validation and research-integrity requirements

The model must not be considered validated merely because it runs or produces plausible-looking plots.

Minimum checks:

1. **Dimensional analysis:** equations and parameters have consistent units.
2. **Limiting cases:** test zero generation, zero recombination, and other analytically interpretable limits.
3. **Conservation checks:** verify carrier balance under the model's stated assumptions.
4. **Numerical convergence:** test time step, spatial mesh (when applicable), solver tolerances, and domain size.
5. **Independent calculation:** reproduce selected results using a separate implementation or analytic check where feasible.
6. **Baseline comparison:** compare added model complexity against a simpler model using comparable validation criteria.
7. **Parameter identifiability:** report when different parameter combinations produce indistinguishable outputs.
8. **Uncertainty:** propagate source and fitting uncertainty; do not report excessive significant figures.
9. **Reproducibility:** a clean environment must be able to rerun the experiment from documented inputs.
10. **Negative results:** preserve failed fits, unstable runs, rejected models, and changes to the protocol.

Hashes establish byte identity relative to a recorded digest. They do not prove that source data are correct, that a model is physically valid, or that a result is scientifically true.

## 10. Data, software, and provenance plan

The project will use open, machine-readable formats wherever practical:

- CSV for tabular measurements and parameter sweeps.
- JSON for experiment manifests, parameter metadata, and machine-readable run records.
- Markdown for protocols, literature notes, and analysis.
- Plain-text logs for execution records.
- Version-controlled source code and environment specifications.
- Immutable or append-only experiment identifiers and artifact hashes.

Each run should record at minimum:

- Experiment ID and run ID.
- Protocol and source-data revisions.
- Code commit/revision and dependency versions.
- Parameter manifest and input-data hashes.
- Execution platform and relevant hardware/software details.
- Start/end timestamps and exit status.
- Solver configuration, random seed where applicable, and warnings.
- Output artifact paths, sizes, and hashes.
- Analysis revision and reviewer/acceptance status.

The research record should follow the FAIR principles—Findable, Accessible, Interoperable, and Reusable—while respecting data rights and source licenses. Public availability is desirable where lawful and appropriate, but it does not override licensing or other restrictions.

## 11. Relationship to HiveNet Compute Mesh

HiveNet Compute Mesh is a proposed provider-independent execution and recovery layer. It may later provide a useful way to distribute independent parameter-sweep jobs and preserve task provenance. It is not required to establish the first scientific result.

### Separation of responsibilities

- **SECTAR** defines the scientific question, model, parameters, protocol, and interpretation.
- **Compute Mesh** executes bounded computational tasks, preserves checkpoints and artifacts, and records execution provenance.
- **HiveNet** may provide node identity, consent, task coordination, and owner-governed resource sharing.
- **The researcher/owner** retains authority over protocol changes, data disclosure, acceptance of results, and conclusions.

A successful task execution is not scientific validation. Provider agreement is not independent scientific replication. A scheduler cannot decide whether a physical model is correct.

### Initial execution sequence

1. Run the minimal model locally and establish a reference result.
2. Package independent parameter combinations as deterministic tasks.
3. Verify that repeated local runs produce equivalent outputs within declared numerical tolerances.
4. Test task interruption, checkpoint/recovery, duplicate execution handling, and result integrity in the Compute Mesh prototype.
5. Compare a remote result with the local reference.
6. Add providers only after their current terms, quotas, data rules, and technical constraints have been checked.

### Candidate distributed-computing systems

- **BOINC Central:** Potentially relevant to large batches of independent scientific jobs. Its current published requirements include a scientific or nonprofit goal, open-source software, public non-sensitive input/output data, and workloads suited to volunteer computers. It is a candidate requiring application and eligibility review, not guaranteed compute capacity. [BOINC Central scientist guidance](https://boinc.berkeley.edu/central/scientist.php).
- **Parsl:** Candidate for Python task orchestration and execution across suitable providers or clusters. Its task and checkpoint semantics must be evaluated against the specific SECTAR workload.
- **FireWorks:** Candidate for managing scientific workflow dependencies, execution records, and recovery. Its infrastructure requirements and deployment overhead must be assessed.
- **Local execution:** Remains the reference baseline and must remain possible without any remote provider.

Do not use a provider in a way that violates its terms, evade quotas, upload sensitive data, or assume that a free tier guarantees persistent or unattended execution. Provider adapters must declare actual capabilities and limitations.

## 12. Resource and feasibility plan

The project is designed to begin with no purchased laboratory equipment and no paid compute requirement.

### Initial resources

- Existing Android tablet/phone and Termux or another accessible Python environment.
- Python scientific stack, using packages that can be installed and run within available memory.
- Public papers, supplementary information, and legally reusable datasets.
- Git-based source and document history.
- Local storage for small parameter sweeps and reproducibility artifacts.

### Constraints

- Mobile hardware and memory are limited; start with small models and modest sweeps.
- Heavy density-functional-theory or atomistic calculations are out of scope for the first milestone.
- Free cloud resources are variable, quota-limited, and governed by provider terms.
- A computational model can be wrong even when its code is correct.
- Published measurements may not expose all raw data or experimental metadata needed for a faithful reproduction.

If a study cannot be reproduced from accessible data, document the limitation rather than inventing missing values.

## 13. Milestones and deliverables

### M0 — Research charter and source audit

- [ ] Approve scope, research question, and initial sample class.
- [ ] Read and annotate the 2018 review, 2022 nanocrystal study, and 2026 thin-film study.
- [ ] Obtain and inspect supplementary data where available.
- [ ] Build a source/parameter registry.
- [ ] Identify disagreements, missing measurements, and non-transferable values.

**Exit criterion:** A traceable literature and parameter table, with unresolved gaps explicit.

### M1 — Reproducible minimal model

- [ ] Define the initial observable and model equations.
- [ ] Implement the constant-lifetime baseline.
- [ ] Add only source-justified mechanisms.
- [ ] Add unit, limiting-case, dimensional, and conservation checks.
- [ ] Record environment and deterministic run instructions.

**Exit criterion:** Independent rerun of the baseline produces equivalent results within declared tolerances.

### M2 — Reference-data comparison

- [ ] Reproduce selected published carrier-dynamics plots or tabulated observations where data permit.
- [ ] Report fitting method, residuals, uncertainty, and parameter identifiability.
- [ ] Compare the richer model against the simpler baseline.
- [ ] Document non-reproducible or contradictory observations.

**Exit criterion:** A reviewable comparison with the source data and a clear account of limitations.

### M3 — Transport and collection model

- [ ] Specify geometry, transport equations, contacts, and boundary conditions.
- [ ] Introduce spatial resolution and convergence testing.
- [ ] Define collection metrics precisely.
- [ ] Compare against analytically or independently checkable limiting cases.

**Exit criterion:** A numerically verified model whose assumptions and collection metrics are fully documented.

### M4 — Compute Mesh integration

- [ ] Package independent, deterministic sweep tasks.
- [ ] Test local execution, interruption, recovery, and artifact verification.
- [ ] Test one external provider only after policy/eligibility review.
- [ ] Compare remote outputs against local reference runs.

**Exit criterion:** Demonstrated task continuity and result equivalence for a bounded workload. This does not validate the underlying physics by itself.

### M5 — Research report and public release

- [ ] Consolidate methods, data, code, results, uncertainty, and limitations.
- [ ] Obtain independent technical review.
- [ ] Resolve licensing and attribution.
- [ ] Publish a versioned research release if appropriate.
- [ ] Consider a preprint or conference/journal submission only after the evidence and authorship record are ready.

**Exit criterion:** A reproducible, reviewable research package. Publication acceptance is not assumed.

## 14. Proposed repository layout

    research/
      sectar/
        README.md
        SECTAR-RS-001_BI2S3_COMPUTATIONAL_RESEARCH_PROPOSAL.md
        literature/
          source-register.csv
          notes/
        data/
          raw/
          processed/
        models/
          rate-equation/
          drift-diffusion/
        experiments/
          SECTAR-EXP-001/
            protocol.md
            parameters.json
            runs/
        analysis/
        reviews/
        releases/

Only create data and code directories when actual artifacts are ready. Do not populate them with empty placeholders that imply work has been completed.

## 15. Risks and controls

| Risk | Control |
|---|---|
| Conflicting Bi₂S₃ parameter values | Track morphology, phase, stoichiometry, temperature, and measurement method for every value. |
| Trapping confused with recombination | Model capture, release, and recombination as distinct processes where evidence permits. |
| Overfitting a small dataset | Compare against simpler baselines; report identifiability and uncertainty. |
| Unjustified parameter assumptions | Label measured, fitted, inferred, and exploratory values separately. |
| Numerical artifact mistaken for physical effect | Perform convergence, limiting-case, conservation, and independent checks. |
| Remote execution changes results | Keep local reference runs and compare outputs within defined tolerances. |
| Provider access disappears | Keep provider-neutral task packages and local execution as the fallback. |
| Simulation mistaken for experimental proof | Label every result as simulated, fitted, reproduced, or experimentally measured. |
| Premature novelty claims | Conduct a separate prior-art review before making novelty or priority claims. |

## 16. Open questions

1. Can the 2026 thin-film study's key carrier-dynamics observations be reproduced from the paper and supplementary information?
2. Which parameters are independently measured and which are inferred by fitting?
3. Which observed decay channels represent trapping, recombination, or coupled processes?
4. How should the pseudo-direct band-edge picture be represented in a tractable rate model?
5. Under what conditions can the nanocrystal trapping results be compared meaningfully with thin-film data?
6. Which transport parameters are sufficiently supported to justify a spatial collection model?
7. What is the smallest model that explains the selected data without excessive free parameters?
8. Which parts of the proposed SECTAR collection-geometry concepts can be expressed as falsifiable computational hypotheses?
9. Can a BOINC-style independent-job workload be packaged without compromising provenance or reproducibility?
10. What independent review would most effectively challenge the model and its interpretation?

## 17. Research integrity and authorship

This proposal records a research direction and a planned method. It does not claim that experiments have been run, results obtained, material properties measured, or hypotheses confirmed.

The researcher must retain a clear distinction between:
- Published observations.
- Values extracted from published observations.
- Values fitted by a model.
- Assumptions introduced for tractability.
- Predictions generated by simulation.
- Independent reproductions.
- Physical measurements, if any are later obtained.

Authorship, affiliation, contribution statements, software/data licensing, and any AI-assistance disclosure must be settled transparently before formal publication. No institutional affiliation, peer review, or external endorsement is implied.

## 18. Initial references

1. N. C. Miller and M. Bernechea, “Research Update: Bismuth based materials for photovoltaics,” APL Materials 6, 084503 (2018). [https://doi.org/10.1063/1.5026541](https://doi.org/10.1063/1.5026541).
2. “Intrinsic Trapping and Recombination Dynamics in Low-Dimensional Bismuth Sulfide Nanocrystals,” Advanced Materials Interfaces (2022). [https://doi.org/10.1002/admi.202200219](https://doi.org/10.1002/admi.202200219).
3. “Delayed electron–hole recombination in a pseudo-direct semiconductor,” Nature (2026). [https://www.nature.com/articles/s41586-026-11223-x](https://www.nature.com/articles/s41586-026-11223-x).
4. Wilkinson et al., “The FAIR Guiding Principles for scientific data management and stewardship,” Scientific Data 3, 160018 (2016). [https://doi.org/10.1038/sdata.2016.18](https://doi.org/10.1038/sdata.2016.18).
5. BOINC Central, “Computing with BOINC Central — Scientist guidance.” [https://boinc.berkeley.edu/central/scientist.php](https://boinc.berkeley.edu/central/scientist.php).

---

**Current status:** Proposed; founder review and M0 source audit pending.  
**Next action:** Complete the literature/parameter registry and choose the first reference dataset before writing the first model.

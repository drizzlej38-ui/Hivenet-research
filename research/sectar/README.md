# SECTAR — Solar Energy Collection Technology and Research

**Status:** Exploratory research programme  
**Maturity:** Initial computational research proposal; no results are claimed  
**Scope:** Semiconductor materials, solar energy conversion, charge generation, carrier dynamics, transport, and collection concepts.

## Research documents

1. [SECTAR-RS-001 — Computational Investigation of Charge-Carrier Dynamics and Collection in Bi₂S₃](SECTAR-RS-001_BI2S3_COMPUTATIONAL_RESEARCH_PROPOSAL.md) — initial literature-grounded proposal for a reproducible computational study of trapping, recombination, transport, and collection in bismuth sulfide.

## Programme principles

- Separate published observations, model assumptions, fitted parameters, simulation outputs, and physical measurements.
- Record material form, phase, stoichiometry, morphology, temperature, excitation conditions, and measurement method alongside every parameter.
- Do not treat carrier trapping and electron–hole recombination as interchangeable.
- Do not transfer parameters between nanocrystals, thin films, and bulk material without justification.
- Preserve failed runs, negative results, uncertainty, and changes to methods.
- Establish a local reproducible baseline before introducing remote or distributed compute.
- Treat simulation as a source of testable predictions, not as a substitute for physical measurement.

## Relationship to HiveNet

HiveNet Compute Mesh may provide provider-independent task execution, recovery, artifact integrity, and provenance for suitable SECTAR workloads. The scientific protocol and interpretation remain independent of the compute platform. A successful distributed run does not validate the physical model.

## Current next step

Complete the source audit and parameter registry for SECTAR-RS-001 before implementing the first rate-equation model.

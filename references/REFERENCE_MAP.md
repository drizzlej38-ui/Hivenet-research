# HiveNet Reference Map

**Status:** Initial bibliography and research map  
**Purpose:** Establish authoritative starting points. Inclusion does not imply that a source validates HiveNet or any particular implementation claim.

## Security architecture and engineering

1. **NIST SP 800-207 — Zero Trust Architecture.** National Institute of Standards and Technology (2020).  
   https://doi.org/10.6028/NIST.SP.800-207  
   Relevant to explicit access decisions, resource protection, and avoiding implicit trust based solely on network location. HiveNet-specific owner authority and federation semantics still require their own specification.

2. **NIST SP 800-218 — Secure Software Development Framework (SSDF) v1.1.** NIST (2022).  
   https://doi.org/10.6028/NIST.SP.800-218  
   Useful for secure development practices, provenance, vulnerability handling, and evidence discipline.

3. **NIST Cybersecurity Framework 2.0.** NIST (2024).  
   https://www.nist.gov/cyberframework  
   A risk-management framework for organizing governance, identification, protection, detection, response, and recovery activities.

## Data stewardship and Indigenous governance

4. **Carroll, S. R., et al. (2020). “The CARE Principles for Indigenous Data Governance.” Data Science Journal, 19(1), 43.**  
   https://doi.org/10.5334/dsj-2020-043  
   Introduces Collective Benefit, Authority to Control, Responsibility, and Ethics as principles for Indigenous data governance.

5. **Global Indigenous Data Alliance — CARE Principles.**  
   https://www.gida-global.org/care  
   Background and supporting resources for CARE-aligned data governance.

6. **Wilkinson, M. D., et al. (2016). “The FAIR Guiding Principles for scientific data management and stewardship.” Scientific Data, 3, 160018.**  
   https://doi.org/10.1038/sdata.2016.18  
   FAIR provides guidance on findability, accessibility, interoperability, and reuse. FAIR should not be treated as a substitute for consent, custodianship, or Indigenous governance; CARE and FAIR address complementary concerns.

## Research dissemination and citation

7. **GitHub documentation — Referencing and citing content.**  
   https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content  
   Useful for stable references to repository content and commits.

8. **Zenodo documentation — GitHub integration.**  
   https://help.zenodo.org/docs/github/enable-repository/  
   Describes archiving GitHub releases and assigning DOIs. A DOI provides a persistent scholarly reference; it is not peer review, proof of novelty, proof of ownership, or legal protection.

## Further literature required

The initial bibliography is intentionally incomplete. A publishable technical paper will need a deeper, claim-specific review of:
- Peer-to-peer and federated systems.
- Distributed consensus, Byzantine fault tolerance, and network partitions.
- Capability-based security and delegated authorization.
- Key management, secure messaging, and forward secrecy.
- Privacy-preserving telemetry and secure aggregation.
- Fault tolerance, self-healing systems, and adversarial resilience.
- Distributed machine learning and resource scheduling.
- Biohybrid, organoid, and biological-computing research, with careful distinctions between demonstrated systems and speculative interfaces.

## Citation practice

For every substantive technical claim:
1. Cite primary research, standards, or authoritative technical documentation where possible.
2. Record publication date and version.
3. Distinguish established findings from interpretation.
4. Explain where a cited source is analogous rather than directly applicable.
5. Avoid implying that a reference validates HiveNet unless the relevant design or experiment has actually been evaluated.

This map is a starting bibliography, not a completed systematic literature review.

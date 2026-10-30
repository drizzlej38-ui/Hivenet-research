# HiveNet Publication Readiness Checklist

**Status:** Working checklist  
**Rule:** Do not treat repository availability or a DOI as evidence of peer review, novelty, ownership, or technical validation.

## Before public release of a manuscript

- [ ] Founder confirms author display name.
- [ ] Confirm whether an affiliation should be listed or omitted.
- [ ] Agree on contribution statement.
- [ ] Prepare accurate AI-assistance disclosure consistent with the target venue.
- [ ] Confirm license and copyright choices.
- [ ] Review all included project documents for third-party material and licensing.
- [ ] Review cultural material and obtain appropriate custodial/community permissions; exclude material when permission is unclear.
- [ ] Check that no private keys, credentials, personal data, or sensitive operational details are present.
- [ ] Verify all citations and bibliographic metadata.
- [ ] Distinguish implemented, prototype, specified, and proposed claims.
- [ ] Tie every implementation claim to a commit, environment, command, result, and limitation.
- [ ] Remove unsupported novelty, security, performance, and biological-equivalence claims.
- [ ] Obtain independent technical critique where feasible.

## Before claiming implementation results

- [ ] Identify repository, file path, and commit SHA.
- [ ] Record platform, runtime, dependencies, and configuration.
- [ ] Record exact test or experiment commands.
- [ ] Preserve outputs or logs where appropriate.
- [ ] Report failures and limitations, not only successful cases.
- [ ] Separate test-plan coverage from tests actually executed.
- [ ] Avoid extrapolating from a prototype to production behavior.

## Before archival release

- [ ] Choose a stable release tag.
- [ ] Review the exact release contents.
- [ ] Confirm license and metadata.
- [ ] Enable the appropriate GitHub-to-Zenodo archival workflow if desired.
- [ ] Verify the resulting DOI and archived version.
- [ ] Cite the exact version, not an unpinned moving branch.

## Potential publication sequence

1. Foundational architecture and governance paper.
2. SRM and AGP technical specification/evaluation papers.
3. ASH and collective diagnostic-memory paper.
4. ENDCAP implementation and reliability paper.
5. Distributed compute scheduling experiments.
6. Separate biodigital research review or hypothesis paper after a focused literature review.

## Publication venue decision

For each manuscript, assess:
- Scope and audience.
- Whether the venue accepts conceptual or systems papers.
- Peer-review process and expected evidence.
- Fees and open-access terms.
- Preprint policy.
- Data, code, and artifact requirements.
- Conflict-of-interest and AI-assistance disclosure requirements.

## Non-negotiable integrity rules

- No claim that a patent is filed or pending.
- No claim of peer review before peer review occurs.
- No claim of formal verification without a formal verification artifact and scope.
- No claim of production readiness based solely on a prototype.
- No claim of biological integration based on analogy or conceptual architecture.
- No publication of culturally governed knowledge without appropriate authorization.

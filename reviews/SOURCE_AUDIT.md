# HiveNet Source and Claim Audit

**Status:** Initial research audit  
**Purpose:** Identify alignment issues, evidence gaps, and publication risks before drafting definitive technical claims.

This audit is a working assessment of the project documents reviewed to date. It is not a formal security audit, legal opinion, peer review, or independent verification of implementation.

## 1. Architecture alignment

### Coordinator and sovereign mesh

Earlier architecture material describes coordinator, router, model-pool, and validator functions. Later mesh material emphasizes independently controlled nodes, group-scoped discovery, owner-audited identities, and optional gateways.

**Working reconciliation:** coordination is a logical role or service that may be hosted by a node. It is not inherently a permanent central authority. A coordinator may be local, temporary, delegated, replaceable, or absent where unnecessary.

**Questions requiring explicit specification:**
- Who appoints, authorizes, limits, and replaces a coordinator?
- What happens when coordinators disagree, become unreachable, or act maliciously?
- Can nodes continue useful operation without a coordinator?
- How are policy conflicts resolved without silently elevating one node?
- Which decisions require human-owner approval?

Do not describe the architecture as fully decentralized until these behaviors are specified and tested.

## 2. Terminology control

- Current corrected expansion of **S.P.E.E.D.**: **Emergent Endogenic Design**. Earlier variants should be marked historical or superseded.
- **AGP** terminology has evolved around Access Grant Pointer / access-grant pointer tokens. A canonical definition, lifecycle, and threat model should be approved before protocol claims are made.
- **SRM** is Secure Resource Management + Messaging.
- **ASH** is Artificial System Health. Keep health/diagnostic functions distinct from integrity and evolution mechanisms such as SY-M unless a later specification deliberately unifies them.

## 3. Security claims requiring qualification

The following concepts need concrete mechanisms and evidence before strong security language is used:

| Claim area | Evidence needed |
|---|---|
| Forward secrecy | Key agreement, rotation, compromise recovery, and a stated threat model |
| Node identity | Enrollment, key custody, revocation, rotation, and recovery procedures |
| Reputation | Sybil resistance assumptions, poisoning resistance, appeal, and limits |
| Multi-node agreement | Consensus model, quorum assumptions, partitions, and failure semantics |
| Instant propagation | Delivery guarantees, consistency model, retry behavior, and measurable latency |
| Sanitization / detonation | Coverage limits, sandbox assumptions, evasion tests, and residual risk |
| Hashes | State clearly that a hash supports integrity comparison, not benignness, authorization, or authorship |
| Zero-knowledge | Use only for a defined cryptographic construction with a stated proof and security model |

A successful integrity check does not establish that content is safe. A trusted identity does not establish that every action by that identity is authorized.

## 4. ASH and collective immune memory

The design direction of observable, owner-governed telemetry is promising as a research topic. The system should specify:
- Exact telemetry fields and collection triggers.
- Whether data stays local by default.
- Owner inspection, export, deletion, and sharing controls.
- Retention and expiration.
- False-positive handling and quarantine review.
- Resistance to poisoned reports and malicious consensus.
- Metadata privacy and risks of behavioral inference.
- Consent and revocation for shared telemetry.

Telemetry should not silently expand from operational signals into private semantic-content collection.

## 5. ENDCAP evidence boundary

The described Python prototype includes encrypted archive operations, owner-key handling, signing, manifest-last commit behavior, verification, retrieval, and status reporting. These are implementation descriptions that must be tied to an exact repository revision and reproducible test output before publication as verified results.

Recommended evidence record for every implementation claim:
- Repository and path.
- Commit SHA or release.
- Runtime and dependency versions.
- Exact command or test invocation.
- Observed result and date.
- Known limitations and untested cases.

Do not infer streaming-read behavior, crash consistency, or large-file performance from a design intention alone.

## 6. Indigenous and culturally governed knowledge

Technical discoverability must not override community authority. Knowledge may be family-held, community-held, ceremonial, seasonal, restricted, or otherwise governed by protocols that cannot be reduced to a public/private switch.

Before including cultural material, confirm:
- Who has legitimate authority to authorize its use.
- Whether permission covers preservation, analysis, publication, and redistribution separately.
- Whether attribution, access conditions, or benefit-sharing are required.
- Whether the material should be excluded entirely.

CARE-aligned governance is relevant; FAIR data principles alone do not establish culturally appropriate permission.

## 7. Patent and legal-status correction

**No patent is claimed as filed or pending.** A repository filename or draft document is not evidence of legal status. Any patent-related artifact should be inspected and accurately classified as a draft, historical note, or other document before inclusion in a public research release.

## 8. Historical and evidentiary discipline

- Historical summaries are snapshots, not proof of current implementation.
- A test plan is not a test result.
- A test script is not proof that the script was run.
- A prototype is not a production system.
- A proposed design is not an experimentally validated result.
- A conceptual biodigital application is not evidence of a working biological interface.

## 9. Immediate research priorities

1. Approve a canonical glossary and versioned terminology.
2. Reconcile coordinator roles with sovereign-node principles.
3. Define AGP lifecycle and authorization semantics.
4. Publish reproducible ENDCAP and ASH evidence records.
5. Establish threat models for SRM, AGP, node identity, and shared telemetry.
6. Separate conceptual biodigital hypotheses from engineering results.
7. Establish authorship, license, and cultural-data review before formal release.

## Audit conclusion

HiveNet contains a coherent set of research directions, design principles, and prototype work. The strongest publication approach is to present it as an evolving framework with clearly separated maturity levels, explicit open questions, and reproducible evidence—not as a finished or formally proven system.

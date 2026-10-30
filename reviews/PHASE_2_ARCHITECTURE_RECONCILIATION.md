# Phase 2 — Architecture Reconciliation

**Status:** Initial source-based reconciliation; founder review required  
**Date:** 2026-10-30  
**Source repository:** https://github.com/drizzlej38-ui/hivenet-docs  
**Source branch:** `main`  
**Source tree SHA inspected:** `15d854a3f44a097b88a79ae27a4e372ef4a3d97b`

This document compares the current source documents and selected code artifacts. It does not modify the source repository. Findings are an engineering/research review, not a formal security audit, independent penetration test, or legal opinion.

## 1. Executive findings

The source material contains two distinguishable architectural stages:

1. **Single-coordinator proof-of-concept:** a LAN-oriented Python coordinator/worker arrangement with a central task dispatcher.
2. **Sovereign mesh target architecture:** independently controlled nodes, group-scoped visibility, owner-audited identity, optional gateways, and coordination as a bounded function.

These can be reconciled without discarding either. The first is an early implementation baseline; the second is a target architecture. They must not be described as though the proof-of-concept already implements the sovereign mesh.

The most important corrections before publication are:

- Explicitly label the coordinator/worker code as a limited LAN proof of concept, not a federated mesh.
- Treat coordination as a role/service in the target architecture, while acknowledging the current implementation has one central coordinator.
- Establish a single canonical terminology registry. The source glossary contains an outdated S.P.E.E.D. expansion relative to the founder's correction.
- Rewrite SRM's strongest security claims as hypotheses or requirements until protocol mechanisms and tests exist.
- Resolve incompatible collective immune-memory schemas.
- Reconcile cultural stewardship language with explicit community/custodian authority and restricted knowledge.
- Separate source-repository artifacts from research claims. The source repository contains mixed-purpose material; do not copy it wholesale into this research repository.

## 2. Architecture evolution: coordinator versus sovereign mesh

### Source evidence

- `ARCHITECTURE.MD` (blob `3cb524a614d4d9da3b182641ca1912e7c8085a6a`) depicts a central coordinator, task router, model pool, validator/consensus layer, and response aggregator. Its implementation roadmap places distributed mesh networking in a future phase.
- `coordinator.py` (blob `31f6e6d30a19c9aea75ea68541b2e336f65ff7a7`) implements one coordinator that registers workers and dispatches work.
- `worker_node.py` (blob `c7791075a90ae81533ff81b199566126a327d4b6`) implements a worker that announces to the coordinator and listens for tasks.
- `HIVENODE_SOVEREIGN_MESH.md` (blob `89af8a94d7dad3acf4621a6090397d40ea971fe0`) describes independent nodes, group-scoped visibility, optional gateway bridges, owner-audited identity, and distributed local awareness.

### Reconciliation

The coordinator is a valid **deployment role**, not a mandatory constitutional authority of the target system.

- In the current proof of concept, the coordinator is a central runtime dependency.
- In the target architecture, coordination may be hosted by a node or service, locally or temporarily.
- A mesh deployment may have multiple coordinators for different scopes, or no active coordinator for tasks that do not need one.
- Coordination authority must be bounded by owner policy and explicit task grants.
- Coordinator failure must not silently transfer authority to another node. Replacement, delegation, and conflict behavior must be specified.
- Local operation should remain possible when the network or coordinator is unavailable, to the extent local resources permit.

**Publication rule:** Say “the project explores a path from a single-coordinator prototype toward a federated sovereign mesh.” Do not say “the current implementation is decentralized” or “there is no central point of failure.”

### Required future specification

Create a Coordinator Role and Failure Semantics specification defining:
1. Appointment and authorization.
2. Scope and expiration.
3. Delegation and replacement.
4. Multiple coordinators and conflicting decisions.
5. Partition behavior and stale policy handling.
6. Local fallback and graceful degradation.
7. Owner override and auditability.
8. Proof that no role acquires authority merely through discovery or technical capability.

## 3. Node roles and taxonomy

The documents use several different vocabularies:

- The mesh document lists Relay, Compute, Storage, Sensor, and Gateway.
- ASH refers to archive, gateway, ghost, triage, sentinel, and compute-like behavior.
- SRM describes Sanitizer, Triage, Detonation, and Render Proxy as service roles.
- Earlier architecture material uses coordinator, router, model pool, validator, and aggregator.

These need not all be mutually exclusive node classes. Some are **node capabilities**, some are **network roles**, and some are **services running on a node**.

### Proposed taxonomy separation (for review)

| Layer | Examples | Meaning |
|---|---|---|
| Node capability | compute, storage, sensor, network | What the hardware/service can provide |
| Network role | relay, gateway, coordinator, registry | What responsibility it performs in a scope |
| Security service | sanitizer, triage, detonation, sentinel | What security function it runs |
| Application service | inference, archive, render proxy | What task or user-facing function it provides |

A node may host multiple services, and roles may change, but only under owner-approved policy. This is a proposed organizing model, not yet a founder-approved canonical schema.

**Missing source artifact:** the mesh and ASH documents refer to `NODE_CLASSES.md`, but no file with that exact name appears in the inspected source tree. The canonical node-class specification therefore remains unlocated.

## 4. Authority, capability, and consent

The founding principles and architecture repeatedly prioritize owner authority and local control. The mesh document adds inspectability by the device owner and explicit owner policy controls. These ideas support the governance proposition:

> Knowledge is not capability. Capability is not command. Authority is not consent.

For implementation, the proposition needs distinct enforceable checks:

- **Discovery:** learning that a resource exists.
- **Capability:** learning that it can perform an operation.
- **Authorization:** receiving a valid, scoped grant from the legitimate owner or custodian.
- **Execution:** performing only the authorized operation within scope.
- **Audit/revocation:** allowing the grantor to inspect and revoke according to defined rules.

Do not infer authorization from trust level, group membership, reputation, node class, or successful discovery.

## 5. AGP and SRM: specification gaps

### Current documented idea

The glossary and SRM documents describe AGP as a pointer/token that refers to a resource at its source and expresses access level, time-to-live, and a verification threshold. SRM adds message triage and content-sanitization services.

### Unresolved protocol fields

The documented compact string does not yet define enough information for an interoperable authorization protocol. A complete versioned schema should address:

- Issuer identity and signing key identifier.
- Intended subject/recipient or audience.
- Canonical resource identifier and source locator resolution.
- Exact permitted operations and constraints.
- Expiration, nonce, replay prevention, and clock-skew behavior.
- Revocation mechanism and offline/stale-policy behavior.
- Delegation limits and whether sub-grants are permitted.
- Threshold semantics: who selects validators, how independence is assessed, and what happens when validators disagree or are unavailable.
- Cryptographic signature format and canonical serialization.
- Binding to a specific request/session and protection against token substitution.
- Audit and owner-visible grant history.

A SHA-256 content hash can identify or integrity-check bytes when compared against a trusted expected hash. It does not itself authenticate the issuer, prove permission, establish safety, or locate the resource.

### SRM claims to downgrade pending evidence

The source SRM document claims “perfect forward secrecy at the identity layer,” instant reputation propagation, zero persistence by default, and a self-immunizing network. The reviewed material does not provide the full key-agreement protocol, revocation and replication semantics, persistence model, or validation evidence necessary to establish those claims.

Recommended language:
- “ephemeral or task-scoped identifiers are proposed” rather than “perfect forward secrecy.”
- “reputation updates may be propagated” rather than “propagates instantly.”
- “default non-persistence is a design goal, subject to explicit local logs, caches, and owner-selected retention” rather than “nothing persists.”
- “triage and shared threat indicators are intended to improve detection” rather than “the network becomes self-immunizing.”

### Important semantic distinction

“Files never move” is too absolute if a recipient can read or edit a remote resource. Bytes must be transmitted or rendered somewhere for remote access. More precise wording would be: “The authoritative resource remains at its source; an access grant authorizes a scoped read, preview, or remote operation without treating an attachment copy as the primary transfer model.” Confirm this wording with the founder.

## 6. ASH and the Sovereign Telemetry Boundary

### Strongest coherent design principle

The ASH documents converge on a clear boundary: monitor system/agent behavior and resource use, not the human owner's private semantic content. The fuller addendum also asserts owner custody and no owner-bypass.

### Source inconsistencies and open decisions

- `ASH.md` describes an Isolation Chamber, freeze-frame, diagnostic swarm, behavioral repository, and biological taxonomy.
- `ASH_Addendum_Sovereign_Telemetry_Boundary.md` merges prior drafts and explicitly flags “No Owner-Bypass” for confirmation.
- `ASH_TELEMETRY_BOUNDARY.md` and `SOVEREIGN_TELEMETRY_BOUNDARY_V2.md` use different three-axiom formulations.
- The addendum introduces `sentinel` as a node class while noting it is absent from the earlier node-class list.
- ASH freeze-frames include active AGP tokens, telemetry, and recent interaction hashes. The privacy implications and exact owner-controlled access rules need specification.

### Required precision

“Mathematically enforced” is not established by prose. To make the boundary enforceable, define:
- Exact telemetry schema and collection points.
- Explicitly prohibited data sources and APIs.
- Whether hashes of user content are prohibited (the addendum says semantic content must not be hashed).
- Local encryption and owner key custody.
- Export/sharing as explicit opt-in.
- Retention, deletion, and backup behavior.
- Verification tests proving ASH cannot read protected content.
- Detection and response when ASH itself violates policy.
- False-positive review and owner appeal.

Behavioral metadata can still reveal sensitive patterns. “No semantic content” is a useful minimization rule, not a guarantee of zero privacy risk.

## 7. Collective Immune Memory: schema conflict

The source contains two incompatible schemas:

- `IMMUNE_MEMORY.MD` v1.0: effect-oriented classifications, aggregate trigger counters, a mitigation string, and confidence score.
- `IMMUNE_MEMORY.md` v1.2: explicitly preserves Option A (attack-type/severity taxonomy, event sequence, signed record, quarantine recommendation) and Option B (effect taxonomy, aggregate counters, confidence score), pending a decision.
- `COLLECTIVE_IMMUNE_PROTOCOL.md` introduces a related Phenotype Record structure.

Do not claim the schema is finalized.

### Recommended research direction (not adopted)

Use separate fields for separate questions:
- `event_type`: observed behavior or protocol event.
- `resource_effect`: resource/authority effect.
- `severity_assessment`: local assessment with defined scale and uncertainty.
- `evidence_summary`: minimized behavioral features, with privacy review.
- `provenance`: signer, key identifier, software/version, timestamp, and source scope.
- `recommendation`: advisory action, not an automatically binding command.
- `confidence`: calibrated only after evaluation; otherwise omit or label subjective.

A signature can establish that a record was signed by a key; it does not establish that the observation is true. A hash of a behavioral pattern is not automatically “zero knowledge.” That term should be reserved for a defined cryptographic proof system with a stated security property.

Sharing should be opt-in and policy-scoped. The source phrase “a node must warn the mesh” needs reconciliation with owner sovereignty and consent.

## 8. Reputation and trust

The Sovereign Reputation document distinguishes private owner-visible details from an abstract public trust level. SRM, however, describes a shared ledger whose scores propagate across the mesh.

These models can be reconciled only if the project specifies:
- What exact value is public (if any).
- Whether sharing is opt-in and group-scoped.
- Who can issue and challenge a report.
- How revocation, false positives, and appeals work.
- Whether reputation is local policy input or a network-wide decision.
- How Sybil identities, collusion, and poisoning are handled.
- How trust decays and how new nodes are treated.

Reputation is not proof of identity, authorization, truthfulness, or safety. A node's trust score must never replace a grant from the resource owner.

## 9. Cultural stewardship and Estuary

The founding principles and parallel-project documents express a valuable goal: preserving living voices and allowing knowledge to travel in original form. They also contain broad phrases such as “accessible to anyone,” “owned by no one,” and “without asking anyone's permission.”

Those phrases conflict with the project's other stated commitment to custodianship and sovereignty when applied to culturally restricted knowledge. They cannot all be universal defaults.

### Reconciliation required

- Publicly shareable material may be made discoverable and accessible under its custodians' terms.
- Restricted, family-held, ceremonial, seasonal, or otherwise governed material may require limited discovery, restricted access, or no digital circulation.
- Preservation, transcription, translation, analysis, publication, and redistribution are separate permissions.
- A technical custodian is not automatically a cultural authority.
- The system must not assign custodial authority or cultural legitimacy through account creation, membership, or reputation score.

CARE-aligned governance and community-specific protocols should inform this layer. Do not copy language/audio files or other potentially sensitive cultural material into the research repository as part of a technical documentation migration.

## 10. S.P.E.E.D. terminology correction

The source `GLOSSARY.MD` currently says “Symbiosis Protocol: Emergent Endogenic Design.” This conflicts with the founder's later explicit correction for current terminology: **Emergent Endogenic Design**.

For current research documents, use **Emergent Endogenic Design** only. Treat the glossary's longer expansion as stale historical wording until the source glossary is intentionally corrected by the founder.

## 11. Source-repository hygiene

The inspected source repository contains relevant architecture documents and code alongside unrelated learning materials, personal writing, language/cultural files, third-party books, reports, and a PDF whose filename includes “Provisional Patent.” This repository is a mixed working archive, not a clean research corpus.

Actions:
- Do not copy the repository wholesale into the research repository.
- Cite only relevant technical artifacts and their exact revisions.
- Review licenses and third-party rights for any material considered for redistribution.
- Do not infer patent filing or pending status from a filename. The founder has explicitly stated that no patent exists or is pending; the PDF's legal status/content has not been established by this audit.
- Treat project summaries as historical context, not as current implementation evidence.

## 12. Proposed canonical architecture statement

The following statement reconciles the current prototype and target design without overstating maturity:

> HiveNet is a modular, local-first coordination and resource-sharing framework. Its current demonstrator uses a central coordinator to register workers and dispatch bounded test tasks over a local network. The longer-term architecture explores federation among independently controlled nodes. In that target architecture, coordination is a bounded role or service rather than an inherent central authority. Participation, resource sharing, external connectivity, and data disclosure are governed by explicit owner- or custodian-authorized policies.

This statement is recommended for founder review; it is not silently adopted as a final architecture decision.

## 13. Priority order

1. Approve the prototype-versus-target distinction and canonical architecture statement.
2. Establish a canonical role taxonomy: capabilities, network roles, security services, application services.
3. Correct the S.P.E.E.D. glossary entry in the source of truth.
4. Specify AGP authorization semantics and lifecycle.
5. Resolve the immune-memory schema and opt-in sharing model.
6. Consolidate the Sovereign Telemetry Boundary and its testable enforcement requirements.
7. Define coordinator failure, replacement, and partition behavior.
8. Reconcile Estuary access language with community custodianship.
9. Produce reproducible evidence for code and tests before making implementation or performance claims.

## 14. Source artifacts inspected

The following exact files were read from `drizzlej38-ui/hivenet-docs` on `main`:

| Artifact | Blob SHA |
|---|---|
| `ARCHITECTURE.MD` | `3cb524a614d4d9da3b182641ca1912e7c8085a6a` |
| `FOUNDING_PRINCIPLES.MD` | `9055a8953b9db8d54f8c8f468f31162fd90f3f95` |
| `GLOSSARY.MD` | `b2f487a8d2ba8af156c8cd6840dc915f37a0cd7f` |
| `HIVENODE_SOVEREIGN_MESH.md` | `89af8a94d7dad3acf4621a6090397d40ea971fe0` |
| `SRM.MD` | `132ee5858b8d2e1aea206849e7e2f6bd2948e979` |
| `ASH.md` | `e5d571447c53ffd3f03a1856fb355687bf9e358d` |
| `ASH_Addendum_Sovereign_Telemetry_Boundary.md` | `e002f8c96c9554535644585721c3d630364e0cc2` |
| `ASH_TELEMETRY_BOUNDARY.md` | `c9bdc4f7a6ffedbdae69dfc407aef4298b9d51ed` |
| `SOVEREIGN_TELEMETRY_BOUNDARY_V2.md` | `44d2f870a1a3a4614d057e67b8366b5ceee8cd4c` |
| `COLLECTIVE_IMMUNE_PROTOCOL.md` | `b4b383cf876442d4240df4ab7aea8d2e3003b851` |
| `IMMUNE_MEMORY.MD` | `37d82343845231ca5101cbf8c36b7e8ee314294e` |
| `IMMUNE_MEMORY.md` | `5209defeebc3c8db20741aef78e337b51744daef` |
| `SOVEREIGN_REPUTATION.md` | `a6aefe732d508fdb71039be10380c9af65d8cfe5` |
| `STRESS_TEST_PLAN.md` | `fd1c62f2b79ecc80a05182e49d67eb29b2f65c5d` |
| `TEST_HARNESS_GUIDE.md` | `ca495a539bc52b66d40106b93db4cb778aec4ec6` |
| `HiveNet_Project_Summary.md` | `81774dce9477e65f63270e43efbe88bbd7ee8afa` |
| `PARALLEL_PROJECTS.MD` | `d7b22bc1a7e07a180f2718e40c6d232fa64a1653` |
| `coordinator.py` | `31f6e6d30a19c9aea75ea68541b2e336f65ff7a7` |
| `worker_node.py` | `c7791075a90ae81533ff81b199566126a327d4b6` |
| `test_harness.py` | `41b9daf5191e9a02858bfe7954e61b14ef65c7e4` |
| `server.py` | `ba764e9e49dde1ef9a6bcda66ed2a1c67bd2ccb8` |

This list is the inspected subset, not the entire source repository.

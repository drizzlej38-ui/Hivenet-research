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


## 15. Additional source repository: SkyNet

A second project repository, `drizzlej38-ui/SkyNet`, was also inspected after it appeared in the connected GitHub repository list. Its `main` tree SHA at inspection was `a1e454edbb81e14b0f95980cae2382249c42fbb7`. It contains more developed subsystem specifications and an ENDCAP/AGP federation concept prototype. This materially extends the earlier review; the first source repository is not the only relevant source of truth.

### New evidence located

- `ENDCAP.md`: a versioned self-describing node specification with standalone operation, completeness, owner identity, and set membership.
- `AGP_FEDERATION.md`: a structured AGP token schema with issuer, subject, grantee, permissions, expiry, and revocation fields; a logical set and informational federation map; and a delegation model.
- `NODE_CLASSES.md`: the previously missing node-class specification, with eight classes and composability rules.
- `DRAGON_RADAR.md`: a detailed monitoring, alert, TX-state, canary, and anomaly-scoring design.
- `AGENT_CARD_SCHEMA.md`: a combined discovery/identity schema intended to connect A2A-style agent discovery with ENDCAP and AGP.
- `endcap_prototype.py`: a deliberately incomplete Python prototype demonstrating ENDCAP manifests, AGP permission objects, node sets, and owner-mediated membership.

### Updated node taxonomy finding

The earlier finding that `NODE_CLASSES.md` was missing applies only to `hivenet-docs`. It is present in the SkyNet repository. However, the two SkyNet documents are not yet synchronized: `AGENT_CARD_SCHEMA.md` declares `node_class` as a string in its field description/example, while `NODE_CLASSES.md` says it is an array to support composability. The schema should be version-aligned before implementers rely on it.

The eight classes in `NODE_CLASSES.md` are inference, coordinator, triage, archive, gateway, sentinel, registry, and ghost. These should be treated as a current proposed canonical node-class list, subject to founder confirmation. Service sub-roles such as sanitizer, detonation, render_proxy, and consensus are distinct from the node-class list.

### AGP specification is more developed, but not yet a verified protocol

`AGP_FEDERATION.md` defines a richer token object than the earlier compact string alone. It identifies issuer, token ID, subject node and set, grantee, permission flags, issue/expiry times, revocation state, and scope notes. It also states that delegation cannot exceed the delegator's permission scope.

However, the inspected `endcap_prototype.py` explicitly says cryptographic signing, transport/discovery, persistent storage, Dragon Radar, Confluence handshake, and delegation chains are not implemented. The Python `AGPToken` is therefore a mutable in-memory permission object, not a cryptographically authenticated AGP credential.

Static code review also found that `ENDCAPNode.read_all()` and `read_metadata()` check that a supplied token targets the node and has the relevant permission, but do not compare the requestor identity with `token.grantee_id` or validate an issuer signature. A token object with the right node ID and permission could therefore be presented by a different requestor within this prototype. This is a prototype authorization defect, not a finding about a later implementation.

The prototype's `NodeSet` stores members in a dictionary keyed only by `node_id`; registering multiple grants for the same node overwrites the previous token entry. The demo registers family and researcher tokens for the same node, so the set abstraction does not preserve multiple grantee grants for that node. This should be fixed before using the prototype as evidence of multi-grantee authorization.

The `write()` method in the prototype is owner-only; the AGP `write` permission exists in the data model but is not implemented as a grantee write path. The prototype is in-memory only and does not demonstrate durable storage, encrypted archive payloads, network federation, or crash-safe atomic commits.

### Dragon Radar: clarify pre-authorized automation and canary limits

`DRAGON_RADAR.md` explicitly states that Dragon Radar watches but does not act unilaterally, while also specifying automatic temporary AGP suspension for TX-flagged nodes. These can coexist if suspension is defined as a narrow, pre-authorized, temporary protective action, with clear owner notification, expiry/review, appeal, and restoration semantics. The document should not simultaneously imply that all response requires contemporaneous human action and that automatic suspension is unconditional.

The anomaly score thresholds and weights are specified as constants, but no calibration data, false-positive rate, adversarial evaluation, or implementation is present in the inspected source set. Treat them as proposed policy parameters, not validated detection performance.

Canary URLs and remote callbacks can themselves disclose access metadata (such as network address, time, and correlation identifiers), fail when network access is blocked, or be triggered by automated preview/scanning systems. They should be opt-in, threat-modelled, and described as indicators rather than conclusive proof that a particular person intentionally accessed or leaked a document. “Identifies exactly which authorized recipient” is too strong without recipient-unique marking, careful forwarding/collusion analysis, and false-trigger controls.

### ENDCAP completeness invariant needs operational semantics

The ENDCAP specification and prototype assert that each node is standalone and complete, and that records are not split across nodes. In the prototype, `complete=True` is a constructor invariant; it does not by itself prove crash consistency or make partial writes impossible. Atomicity, commit markers, durable flush behavior, recovery after power loss, and storage integrity must be established by the actual storage implementation and tests.

The SkyNet ENDCAP identity-node prototype is also distinct from the encrypted archive implementation described in project history. Do not conflate a self-describing manifest and in-memory record container with the separate encrypted ENDCAP archive package.

### Updated publication conclusion

The SkyNet repository contains more than prose: it includes a deliberately incomplete ENDCAP/AGP concept prototype. This supports the classification **prototype source exists**, while its own header and static inspection clearly identify major unimplemented security and persistence features. It does not establish production-ready ENDCAP, signed AGP, network federation, or Dragon Radar enforcement.

### Additional SkyNet source revisions inspected

| Artifact | Blob SHA |
|---|---|
| `AGENT_CARD_SCHEMA.md` | `b29830a21074f3e4f7e4558a01bad29e2d357ac9` |
| `AGP_FEDERATION.md` | `152415b9e98005d0f7c1bf98eb6882291bf4f2e1` |
| `DRAGON_RADAR.md` | `80e8edda8e61fba0855e594f85a3c60e24d77629` |
| `ENDCAP.md` | `390fea98c4cd831bafdd701c90d14c87699b6302` |
| `NODE_CLASSES.md` | `1ca8f3720658c3b13ab39e402cabc83546a32b2c` |
| `endcap_prototype.py` | `9361dc3868648e4b4bbe52ebbd568ad700806887` |

The missing SHA values above are intentionally left blank rather than guessed; they should be filled after retrieval of those exact file metadata records.

# MNN Local Routing and Domain Admission: Protocol Draft

**Document type:** Protocol design draft  
**Status:** Proposed; not implemented or security-reviewed  
**Version:** 0.1  
**Date:** 2026-11-19  
**Parent:** [MNN Concept and Architecture](04_MESH_NEURAL_NETWORKING_MNN_CONCEPT.md)

## 1. Purpose

This document turns the MNN concept into a first-pass protocol model. It defines how a neuron can forward compatible signals from other neurons using local peer awareness, how a new neuron enters a specialization domain, and how routing remains bounded without global topology knowledge.

This is a design draft. Field names, message formats, cryptographic choices, timers, and algorithms remain subject to simulation and review.

## 2. Protocol invariants

1. A neuron forwards only traffic allowed by its declared domain policy.
2. A relay preserves the original signal identity and origin.
3. Forwarding does not imply semantic interpretation.
4. A node uses direct-peer information and bounded route state; a complete topology map is unnecessary.
5. A new neuron is admitted through its relevant domain, not through a mandatory global broadcast.
6. Discovery never grants authorization.
7. Routing state is bounded, expiring, and recoverable.
8. A node that cannot establish a compliant route fails closed rather than forwarding incompatible traffic.

## 3. Identity and domain descriptors

Each participating neuron has a logical descriptor:

| Field | Meaning |
|---|---|
| node_id | Stable or scoped identity for the neuron |
| domain_ids | Declared specialization domains |
| capability_profile | Processing and forwarding capabilities |
| forwarding_policy | Domains and traffic classes it may relay |
| peer_policy | Rules for accepting direct peers |
| lifecycle_state | Pending, active, dormant, quarantined, retired |
| policy_version | Version of the applicable domain/compatibility policy |
| owner_or_controller | Authority that approved participation, where applicable |

The descriptor should be authenticated in deployed systems. A self-asserted domain label is not sufficient evidence of authorization or capability.

## 4. Local state model

A neuron maintains bounded local state:

### 4.1 Direct peer table

Each entry describes a directly reachable peer:
- Peer identity.
- Accepted domain intersection or compatibility result.
- Advertised capabilities and forwarding permissions.
- Link/peer health.
- Authentication state.
- Last-seen time and expiry.
- Optional resource/load signal.

### 4.2 Route cache

A route entry may contain:
- Destination neuron or permitted destination scope.
- Domain and policy version.
- Next-hop peer.
- Route metric or preference.
- Hop estimate, if known.
- Expiry and validation state.
- Discovery provenance.

The cache stores next-hop information, not a mandatory complete end-to-end path. A route may be invalidated and rediscovered when the next hop fails or policy changes.

### 4.3 Resource limits

Implementations must set explicit bounds for:
- Direct peer count.
- Route-cache entries.
- Pending discovery requests.
- In-flight messages.
- Duplicate-detection records.
- Per-peer and per-domain forwarding rates.

No unbounded route learning or message buffering is permitted in the baseline profile.

## 5. Signal envelope

The conceptual envelope is:

```text
MNN-SIGNAL {
  protocol_version
  message_id
  origin_id
  destination_id_or_scope
  domain_id
  domain_policy_version
  payload_or_payload_reference
  integrity_and_authentication
  hop_limit
  expiry
  priority
  trace_or_provenance
}
```

The final encoding is intentionally unspecified. A compact binary format, structured object, or event representation may be selected after simulation.

### 5.1 Forwarding behavior

A relay:
1. Validates the envelope structure and integrity/authenticity requirements.
2. Checks message expiry and hop limit.
3. Checks the domain identifier against its forwarding policy.
4. Checks duplicate state.
5. Selects an eligible next hop from local state or initiates bounded discovery.
6. Decrements the hop limit and forwards the original signal envelope, preserving origin and message identity.
7. Records the forwarding event according to the configured provenance policy.

A pure relay must not alter the semantic payload. Any transformation creates a new derived event linked to the original message.

### 5.2 Loop and duplicate control

The baseline protocol uses:
- A finite hop limit.
- A unique message identifier.
- A bounded duplicate cache.
- Expiry timestamps or bounded lifetimes.
- Optional path-vector or recent-hop information where required by the chosen routing algorithm.

A node must not forward a message it has already processed within the active duplicate window. Duplicate suppression state must itself be bounded.

## 6. Domain compatibility

A domain policy defines which signal classes a node may process or relay. For the initial profile:
- Same-domain forwarding is permitted when peer and policy checks pass.
- Explicitly declared compatible subdomains may be permitted.
- Cross-domain forwarding is denied by default.
- Unknown domains and policy-version mismatches are rejected or held for policy resolution.

A future compatibility matrix may express permitted relationships between domains. It must be versioned and auditable. No compatibility should be inferred merely because two domains share a parent label.

## 7. Local route discovery

The initial design favors **bounded, domain-scoped discovery**.

When a destination is not in the local route cache:
1. The neuron checks whether the destination/domain is within its permitted forwarding scope.
2. It sends a discovery request only to eligible direct peers.
3. A peer processes the request locally and may answer from its own route cache or forward the request to eligible peers.
4. Discovery requests carry a finite hop limit, request identifier, domain, policy version, and expiry.
5. Duplicate requests are suppressed.
6. A valid response establishes a next-hop route with an expiry.
7. If discovery fails, the signal is reported as undeliverable or retained only within a bounded retry policy.

The protocol must not flood every domain indiscriminately. Later experiments should compare bounded flooding, expanding-ring discovery, gossip-based discovery, and proactive local advertisements.

## 8. New-neuron admission

### 8.1 Admission sequence

A new neuron enters through its relevant specialization domain:

1. **Provision:** create the new neuron's identity and descriptor.
2. **Authorize:** obtain the required owner/controller authorization.
3. **Request:** submit an admission request to the domain-local membership service or authorized local peers.
4. **Validate:** verify identity, policy version, domain claims, capability declarations, and admission rules.
5. **Attach:** establish direct peer relationships with selected compatible neighbors.
6. **Advertise locally:** make the new member discoverable within the relevant domain's local membership mechanism.
7. **Verify:** test bidirectional reachability and policy enforcement.
8. **Activate:** mark the neuron active for the permitted processing and forwarding roles.
9. **Record:** append the admission decision and connection changes to the provenance record.

### 8.2 Locality requirement

Unrelated domains do not need to update their membership tables simply because a neuron joined this domain. They may become aware of the change only through a separately authorized interface or a higher-level summary, if such an interface is later designed.

### 8.3 Registry design

The domain membership service is a logical role, not necessarily one central server. It may be:
- A small replicated registry scoped to one domain.
- A distributed membership protocol among authorized peers.
- A hybrid local registry with signed membership records.

The first simulation may use a simple registry to isolate routing behavior. Production design must examine registry failure, compromise, partition, and authority concentration.

## 9. Departure, failure, and quarantine

A neuron may leave because it is retired, dormant, unreachable, or quarantined.

The protocol should:
- Expire or invalidate routes through the departed node.
- Notify direct peers and the domain-local membership mechanism.
- Avoid requiring unrelated domains to rebuild state.
- Preserve provenance of the lifecycle change.
- Prevent quarantined nodes from continuing to forward new traffic.
- Define how in-flight messages are retried or failed.

A transient network partition must not automatically be interpreted as malicious behavior. Quarantine authority and automatic protective action require explicit policy.

## 10. Security and abuse considerations

Threats include:
- Domain impersonation.
- Unauthorized membership.
- Malicious route advertisements.
- Message replay and duplication.
- Routing loops and discovery storms.
- Selective dropping or modification.
- Resource exhaustion and congestion.
- Stale or poisoned route caches.
- Compromised relays observing metadata.
- Colluding nodes creating false reachability.

Required controls to evaluate include authenticated identities, signed or authenticated membership updates, integrity-protected messages, replay protection, hop limits, quotas, route validation, local audit records, and explicit owner-controlled policy.

Cryptographic mechanisms are not selected in this draft. They must align with HiveNet's existing identity and authorization specifications rather than inventing a conflicting security model.

## 11. Observability and provenance

Minimum experiment telemetry:
- Message ID and origin identity.
- Forwarding node identity.
- Domain and policy version.
- Selected next hop.
- Hop count.
- Forwarding outcome.
- Queue delay and route-discovery cost.
- Drop/reject reason.
- Any transformation or derived-message reference.

Telemetry should avoid recording semantic payloads by default. The experiment must distinguish operational metadata from content and document metadata leakage risks.

## 12. Protocol state transitions

Neuron lifecycle:

```text
PENDING -> AUTHORIZED -> ATTACHED -> ACTIVE
ACTIVE -> DORMANT
ACTIVE -> QUARANTINED
ACTIVE -> RETIRING -> RETIRED
QUARANTINED -> ACTIVE       (only after authorized review)
DORMANT -> ATTACHED -> ACTIVE
```

The exact transition authority and recovery rules remain to be specified.

## 13. Unresolved protocol choices

- Reactive discovery versus proactive advertisements versus hybrid.
- Exact route metric: hop count, latency, reliability, load, energy, or composite.
- How destination scopes are named and resolved.
- How overlapping domains and subdomain inheritance work.
- Whether local registries are replicated or peer-distributed.
- How route cache consistency is handled during rapid topology change.
- How much provenance is retained and where.
- How to handle multicast or one-to-many signal delivery.
- Whether relays can aggregate signals without violating identity preservation.

## 14. Status

This document is a protocol draft, not an implementation specification. It should not be used as a production networking protocol until message formats, authentication, authorization, failure semantics, resource bounds, and security review are complete.

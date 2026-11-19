# Mesh Neural Networking (MNN): Concept and Architecture

**Document type:** Architecture concept and research proposal  
**Status:** Proposed; not implemented or experimentally validated  
**Version:** 0.1  
**Date:** 2026-11-19  
**Origin:** Founder discussion, 2026-11-19  
**Program:** HiveNet neural systems and biodigital research

## 1. Executive summary

Mesh Neural Networking (MNN) proposes a neural-network communication architecture in which computational neurons retain their ordinary processing roles while also being eligible to relay and route signals for other neurons. The additional forwarding responsibility is constrained by functional specialization: a neuron forwards signals only within its assigned domain or an explicitly compatible domain. A mathematical-specialist neuron, for example, does not become a general-purpose language relay merely because it participates in the mesh.

Each neuron maintains **local awareness** of its immediate peers and the routes it has learned or cached. It does not need a complete map of the network. A neuron may forward a signal that originated at another neuron even when that signal was not originally addressed to the forwarding neuron. This is the feature that makes the proposal a genuine multi-hop mesh rather than simply a larger list of direct neural connections.

New neurons are introduced through the relevant specialization domain. The local domain recognizes and integrates the new member; unrelated domains need not be globally notified or reorganized. This is intended to support incremental growth while keeping membership and routing coordination local.

MNN is a proposed computational architecture. It is not a claim that biological neurons implement digital packet routing, nor a claim of demonstrated novelty. Existing neuromorphic systems already demonstrate distributed routing, local communication, hierarchical event routing, and decentralized synchronization. MNN's candidate contribution is the particular combination of forwarding-capable computational neurons, specialization-scoped forwarding, local-only routing knowledge, and domain-local admission.

## 2. Problem statement

Many neural and neuromorphic architectures distinguish computational elements from the communication infrastructure that transports signals between them. Other architectures encode communication through fixed or explicitly configured synaptic connections. These approaches can be effective, but they raise questions for a dynamically growing, specialization-aware network:

- Must every computational unit maintain broad or global connectivity knowledge?
- Can computational units themselves participate in forwarding signals generated elsewhere?
- Can forwarding be constrained by specialization rather than being unrestricted?
- Can a new unit be integrated locally without requiring network-wide membership updates?
- Can topology expand while preserving existing processing roles and bounded coordination?

MNN investigates these questions as a combined architecture.

## 3. Core architectural proposition

> A computational neuron may retain its primary processing function while also forwarding compatible signals originating from other neurons. It needs awareness of its local peers, not a complete network map. New neurons are admitted through their relevant specialization domain, allowing the rest of the network to continue operating without global reconfiguration.

The proposal separates three concerns:

1. **Computation:** the neuron's ordinary task-specific processing.
2. **Forwarding:** moving a signal onward without necessarily interpreting or recomputing it.
3. **Routing:** selecting an eligible next hop using local information and domain constraints.

These may be implemented as separate logical functions within one computational unit. A deployment may also use a shared communication substrate beneath many logical neurons; MNN does not require one physical network interface per mathematical neuron.

## 4. Functional specialization and domain boundaries

### 4.1 Specialization-scoped forwarding

Every neuron has one or more declared functional domains. A forwarding operation is permitted only when the signal's domain is compatible with the forwarding neuron's declared forwarding scope.

Illustrative domains include:
- Mathematics: arithmetic, algebra, geometry, statistics, calculus.
- Language: syntax, semantics, linguistic representations.
- Vision: visual features, spatial relations, object representations.

These examples are conceptual. Actual neural-network specialization may be distributed, overlapping, learned, or context-dependent rather than cleanly partitioned.

A neuron may belong to more than one domain, but multi-domain membership must be explicit. Compatibility should be represented by a versioned policy or compatibility relation, not inferred solely from a neuron label.

### 4.2 No implicit general-purpose relay

A mathematical neuron must not automatically forward language-domain traffic. Cross-domain forwarding is disabled in the initial MNN profile. Later research may examine explicit gateways or shared representations, but such mechanisms must be separately specified and evaluated.

### 4.3 Specialization is not semantic certainty

A domain label is an architectural routing constraint, not proof that a signal has been correctly classified. The design must account for ambiguous, mislabeled, mixed-domain, or adversarial signals. Unknown or incompatible traffic should be rejected, quarantined, or returned as unroutable rather than silently forwarded.

## 5. Local awareness and extended routing

Each neuron maintains a bounded local view containing, at minimum:
- Its own identity and declared domain membership.
- Directly connected eligible peers.
- The capabilities and current availability advertised by those peers.
- A small set of learned or cached next-hop routes, if used.
- Route expiry, health, and policy metadata.

A neuron may forward a signal from another origin through a sequence of compatible peers. It does not need to know every neuron in the domain or the complete end-to-end topology.

The architecture therefore distinguishes:
- **Direct connectivity:** a local peer relationship.
- **Extended reachability:** the ability to reach a more distant destination through one or more local peers.
- **Global topology knowledge:** a complete network map, which is not required by the MNN design.

Local awareness does not mean routing can operate without any route-discovery or maintenance traffic. The protocol must bound that traffic and avoid turning a local registry into a hidden global controller.

## 6. Domain-local neuron admission

When a new neuron is created or activated:

1. Its identity, specialization, capabilities, owner/policy authorization, and lifecycle state are established.
2. It requests admission to the relevant domain.
3. The domain's local membership mechanism validates the request.
4. Eligible local peers discover or are informed of the new member.
5. Local connections and route information are established or refreshed.
6. The new neuron becomes eligible for domain-scoped forwarding and processing according to its permissions.

Unrelated specialization domains are not required to receive a global topology update. A domain registry may coordinate local membership, but should not become an unrestricted central authority. The registry may be replicated or partitioned within a domain.

Admission must be explicit and auditable. Discovery is not authorization; capability is not permission; network reachability is not consent.

## 7. Logical architecture

MNN defines the following logical roles:

| Role | Responsibility |
|---|---|
| Processing function | Performs the neuron's ordinary computation |
| Relay function | Forwards an eligible signal without changing its semantic payload |
| Routing function | Selects a next hop using local state and domain policy |
| Local peer table | Records direct eligible neighbors |
| Domain membership service | Handles local admission, departure, and domain policy |
| Route cache | Stores bounded, expiring next-hop information |
| Signal envelope | Carries origin, destination/scope, domain, identity, integrity, and hop controls |

A single neuron may implement processing, relay, and routing functions. These are logical responsibilities and need not map one-to-one to physical hardware components.

## 8. Signal handling principles

Forwarding should preserve the origin and identity of the signal. A relay must not silently replace the source identity with its own or make forwarded information appear to have been independently generated.

The initial signal envelope should support:
- Unique message or event identifier.
- Origin identity.
- Destination identity or permitted destination scope.
- Domain identifier and compatibility-policy version.
- Payload or payload reference.
- Integrity/authenticity evidence appropriate to the deployment.
- Hop limit or time-to-live.
- Duplicate-detection information.
- Optional priority and expiry.
- Provenance of any transformation.

A pure relay forwards the payload unchanged. If a node transforms, filters, aggregates, or interprets the payload, that is a separate processing operation and must be recorded as such.

## 9. Resilience and bounded behavior

MNN should support alternate eligible paths where they exist, but must not assume that redundancy is free. Route discovery, retries, duplicate suppression, congestion, and failure recovery all consume resources.

Required safeguards include:
- Hop limits and loop prevention.
- Duplicate detection and bounded replay windows.
- Route expiry and stale-route invalidation.
- Backpressure or congestion handling.
- Rate limits for discovery and forwarding.
- Authentication and authorization of peers.
- Isolation of malformed or incompatible signals.
- Safe behavior when no eligible route exists.

A node's failure should not require global network reconstruction. Recovery should be local where possible, with broader coordination only when local alternatives are insufficient.

## 10. Relationship to earlier ANDNM work

MNN is a focused refinement within the broader Adaptive Neurogenesis and Dynamic Neural Mesh (ANDNM) research direction documented in [Neurogenesis and Adaptive Neural Mesh](01_NEUROGENESIS_AND_ADAPTIVE_NEURAL_MESH.md).

ANDNM considers dynamic creation, recruitment, connection, reconfiguration, and retirement of computational units. MNN narrows the communication question: how locally aware units can forward signals beyond their direct connections while respecting functional specialization and supporting localized admission.

MNN does not replace ANDNM. It provides a candidate communication architecture that ANDNM-style growth could use.

## 11. Relationship to HiveNet

MNN may eventually inform HiveNet's distributed AI and neural-system research. The analogy is architectural:
- MNN neuron: independently identifiable computational unit.
- MNN domain: specialization-scoped group of compatible units.
- MNN relay: bounded forwarding role.
- MNN route: local next-hop decision.
- MNN admission: controlled introduction of a new unit.

This does not mean that every HiveNet node is a neuron or that HiveNet's general-purpose network must enforce neural specialization rules. Any adoption into HiveNet requires a separate system-level design and threat model.

## 12. Research hypotheses

- **H1 — Local-state sufficiency:** A network using bounded local peer state and extended routing can deliver eligible signals without requiring every neuron to maintain a global topology map.
- **H2 — Domain isolation:** Specialization-scoped forwarding can reduce irrelevant cross-domain traffic compared with unrestricted forwarding.
- **H3 — Localized admission:** Adding a neuron to one domain can be completed without requiring unrelated domains to update their membership state.
- **H4 — Resilience:** Multiple eligible paths can improve delivery under node or link failure, subject to route overhead and topology.
- **H5 — Processing preservation:** Separating forwarding from semantic processing can preserve a neuron's primary task performance better than architectures that require every relay to interpret forwarded signals.

These are hypotheses, not established results.

## 13. Open design questions

1. Is domain membership assigned, learned, or jointly determined?
2. How should overlapping and hierarchical specializations be represented?
3. Should local routing use reactive discovery, proactive neighbor advertisements, or a hybrid?
4. What is the appropriate bound for peer tables and route caches?
5. How are routes authenticated and protected against malicious or faulty peers?
6. How should the system handle a valid signal whose destination is temporarily unreachable?
7. Can a neuron forward a signal while simultaneously performing its primary computation without unacceptable interference?
8. What hardware or runtime abstraction is appropriate when many logical neurons share one physical communication fabric?
9. How should domain-local registries be replicated without creating a single point of authority?
10. Under what conditions, if any, should explicit cross-domain gateways be allowed?

## 14. Scope exclusions for the first MNN profile

The initial profile does not require:
- Every neuron to connect directly to every other neuron.
- Every neuron to maintain a global network map.
- Unrestricted forwarding across all specializations.
- A full independent physical router per neuron.
- Automatic changes to model weights.
- Biological implementation or intervention.
- A central controller with authority over all domains.

## 15. Status and evidence

MNN is a founder-originated architectural proposal recorded on 2026-11-19. The architecture has not yet been implemented, simulated, benchmarked, or independently reviewed. Related research demonstrates important component techniques, but does not by itself establish MNN's exact combination or its performance.

The next step is a protocol-level specification and a controlled simulation comparing MNN against appropriate baselines.

# MNN Prior Art and Research Positioning

**Document type:** Preliminary literature review and research-positioning note  
**Status:** Initial source review; not an exhaustive literature or patent search  
**Version:** 0.1  
**Date:** 2026-11-19  
**Scope:** Neuromorphic routing, local coordination, hierarchical event routing, and specialization-aware neural communication

## 1. Purpose and caution

This note identifies established work close to parts of Mesh Neural Networking (MNN). It is intended to prevent overstatement of novelty and guide deeper research.

It is not a legal prior-art opinion, patentability assessment, freedom-to-operate review, or exhaustive systematic literature review. Search coverage is limited to the cited papers and their directly described architectures. Patent databases, citations, related work, open-source implementations, and additional academic databases still require review.

## 2. Preliminary findings

### 2.1 MOSAIC: in-memory computing and routing for small-world spike-based neuromorphic systems

Dalgaty et al. (2024) present MOSAIC, a neuromorphic architecture for small-world spiking neural networks. It uses distributed computing tiles and routing tiles, with local dense connectivity and globally sparse connections. The paper reports fabricated and experimentally demonstrated building blocks and evaluates routing efficiency.

**Overlap with MNN:**
- Distributed and decentralized communication.
- Local connectivity with longer-range routing.
- Small-world topology.
- Routing integrated into the neuromorphic system rather than relying only on a conventional centralized network.

**Difference from the current MNN proposal:**
- MOSAIC distinguishes analog computing tiles from routing tiles.
- Its routing is implemented through dedicated routing infrastructure and configurable crossbars.
- The MNN proposal makes each computational neuron logically eligible to relay signals originating from other neurons, subject to specialization and local peer rules.

MOSAIC is a close architectural precedent for local-plus-extended communication, but it does not establish the exact MNN combination.

Primary source:
- Dalgaty, T. et al. (2024). “Mosaic: in-memory computing and routing for small-world spike-based neuromorphic systems.” *Nature Communications*, 15, 142. https://doi.org/10.1038/s41467-023-44365-x
- Open full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC10761708/

### 2.2 NeuroScale: deterministic neuromorphic architecture with scalable time synchronization

Li, Imam, and Manohar (2025) present NeuroScale, a neuromorphic architecture using local, aperiodic synchronization without global coordination. Multiple cores communicate through a routing mesh. The paper evaluates hardware and simulation behavior and compares its approach with global barrier synchronization in TrueNorth and Loihi.

**Overlap with MNN:**
- Local coordination rather than mandatory global synchronization.
- Distributed event-driven communication.
- Routing mesh between computational regions.
- Explicit attention to scaling and communication overhead.

**Difference from the current MNN proposal:**
- NeuroScale's synchronization and routing operate at the core/network-on-chip level.
- Its paper describes neurons within a core sharing a synchronization unit; it does not describe every individual neuron acting as a general multi-hop relay for other neurons' signals.
- It does not define the MNN proposal's specialization-scoped forwarding and domain-local neuron admission as a combined protocol.

NeuroScale is highly relevant to MNN's locality and coordination principles. It should be studied before implementing MNN, especially for deadlock avoidance, buffering, asynchronous progress, and bounded local synchronization.

Primary source:
- Li, C., Imam, N., and Manohar, R. (2025). “A deterministic neuromorphic architecture with scalable time synchronization.” *Nature Communications*, 16, 10329. Published 24 November 2025. https://doi.org/10.1038/s41467-025-65268-z
- Open full text: https://pmc.ncbi.nlm.nih.gov/articles/PMC12645053/

### 2.3 HiAER: Hierarchical Address Event Routing

Park et al. (2017; first published online in 2016) present a hierarchical address-event routing architecture for scalable communication of neural and synaptic spike events across neuromorphic processors. It uses nested routing levels and demonstrates a multi-chip/multi-board system serving approximately 262,000 neurons and 262 million synapses.

**Overlap with MNN:**
- Multi-hop or hierarchical event routing.
- Routing across increasing spatial scales.
- Explicit treatment of neural event communication as a scalable network problem.

**Difference from the current MNN proposal:**
- HiAER focuses on routing infrastructure between neuromorphic processors.
- It does not establish that each computational neuron itself forwards arbitrary compatible signals from other neurons using only local peer awareness.
- The MNN specialization-boundary and localized admission requirements are not its stated contribution.

Primary sources:
- Park, J. et al. (2017). “Hierarchical Address Event Routing for Reconfigurable Large-Scale Neuromorphic Systems.” *IEEE Transactions on Neural Networks and Learning Systems*, 28(10), 2408–2422. https://doi.org/10.1109/TNNLS.2016.2572164
- PubMed: https://pubmed.ncbi.nlm.nih.gov/27483491/

## 3. Related fields requiring further review

The following fields may contain additional close precedents and should be investigated before any novelty claim:

1. **Address-Event Representation (AER):** event-based communication and routing for spiking neural systems.
2. **Network-on-Chip (NoC):** local routers, distributed routing, virtual channels, deadlock avoidance, and hierarchical interconnects.
3. **Graph neural networks:** message passing, neighborhood aggregation, sparse graph topology, and dynamic graph updates. Many GNNs treat message passing as computation over graph edges rather than independent packet forwarding, but the boundary should be reviewed carefully.
4. **Mixture-of-experts and modular neural networks:** specialization, expert selection, gating, and sparse activation. These may inform domain compatibility but do not necessarily implement multi-hop relay networks.
5. **Small-world and modular networks:** local clustering combined with sparse long-range links.
6. **Distributed systems and overlay routing:** local route state, neighbor discovery, gossip, route caches, loop prevention, and incremental membership.
7. **Self-organizing and adaptive networks:** topology adaptation, distributed discovery, and local rewiring.
8. **Neuromorphic hardware and spiking neural networks:** neuron, synapse, axon, dendrite, and routing co-design.

## 4. Preliminary comparison

| Feature | MOSAIC | NeuroScale | HiAER | MNN proposal |
|---|---|---|---|---|
| Neuromorphic/neural context | Yes | Yes | Yes | Computational neural architecture; hardware target open |
| Distributed routing | Yes | Yes | Yes | Proposed |
| Local communication/coordination | Yes | Yes | Hierarchical | Core requirement |
| Multi-hop or extended reach | Yes | Yes | Yes | Core requirement |
| Computational neurons themselves relay others' signals | Not established; separate routing tiles | Not established at individual-neuron level | Not established; routing infrastructure | Proposed |
| Specialization-scoped forwarding | Not identified as core mechanism | Not identified as core mechanism | Not identified as core mechanism | Core requirement |
| Domain-local neuron admission | Not identified as core mechanism | Not identified as core mechanism | Not identified as core mechanism | Core requirement |
| No global topology map per neuron | Localized architecture | Local coordination; core-level routing | Hierarchical routing | Core requirement |

“Not identified” means the feature is not established by the reviewed paper's described contribution; it is not proof that no related implementation or extension exists.

## 5. Candidate MNN research contribution

Based on this limited review, MNN should not be positioned as the invention of distributed neural routing, local communication, hierarchical event routing, or decentralized neuromorphic coordination. Those areas have substantial prior work.

The candidate contribution to investigate is the combination of:

1. Computational neurons retain their primary processing role and may also act as relays/routers.
2. A neuron may forward a signal originating at another neuron without necessarily interpreting the payload.
3. Forwarding is restricted to declared functional specializations or explicitly compatible domains.
4. Each neuron uses local peer awareness and bounded next-hop knowledge rather than a global topology map.
5. A new neuron is introduced through its relevant domain, avoiding mandatory network-wide membership reconfiguration.
6. The architecture is evaluated for processing interference, communication cost, domain isolation, incremental admission, and fault tolerance.

This combination is a research hypothesis about architectural differentiation, not a verified novelty claim.

## 6. Questions for the next literature and patent review

- Do any existing systems explicitly make each computational neuron a multi-hop forwarding participant?
- Are there systems where a neuron forwards another neuron's event without performing semantic integration?
- Have domain- or type-constrained routing rules been applied to neural event meshes?
- Are there distributed graph systems with specialization-local membership updates and no global topology synchronization?
- Do neuromorphic hardware patents cover compute elements that also route other compute elements' events?
- How do MOSAIC, NeuroScale, HiAER, SpiNNaker, Loihi, and related systems represent identity, routing tables, and dynamic membership?
- Can MNN's requirements be implemented using existing AER/NoC mechanisms without a new architecture?
- What is the measurable advantage, if any, over separate compute and router elements?

## 7. Recommended positioning

Use this careful description in future research summaries:

> MNN is a proposed specialization-aware neural communication architecture exploring how computational neurons can also participate in multi-hop signal forwarding while retaining local peer awareness. It builds on established work in neuromorphic routing, small-world connectivity, and decentralized coordination. Its proposed differentiators—domain-constrained forwarding, forwarding of signals originating elsewhere, and domain-local admission of new neurons—require formal specification, systematic prior-art review, and experimental validation.

Do not claim “first,” “unique,” “unprecedented,” or “patentable” on the basis of this preliminary review.

## 8. References

1. Dalgaty, T., Moro, F., Demirağ, Y., De Pra, A., Indiveri, G., Vianello, E., and Payvand, M. (2024). “Mosaic: in-memory computing and routing for small-world spike-based neuromorphic systems.” *Nature Communications*, 15, 142. https://doi.org/10.1038/s41467-023-44365-x
2. Li, C., Imam, N., and Manohar, R. (2025). “A deterministic neuromorphic architecture with scalable time synchronization.” *Nature Communications*, 16, 10329. https://doi.org/10.1038/s41467-025-65268-z
3. Park, J. et al. (2017). “Hierarchical Address Event Routing for Reconfigurable Large-Scale Neuromorphic Systems.” *IEEE Transactions on Neural Networks and Learning Systems*, 28(10), 2408–2422. https://doi.org/10.1109/TNNLS.2016.2572164

## 9. Review status

This is an initial, source-backed positioning note based on three primary research directions. It is not exhaustive. The next review should inspect the cited papers' related-work sections and references, then search academic indexes, patents, and implementation repositories using the specific differentiators in Section 5.

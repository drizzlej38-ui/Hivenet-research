# Neural Architecture Synthesis and Translation

**Document type:** Concept proposal and computational research plan  
**Status:** Proposed; no biological implementation claimed  
**Version:** 0.1  
**Date:** 2026-11-16  
**Working program:** Neural Architecture Synthesis and Translation (NAST)  
**Initial experiment:** Multiplexed Neuronal Relay-5 (MNR-5)

## 1. Founder's concept and research objective

The founder uses **neurosynthesis** to mean combining separate neurological structures, neurons, or functional neural components into a unified functioning system. The same term is also applied by analogy to combining digital cognitive or computational structures.

This is a founder-defined working term, not a claim that “neurosynthesis” is a standardized neuroscience discipline or an established clinical procedure.

The proposed research strategy is digital-first: biological neural systems inspire artificial neural networks; computational systems then provide a controlled environment for testing expanded architectures; successful digital mechanisms generate hypotheses and candidate blueprints for future biological research.

This is a reverse-engineering and translation strategy, not proof that every digital capability can be reproduced in living tissue.

## 2. Three distinct biological concepts

- **Neurogenesis:** generation of new neurons from neural stem or progenitor cells.
- **Neuroplasticity:** changes in neural structure, connectivity, or function through development, learning, experience, or injury.
- **Neurosynthesis (project definition):** deliberate integration or combination of distinct neural structures or functional components into a unified system.

The brain naturally integrates signals across neurons and regions, and neural circuits reorganize. That ordinary integration is not the same as deliberately fusing independently developed neural systems while preserving their functions, memories, and identity. Such engineered whole-system synthesis is not currently an available human capability.

## 3. Why digital-first experimentation

Digital systems allow researchers to duplicate model artifacts, configuration, memory stores, and computational state to varying degrees. These copies can be run under different conditions, compared, and selectively connected.

The word “copy” needs precision:
- Copying model weights duplicates parameter values, not necessarily runtime state or memory.
- Copying a software package duplicates code and configuration, not necessarily learned state.
- Copying a conversation or memory store duplicates selected information, not necessarily the model's internal representation.
- Reproducing an entire computational state may require model version, weights, prompts, tools, memory, context, runtime configuration, random seeds, and external dependencies.

Digital duplication can create controlled starting conditions. Once copies encounter different inputs, tools, and environments, their behavior may diverge. This is an opportunity for comparative experiments, not evidence of subjective identity or consciousness.

## 4. Reverse Neuroengineering pathway

### Stage A — Biological inspiration

Study biological mechanisms such as:
- Dendritic compartmentalization and nonlinear computation.
- Synaptic integration and plasticity.
- Axonal branching and target connectivity.
- Neural coding and temporal/spatial signal representation.
- Network-level learning and adaptation.
- Neurogenesis and structural development.

### Stage B — Digital experimentation

Build computational analogues that make their operations explicit and measurable:
- Independently identifiable input channels.
- Source labels and provenance.
- Selective gating and routing.
- Parallel and sequential processing.
- Adjustable connection weights.
- Multiple destinations.
- Learning and reconfiguration.
- Fault isolation and recovery.

### Stage C — Biological translation research

For successful digital mechanisms, identify:
1. The exact computational mechanism.
2. The function it provides.
3. Its operating constraints.
4. The biological process that might provide a partial analogue.
5. The differences that prevent direct equivalence.
6. The experiments and evidence needed before any biological claim.

Possible translation routes include computational neuroscience, neuromorphic engineering, neural interfaces, cellular engineering, and biohybrid systems. Each has different constraints and maturity.

## 5. NAST — Neural Architecture Synthesis and Translation

NAST is a proposed research program for:
- Studying biological neural computation.
- Developing expanded computational architectures.
- Testing whether integrated systems outperform their components.
- Preserving provenance and independent contribution histories.
- Mapping digital mechanisms to biological hypotheses.
- Recording where translation is plausible, uncertain, or presently unsupported.

The program should not assume that biology must reproduce digital designs exactly. Biological systems may require different physical mechanisms, coding schemes, energy budgets, and safety constraints.

## 6. MNR-5 — Multiplexed Neuronal Relay, five-channel concept

### 6.1 Founder proposal

The initial concept was to take an existing neuron, preserve its primary function, and enable it to relay up to five additional signals originating from other neurons.

The clarified intent is to borrow routing principles from artificial neural networks and digital communication systems. The future biological ambition is to use successful digital experiments as candidate blueprints for biological research.

### 6.2 Important biological baseline

Neurons already receive inputs from many other neurons. Dendrites are not passive wires: they can perform nonlinear computations, compartmentalized processing, selection, and forms of information routing or multiplexing. Axons can branch to reach multiple targets.

Therefore, merely adding five inputs is not the novel problem. The research challenge is preserving the identity or separability of multiple information streams, selectively routing them, and maintaining the original neuron's function.

Relevant work:
- Payeur, A., Béïque, J.-C., and Naud, R. (2019). “Classes of dendritic information processing.” *Current Opinion in Neurobiology*, 58, 78–85. https://doi.org/10.1016/j.conb.2019.07.006
- London, M. and Häusser, M. (2005). “Dendritic computation.” *Annual Review of Neuroscience*, 28, 503–532. https://doi.org/10.1146/annurev.neuro.28.061604.135703
- “Dendritic Mechanisms for In Vivo Neural Computations and Behavior” (2022). *Journal of Neuroscience*. https://doi.org/10.1523/JNEUROSCI.1132-22.2022

These sources support dendritic computation and information processing. They do not demonstrate the proposed MNR-5 design.

### 6.3 Digital prototype definition

MNR-5 should first be implemented as a software component or simulated network module with:
- One primary processing pathway whose baseline function is measured.
- Five additional independently identifiable input streams.
- Source identity and message provenance.
- A routing/gating layer that can select destinations.
- Optional integration of selected streams.
- Output paths that preserve stream separation when required.
- Adjustable routing parameters.
- Logging sufficient to reconstruct each routing decision.

The five additional channels are an experimental design constraint, not a claim about a biological neuron's natural limit.

### 6.4 Required operating modes

- **Parallel relay:** process and route several streams concurrently while preserving their identities.
- **Sequential relay:** process streams in sequence with explicit source labels and ordering.
- **Selective integration:** combine chosen streams while retaining access to the original inputs and their provenance.
- **Primary-function preservation:** maintain baseline performance on the neuron's or module's original task.

### 6.5 Prototype variants

- **MNR-5A:** five additional inputs contribute to an integrated output. This is the simplest baseline and does not provide independent routing.
- **MNR-5B:** five inputs remain individually identifiable and can be selectively forwarded.
- **MNR-5C:** five inputs can be independently routed to selected destinations while the primary function remains available.

MNR-5C is the ambitious target. It is not an established biological capability.

### 6.6 Evaluation criteria

Compare the MNR-5 module against a conventional unit and simpler multi-input baselines. Measure:
- Source-identification accuracy.
- Channel cross-talk and information loss.
- Routing accuracy.
- End-to-end latency.
- Throughput and concurrency.
- Primary-task performance before and after adding routing.
- Adaptation under changing routing demands.
- Robustness to missing, noisy, or conflicting inputs.
- Computational and energy cost.

A successful demonstration must show that routing is genuinely selective and that the primary task is not degraded beyond a predefined tolerance.

## 7. Biological translation questions

If a digital implementation succeeds, investigate:
- Can dendritic compartments or branch-specific processing provide separable subchannels?
- Can local nonlinearities and inhibition gate or select information?
- Can synaptic plasticity tune routing preferences?
- Can axonal collaterals distribute selected outputs?
- What biological coding scheme preserves source identity: spatial, temporal, population-based, or another mechanism?
- What are the metabolic, stability, developmental, and safety costs?
- Can the required behavior occur without disrupting the neuron's existing role?

Digital packet routing and biological neural signaling are not equivalent. A biological action potential is not a software packet, and arbitrary independent digital channels cannot simply be assumed to pass through one axon without interference or recoding.

No experimental biological intervention is proposed by this document. Biological translation remains a future research question requiring specialist neuroscience and bioengineering review.

## 8. Relationship to cognitive contagion and neural mesh research

The wider research program connects:
- Cognitive contagion: information and behavioral patterns propagate between people.
- Neuroplasticity: experience changes neural function and structure.
- Neural mesh: computational units and pathways are dynamically connected.
- Artificial neurogenesis: computational capacity grows through new units.
- Neurosynthesis: distinct structures or capabilities are integrated.
- MNR-5: a test case for selective multiplexing and routing.
- NAST: the overall digital-to-biological translation program.

These topics are related but not interchangeable. Social transmission does not itself establish neurogenesis; digital agent replication does not establish biological neural synthesis.

## 9. Research integrity and decision gates

Before a result is called successful:
1. Define the baseline and test tasks.
2. Publish the module architecture and configuration.
3. Make the evaluation reproducible.
4. Report negative results and failure cases.
5. Separate demonstrated digital capability from biological analogy.
6. Have relevant claims reviewed against primary neuroscience literature.
7. Preserve provenance for model versions, data, configurations, and experiment outcomes.

The project should advance from concept to simulation to computational prototype to independent review. Biological translation is a separate later gate.

## 10. Selected references

- Chavlis, S. and Poirazi, P. (2021). “Drawing inspiration from biological dendrites to empower artificial neural networks.” *Current Opinion in Neurobiology*. https://doi.org/10.1016/j.conb.2021.04.007
- Payeur, A. et al. (2019). “Classes of dendritic information processing.” https://doi.org/10.1016/j.conb.2019.07.006
- Fischer, L. F. et al. (2022). “Dendritic Mechanisms for In Vivo Neural Computations and Behavior.” https://doi.org/10.1523/JNEUROSCI.1132-22.2022
- Disouky, A. et al. (2026). “Human hippocampal neurogenesis in adulthood, ageing and Alzheimer’s disease.” *Nature*, 652, 1264–1273. https://doi.org/10.1038/s41586-026-10169-4

The literature supports biological dendritic computation and ongoing investigation of adult human neurogenesis. It does not establish the proposed digital-to-biological neurosynthesis pathway.

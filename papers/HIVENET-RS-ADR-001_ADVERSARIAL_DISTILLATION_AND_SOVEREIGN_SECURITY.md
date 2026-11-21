# Adversarial Distillation and Sovereign Multi-Model Security

**Document ID:** HIVENET-RS-ADR-001  
**Status:** Research proposal / architecture decision candidate  
**Created:** 2026-11-20  
**Decision authority:** Founder review required

## Problem

A multi-model system can expose useful capabilities through ordinary outputs, reasoning summaries, tool interactions, and other observable behavior. Those outputs can be collected and used to train another model. The resulting model may acquire capabilities without inheriting the original model's safeguards.

OpenAI's 2026-11-20 article, *Combatting adversarial distillation*, describes this risk and a layered response: model training, input/output classifiers, API-level controls, adaptive red-teaming, campaign detection, and coordinated enforcement.

Source: https://openai.com/index/combatting-adversarial-distillation/

This threat is relevant to HiveNet, but the response must remain consistent with local-first operation, human authority, privacy, and opt-in collaboration.

## Distinguish the threat classes

| Threat class | Mechanism | Primary security concern |
|---|---|---|
| Adversarial distillation | Collecting model outputs, reasoning traces, judgments, or tool interactions to train a student | Capability transfer without equivalent safeguards |
| Protected-reasoning extraction | Inducing a service to disclose internal reasoning not intended for release | Confidentiality and unintended capability transfer |
| Weight-space programming | Directly inspecting or modifying model parameters when weight artifacts are accessible | Backdoors, sabotage, unauthorized capability changes |
| Artifact supply-chain compromise | Substituting or altering model files, adapters, or checkpoints | Integrity, provenance, and runtime trust |

These categories overlap in their consequences but are not the same technical attack. OpenAI's article principally addresses output/reasoning extraction and campaign-level abuse. Weight-space programming is treated separately in [HIVENET-RS-WSP-001](../research/weight-space-security/HIVENET-RS-WSP-001_WEIGHT_SPACE_SECURITY.md).

## Design position

HiveNet should not rely on secrecy of prompts, model reputation, or one provider's safeguards as its security boundary. It should establish explicit controls over what information and artifacts are shared, with whom, for what purpose, and under whose authority.

### Proposed requirements

1. **Data-class separation:** Distinguish user-visible answers, authored explanations, tool-call records, internal/private reasoning (where exposed by a provider), model artifacts, and human-authored research.
2. **Minimum necessary disclosure:** Share only the information required for an authorized task.
3. **Session and provenance binding:** Preserve source, session, model, and authorization context for messages and artifacts where technically available.
4. **No assumed portability:** Do not assume protected reasoning, hidden state, or provider-internal artifacts are available for export or reuse.
5. **Cross-model boundary controls:** Do not automatically forward private reasoning or sensitive context from one model/provider to another.
6. **Tool-call inspection:** Treat tool arguments and outputs as data-transfer surfaces, not merely implementation details.
7. **Campaign-aware abuse monitoring:** Where HiveNet provides shared gateways, allow opt-in detection of coordinated extraction patterns using privacy-minimizing operational metadata. Do not inspect user semantic content by default.
8. **Regression corpus:** Preserve successful extraction attempts and defensive test cases as controlled regression material, subject to privacy, provider terms, and lawful access.
9. **Independent review:** No model is the sole authority for validating another model's security claims.
10. **Human authority:** The owner decides what to share, retain, export, or revoke. Automated enforcement must remain bounded, explainable, and reviewable.

## OpenAI-reported evidence

OpenAI reports that, in its internal adaptive black-box evaluation, extraction success for protected reasoning from an earlier request fell from 54.0% on GPT-6 Astra with original safeguards to 0.2% on GPT-6.2 Astra with updated safeguards. For current-request extraction, it reports a decline from 22.9% to 0.9%. These are OpenAI's internal results, aggregated across six attacker models; they are not independent benchmarks.

OpenAI also reports that exact reasoning trajectories transferred more cybersecurity capability to student models than reasoning summaries in its tested training setup. The result supports treating reasoning traces and tool interactions as potentially capability-bearing data, even for otherwise permitted defensive tasks.

Source: https://openai.com/index/combatting-adversarial-distillation/

## HiveNet-specific constraints

- Preserve offline-first and local-first operation.
- Do not create a central authority or mandatory central telemetry service.
- Do not transmit prompts, outputs, metadata, or model artifacts without explicit owner authorization.
- Keep user semantic content outside security telemetry by default.
- Use append-only, human-readable audit records where appropriate; ENDCAP is a candidate archival mechanism, not presumed to be fully integrated or proven.
- Treat model-provider restrictions as external constraints, not as a replacement for HiveNet's own governance.
- Keep security policy, technical enforcement, and human authorization distinct.

## Research questions

1. How can HiveNet prevent accidental cross-provider disclosure of sensitive context?
2. What metadata is sufficient for abuse detection without collecting semantic content?
3. How should task routing represent data sensitivity and allowed recipients?
4. How can a node distinguish user-authorized collaboration from unauthorized bulk extraction?
5. Which regression tests can safely reproduce known extraction attempts?
6. How should the network exchange threat indicators without exposing private user data?
7. How do these controls interact with WSP and model-artifact admission?

## Proposed decision

Adopt adversarial distillation and capability extraction as explicit HiveNet threat-model categories. Require data-class separation, least-disclosure routing, session/provenance context, and human-authorized sharing in future specifications. Treat implementation details and thresholds as open research pending threat modeling and founder approval.

## References

- OpenAI, [Combatting adversarial distillation](https://openai.com/index/combatting-adversarial-distillation/), 2026-11-20.
- Wang, Lu, and Li, [Can LLMs Write Backdoors? An Empirical Security Study of Weight-Space Programming](https://arxiv.org/abs/2611.17395), 2026-11-12.
- Goworek et al., [Replicating and Extending Weight-Space Programming: Frontier LLMs Compile Programs into Weights and Read Input Layers](https://arxiv.org/abs/2611.21449), 2026-11-16.
- [HIVENET-RS-WSP-001 — Weight-Space Programming and Model Integrity](../research/weight-space-security/HIVENET-RS-WSP-001_WEIGHT_SPACE_SECURITY.md)

---

**Status note:** This is a research proposal. It does not claim the controls are implemented, validated, or approved.

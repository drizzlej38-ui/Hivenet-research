# Weight-Space Programming, Model Integrity, and Neural Network Security

**Document ID:** HIVENET-RS-WSP-001  
**Status:** Research direction / literature review (not an implemented control)  
**Created:** 2026-11-20  
**Owner authority:** Founder review required  
**Scope:** HiveNet model admission, model artifacts, adapters, checkpoints, and any future weight-editing workflow

## Executive position

Weight-space programming (WSP) creates a security requirement for any ecosystem that accepts, modifies, distributes, or executes externally supplied model artifacts. HiveNet must treat model-integrity assessment as a mandatory admission and lifecycle control, not an optional enhancement.

This requirement is distinct from (but complementary to) defenses against adversarial distillation. Adversarial distillation can transfer capability through model outputs, reasoning traces, judgments, and tool interactions without obtaining model weights. WSP concerns direct inspection or modification of parameters when an actor has access to the relevant weight artifacts. These attack surfaces must not be conflated.

## Evidence and source boundaries

### OpenAI: adversarial distillation

OpenAI's 2026-11-20 article describes unauthorized extraction of capabilities through model outputs and protected reasoning. It reports layered defenses involving adversarial training, input/output classifiers, API controls, campaign detection, and enforcement. Its Astra evaluations concern extraction of protected reasoning through interactions; the article is not itself evidence of direct weight-space editing.

Source: [OpenAI, Combatting adversarial distillation](https://openai.com/index/combatting-adversarial-distillation/).

### Weight-space programming and backdoor injection

Wang, Lu, and Li, *Can LLMs Write Backdoors? An Empirical Security Study of Weight-Space Programming* (arXiv:2611.17395, 2026-11-12), report experiments in which LLMs directly modified target model weights from natural-language objectives. Their tested targets included an MLP, ResNet-18, and Qwen2.5-0.5B-Instruct. They report backdoor insertion with largely preserved clean-task performance; among the five tested editors, GPT-6 Astra was the only one reported to succeed across all three target architectures.

Source: [arXiv:2611.17395](https://arxiv.org/abs/2611.17395).

This is a preprint and an experimental result within the tested setup. It does not establish that Astra can modify arbitrary models, access remote weights without authorization, or perform such operations through an ordinary hosted inference interface.

### Weight writing, reading, and limited auditing

Goworek, Hickey, Nanni, and O'Reilly, *Replicating and Extending Weight-Space Programming: Frontier LLMs Compile Programs into Weights and Read Input Layers* (arXiv:2611.21449, 2026-11-16), report replication and extensions involving small networks. Their preliminary findings include successful network construction for particular tasks, partial interpretation of network weights, and limited weight-only identification of poisoned models/adapters. The authors characterize weight-only auditing as shallow: in their reported tests it did not recover the trigger or explain the malicious behavior.

Source: [arXiv:2611.21449](https://arxiv.org/abs/2611.21449).

These results are preliminary and bounded by the tested models, artifacts, tasks, and procedures. Weight inspection must not be treated as a substitute for executing behavioral evaluations.

## Terminology

- **Model artifact:** A checkpoint, weight file, tokenizer, configuration, adapter, quantization package, or other material needed to reconstruct or modify a model.
- **Weight-space programming (WSP):** Direct interpretation or modification of model parameters by an LLM or other programmatic process.
- **Weight-space attack:** Unauthorized or malicious parameter modification, including backdoor insertion, capability alteration, or sabotage.
- **Artifact provenance:** Evidence describing origin, authorship or publisher, version, transformation history, and custody of an artifact.
- **Integrity verification:** Evidence that the artifact bytes match a declared reference. A cryptographic hash proves byte identity relative to a trusted digest; it does not prove the artifact is benign.
- **Behavioral verification:** Testing the model's actual behavior under clean, adversarial, and task-specific inputs.
- **Admission:** The owner-authorized decision to permit an artifact into a HiveNet model registry or execution pool.

## Threat model

HiveNet must account for at least the following risks:

1. **Backdoored contribution:** A model, adapter, or checkpoint contains a trigger-dependent behavior while retaining apparently normal performance on ordinary inputs.
2. **Supply-chain substitution:** An artifact is replaced between publication, download, review, and deployment.
3. **Unauthorized modification:** A local process, contributor, plugin, or compromised node changes model parameters after approval.
4. **Malicious adapter or delta:** A small adapter or parameter delta alters behavior while the base model remains unchanged.
5. **Model sabotage:** Parameters are altered to degrade reliability, suppress selected capabilities, or induce targeted failure.
6. **False assurance:** A clean hash, signature, reputation score, model-generated audit, or ordinary benchmark result is incorrectly treated as proof of safety.
7. **Auditor compromise or collusion:** The model performing the audit is itself compromised, manipulated, or insufficiently capable.
8. **Execution-time substitution:** The verified artifact is not the artifact actually loaded by the inference runtime.

Threat actors may include malicious contributors, compromised distribution channels, compromised nodes, malicious insiders, or accidental processes. The design must also handle benign but unreviewed modifications.

## Mandatory architectural requirements

The following are proposed baseline requirements for model-bearing HiveNet nodes. They become binding implementation requirements only after founder approval and technical specification.

### WSP-REQ-01 — No unverified artifact admission

No externally sourced or modified model artifact may enter the trusted model registry or production execution pool until the node owner has authorized admission and the required checks have completed.

### WSP-REQ-02 — Provenance and custody record

Record, where available:
- Origin and publisher identity.
- Model name, version, architecture, and declared license.
- Source URL or repository and immutable revision.
- Artifact filenames, sizes, and cryptographic digests.
- Signatures and signer identity, when available.
- Download, transfer, conversion, quantization, adapter, and modification events.
- Tool versions and operator/owner authorization for each transformation.
- Verification results, limitations, and unresolved anomalies.

Do not represent missing provenance as verified provenance.

### WSP-REQ-03 — Cryptographic integrity is necessary but insufficient

Verify artifact digests against a trusted, independently obtained reference where one exists. Verify signatures where the signing key and trust chain are meaningful. A digest alone establishes only that bytes match a particular digest; it does not establish that the source is trustworthy or that the model is safe.

### WSP-REQ-04 — Isolated inspection and execution

Inspect and test untrusted artifacts in a resource-limited environment isolated from owner secrets, production credentials, and unrestricted network access. Do not load untrusted model code or custom runtime extensions in a privileged environment.

### WSP-REQ-05 — Independent behavioral evaluation

Weight-only inspection may be used as one signal, but it must be combined with behavioral testing. Include baseline task performance, targeted trigger probes where appropriate, distribution-shift tests, safety tests, and regression suites. Record test coverage and known blind spots.

### WSP-REQ-06 — Independent verification

The model that edits, packages, or proposes a change must not be the sole authority that certifies that change. Use independent tools, reproducible measurements, and where feasible a separate model or reviewer. Model consensus is not cryptographic proof and does not replace owner approval.

### WSP-REQ-07 — Immutable admission record

Preserve an append-only, human-readable record of the exact artifact digest admitted, provenance evidence, test suite/version, results, exceptions, and approving authority. ENDCAP is a candidate record layer, subject to its own security and implementation status.

### WSP-REQ-08 — Runtime-to-artifact binding

At load time, verify that the artifact being executed is the artifact that passed admission. Detect and record post-admission changes. A model update, adapter change, quantization change, or conversion creates a new artifact identity and requires reassessment proportional to the change.

### WSP-REQ-09 — Quarantine and rollback

If integrity checks fail, provenance becomes inconsistent, or suspicious behavior is detected, prevent automatic promotion, quarantine the artifact, preserve evidence, and require owner-authorized disposition. Preserve a known-good rollback artifact where feasible.

### WSP-REQ-10 — Owner authority and consent

No model, node, or remote coordinator may silently replace, edit, admit, or revoke another owner's model artifacts. The owner or explicitly delegated custodian retains final authority.

## Proposed model-artifact lifecycle

1. **Acquire:** Download or receive into an untrusted staging area.
2. **Identify:** Record source, version, format, architecture, and artifact digests.
3. **Verify provenance:** Check signatures and publisher references where available.
4. **Inspect:** Examine metadata, configuration, code dependencies, adapters, and weight deltas.
5. **Test:** Run isolated static and behavioral checks; document limits.
6. **Review:** Obtain independent assessment for high-risk or high-impact models.
7. **Authorize:** Owner approves or rejects admission.
8. **Bind:** Register exact artifact digests and runtime identity.
9. **Monitor:** Detect changes, anomalous behavior, and unexpected dependencies.
10. **Reassess:** Repeat appropriate checks after any update or modification.
11. **Quarantine/retire:** Preserve evidence and revoke trust when required.

## Research and evaluation plan

### RQ-1 — Detection limits

How well can weight-only analysis identify known poisoned checkpoints and adapters? Measure false positives, false negatives, and sensitivity to architecture, scale, quantization, and format.

### RQ-2 — Behavioral complementarity

Which behavioral tests detect compromises that weight-only inspection misses? Establish a reproducible suite and explicitly record untested trigger spaces.

### RQ-3 — Artifact provenance

What signed manifests, transparency logs, reproducible builds, and custody records can be used on constrained local-first nodes?

### RQ-4 — Adapter and delta security

Can small adapters or parameter deltas introduce behavior not visible from base-model review? Define independent evaluation and lineage tracking for derivative artifacts.

### RQ-5 — Runtime binding

Can the node prove that the loaded artifact matches the artifact admitted? Evaluate filesystem permissions, immutable storage options, runtime measurements, and process isolation.

### RQ-6 — WSP-assisted defensive auditing

Can Astra or other models assist with weight interpretation and anomaly triage without becoming the sole security authority? Test against known benign and poisoned artifacts, blind holdouts, and independent behavioral ground truth.

### RQ-7 — Capability and access boundaries

What controls are needed when a model is allowed to inspect or edit weights? Separate read access, write access, staging, test execution, registry admission, and production deployment into distinct permissions.

## Initial acceptance criteria for future implementation

A model-artifact admission prototype should not be considered complete until it can:
- Produce a machine-readable and human-readable artifact manifest.
- Verify and record digests.
- Keep incoming artifacts quarantined before approval.
- Run tests without production secrets or unrestricted network access.
- Record behavioral test results and limitations.
- Bind the approved digest to the runtime-loaded artifact.
- Detect a post-approval artifact change.
- Preserve an append-only admission and disposition history.
- Require explicit owner approval for promotion and rollback.

These are proposed criteria, not claims that the current HiveNet or ENDCAP implementations already provide them.

## Open questions and cautions

- A model's ability to write a small network's weights is not equivalent to the ability to edit its own weights or arbitrary frontier-model checkpoints.
- A model that identifies suspicious weights is not necessarily able to explain the behavior or discover every backdoor.
- Hashes and signatures authenticate bytes or signers relative to trust anchors; they do not certify benign behavior.
- Static inspection and behavioral tests are complementary. Neither is complete.
- Security telemetry must preserve HiveNet's sovereignty and privacy boundaries. Do not collect user prompts or semantic content merely to monitor model-artifact integrity.
- Do not expose untrusted model artifacts, credentials, or privileged write paths to an editor model.

## Related work

- [HIVENET-RS-ADR-001 — Adversarial Distillation and Sovereign Multi-Model Security](../../papers/HIVENET-RS-ADR-001_ADVERSARIAL_DISTILLATION_AND_SOVEREIGN_SECURITY.md)
- [HIVENET-RS-ASTRA-001 — Astra Capability Assessment](../../papers/HIVENET-RS-ASTRA-001_ASTRA_CAPABILITY_ASSESSMENT.md)
- [OpenAI: Combatting adversarial distillation](https://openai.com/index/combatting-adversarial-distillation/)
- [Wang et al., arXiv:2611.17395](https://arxiv.org/abs/2611.17395)
- [Goworek et al., arXiv:2611.21449](https://arxiv.org/abs/2611.21449)

---

**Research status:** Proposed requirements pending founder review. No implementation or independent validation is claimed.

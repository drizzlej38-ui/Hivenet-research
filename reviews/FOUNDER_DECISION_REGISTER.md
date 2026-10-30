# Phase 2 — Founder Decision Register

**Status:** Open decisions; recommendations are provisional, not adopted  
**Purpose:** Preserve founder authority while making unresolved architecture choices visible. No item in this register silently changes the source specifications.

## Decision 1 — Prototype versus target architecture

**Question:** How should HiveNet describe its current state?

**Recommendation:** Adopt the distinction between the current LAN coordinator/worker demonstrator and the longer-term sovereign federation target. Describe the coordinator as a current implementation dependency and a bounded role in the target architecture.

**Why:** This preserves the work already done without claiming the mesh is already deployed.

**Status:** Awaiting founder confirmation.

## Decision 2 — Node taxonomy

**Question:** Should the eight classes in `SkyNet/NODE_CLASSES.md` be the canonical node-class vocabulary?

**Recommendation:** Use the eight listed classes as the candidate canonical set: `inference`, `coordinator`, `triage`, `archive`, `gateway`, `sentinel`, `registry`, and `ghost`. Keep sanitizer, detonation, render_proxy, and consensus as service sub-roles. Keep hardware capabilities (compute, storage, sensor, network) separate from classes.

**Why:** It resolves the overlap between node classes, network roles, and security services. Update Agent Card `node_class` to an array to match the composability rule in NODE_CLASSES.

**Status:** Recommendation only.

## Decision 3 — S.P.E.E.D. terminology

**Question:** Which expansion is canonical?

**Recommendation:** Use **Emergent Endogenic Design** as the current expansion. Treat “Symbiosis Protocol:” in the older source glossary as stale wording unless the founder later restores it.

**Why:** The founder explicitly corrected the current expansion.

**Status:** Current project terminology already corrected; source glossary update remains optional.

## Decision 4 — AGP canonical representation

**Question:** Should AGP be represented internally as a structured permission object, a compact string, or both?

**Recommendation:** Define a versioned structured token as the canonical semantic object. A compact string may be a transport/display encoding, but it must encode or securely reference every required field. Require issuer authentication, grantee binding, resource/set scope, expiry, nonce/replay controls, revocation behavior, and delegation constraints.

**Why:** The federation JSON schema is richer than the original compact string, while the current Python prototype has no cryptographic signing or grantee binding.

**Status:** Requires protocol design and founder review.

## Decision 5 — Collective immune-memory schema

**Question:** How should the incompatible phenotype schemas be reconciled?

**Recommendation:** Keep distinct fields for event type, resource effect, severity, minimized evidence, provenance/signature, advisory recommendation, and calibrated confidence (only when empirically supported). Treat records as advisory evidence, not executable commands.

**Why:** The current options classify different dimensions and should not be forced into one field.

**Status:** Proposed schema direction; not adopted.

## Decision 6 — ASH automatic quarantine authority

**Question:** Under what conditions may Dragon Radar automatically suspend AGP permissions?

**Recommendation:** Permit only narrowly scoped, temporary suspension when the owner has explicitly pre-authorized that protective behavior. Notify the owner, preserve a local forensic record, define expiry/review/appeal, and prohibit permanent membership removal without owner action.

**Why:** This reconciles “watches, does not act unilaterally” with automatic temporary suspension for high-severity incidents.

**Status:** Requires governance and threat-model review.

## Decision 7 — Sovereign Telemetry Boundary

**Question:** What is the non-negotiable data boundary for ASH and Dragon Radar?

**Recommendation:** Operational telemetry only, minimized and owner-custodied by default. No semantic-content inspection, hashing, logging, or transmission. Sharing requires explicit owner opt-in and defined scope. Metadata leakage and behavioral inference still require review.

**Why:** “No semantic content” is a meaningful limit, but it is not by itself proof of zero privacy risk.

**Status:** Strong existing design direction; enforcement specification and tests required.

## Decision 8 — Estuary and culturally governed knowledge

**Question:** Should Estuary material be universally discoverable or accessible?

**Recommendation:** No universal default. Discovery, preservation, transcription, translation, analysis, access, publication, and redistribution should be separately configurable by legitimate custodians and community protocols. Restricted material may be undiscoverable or excluded entirely.

**Why:** Universal-access phrases in older founding material conflict with custodianship and community authority when applied to restricted cultural knowledge.

**Status:** Governance principle requiring community/custodian input; technical design must not decide cultural authority.

## Decision 9 — Meaning of ENDCAP completeness

**Question:** What does the invariant `complete=true` guarantee?

**Recommendation:** Define it as a semantic requirement that each ENDCAP node represents a complete, independently useful unit of information. Define atomic commit, crash consistency, recovery, and durability separately in each storage backend.

**Why:** A Boolean constructor invariant does not prevent partial writes or power-loss corruption.

**Status:** Proposed clarification.

## Decision 10 — Canary use

**Question:** Are canaries mandatory or optional?

**Recommendation:** Optional, owner-authorized indicators with explicit disclosure of callback metadata and limitations. Do not treat a canary fire as conclusive proof of a person's intent or exact leak path.

**Why:** Automated scanners, previews, proxies, blocked networks, forwarding, and collusion can cause false or ambiguous attribution.

**Status:** Proposed clarification.

## Decision 11 — Current ENDCAP code lineage

**Question:** Which implementation should the research repository treat as the current ENDCAP implementation?

**Finding:** The SkyNet repository contains `endcap_prototype.py`, a deliberately incomplete in-memory ENDCAP/AGP identity prototype. It is distinct from the encrypted archive package described in project history.

**Recommendation:** Locate and pin the current encrypted archive package and its tests before making implementation claims about encryption, manifest-last commits, crash recovery, streaming, or large-file support.

**Status:** Evidence retrieval required.

## Decision 12 — Public research scope

**Question:** Which source materials should be copied into this research repository?

**Recommendation:** Only purpose-selected technical specifications, code excerpts where licensing permits, sanitized test evidence, and research documents. Do not mirror the mixed source repository wholesale. Do not include personal writing, third-party books, language/cultural files, or potentially restricted knowledge without specific review and permission.

**Why:** The source repository is a mixed working archive and not a curated research corpus.

**Status:** Adopt as working publication hygiene unless founder directs otherwise.

---

## How to use this register

- “Recommendation” is not a decision.
- The founder may accept, reject, amend, or defer any item.
- A decision should be recorded with date, rationale, affected documents, and implementation follow-up.
- No technical convenience overrides owner authority or legitimate cultural custodianship.

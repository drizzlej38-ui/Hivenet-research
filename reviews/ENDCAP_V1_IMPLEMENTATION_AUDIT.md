# ENDCAP V1 Encrypted Archive — Implementation Audit

**Review date:** 2026-10-30  
**Review type:** Static source review, test execution, CLI smoke test, and targeted behavior probes  
**Status:** Preliminary engineering evidence; not an independent cryptographic audit or production-readiness assessment  
**Source artifacts:** Saved project archives in the user's ChatGPT Library; no canonical GitHub source repository for this encrypted archive package was identified during this pass.

## 1. Executive result

The encrypted ENDCAP archive implementation is distinct from the separate SkyNet `endcap_prototype.py` identity/federation demonstration.

The actual package is Python `endcap`, version `0.1.0-proto`, with:
- `endcap/core.py`
- `endcap/storage.py`
- `endcap/cli.py`
- `endcap/__init__.py`
- `tests/test_core.py`
- `tests/test_hardening.py`
- V1-2 addition: `tests/test_recovery.py)

V1-1 implements a local encrypted archive core. V1-2 adds owner-key recovery without changing the archive format. The module explicitly excludes AGP authorization by design. The separate AGP V1 document remains a draft and is not wired into archive operations.

**Fresh test execution on 2026-10-30:**
- V1-1: 81 tests passed.
- V1-2: 90 tests passed.
- V1-2 also passed `pytest -q`: 90 passed.
- V1-2 command-line smoke test: key generation, archive, verify, retrieve, recovery-kit creation, and owner-key restoration succeeded in a temporary test directory. Recovered bytes matched the original input.

Environment: Python 3.13.5; `cryptography` 46.0.4. This environment is not the user's Termux device. The package README itself says Termux validation remains required.

## 2. Source provenance and integrity

| Artifact | Saved filename | Size | SHA-256 |
|---|---|---:|---|
| V1-1 original | `endcap_v1-1.zip` | 18,989 bytes | `d28abaec561b06bcfc8c3bef18914252e8fe5c7ac3121ae3ebb713d364ad3bea` |
| V1-1 duplicate | `endcap_v1-1(1).zip` | 18,989 bytes | `d28abaec561b06bcfc8c3bef18914252e8fe5c7ac3121ae3ebb713d364ad3bea` |
| V1-2 working copy | `endcap_v1-2.zip` | 25,044 bytes | `4af0f3022547d048c84ef3cb90b32776be571c5364b051d75b91e6e21fcdcbef` |

The duplicate V1-1 archive is byte-for-byte identical by SHA-256. V1-2 is a separate working copy, consistent with the earlier approval to work in `endcap_v1-2` while preserving V1-1.

No code was changed during this audit. The ZIPs were extracted to a temporary review directory and treated as read-only source material.

## 3. What the archive implementation actually does

### Encryption and object structure

- Generates a random 256-bit data-encryption key for each archive.
- Encrypts file data in chunks with AES-256-GCM through Python's `cryptography` package; no custom cryptographic primitive is implemented.
- Wraps the per-archive data key using the 256-bit owner key and AES-GCM.
- Encrypts metadata in the manifest, including original filename, plaintext size, chunk size, and chunk count.
- Uses a random 128-bit object ID, not a plaintext content hash.
- Stores no plaintext hash.
- Uses authenticated additional data (AAD) to bind encrypted chunks to the object ID, chunk index, and final-chunk flag.
- Uses a fixed metadata nonce that is distinct from the chunk nonce construction under the per-archive data key.
- Uses a random 96-bit nonce for wrapping the data key under the long-lived owner key.

The documented nonce design relies on a fresh random data key per archive. The design document itself notes that random wrapping nonces under one long-lived owner key should be revisited if that key wraps a very large number of archives.

### Commit and retrieval behavior

- Writes encrypted chunk blobs first.
- Writes the manifest last; the manifest is the logical commit marker.
- An object with data blobs but no manifest is reported as incomplete.
- Retrieval writes to a temporary file, authenticates chunks, checks total plaintext length, flushes and fsyncs the temporary file, then replaces the destination.
- Existing destination files are not overwritten unless the caller explicitly opts in.
- A failed retrieval removes its temporary output and leaves the destination untouched.

### Limits

Pilot implementation defaults, not protocol rules:
- Maximum chunk size: 16 MiB.
- Maximum chunk count: 65,536.
- Maximum archive size: 1 GiB.
- Default chunk size: 1 MiB.

Custom limits must be supplied consistently to archive, verify, and retrieve. The format does not record a named limits profile.

## 4. V1-1 to V1-2 changes

V1-2 adds an owner-key recovery kit:
- Generates a random 256-bit recovery secret.
- Encrypts the existing 32-byte owner key with AES-256-GCM.
- Stores a versioned JSON kit containing the algorithm, nonce, ciphertext, and authenticated owner-key identifier.
- Displays the recovery secret once and returns an 8-hex-character transcription checksum.
- Does not persist the secret in the kit.
- Requires the kit and secret to be stored separately.
- Refuses to overwrite an existing kit or restored key file.
- Uses owner-only file permissions (0600) on POSIX.
- Gives a generic error for wrong secrets and damaged/mismatched kits.

The V1-2 recovery kit does **not** change existing archive blobs, manifests, or archive format. The recovery feature restores the encryption owner key only. It does not recover Ed25519 signing keys and does not implement AGP/ATP owner-bypass authorization.

## 5. AGP relationship: separate by design, not integrated

This distinction is central:

- ENDCAP V1 archive core performs encryption, integrity verification, storage, and retrieval.
- The code comment explicitly states: **“Authorization (AGP) is NOT in this module by design.”**
- The AGP V1 document is labeled a draft and explicitly says it is not a final token format.
- The AGP draft proposes Ed25519 owner-signed grants, recipient-signed requests, resource/operation checks, expiry, revocation, replay prevention, and fail-closed authorization.
- None of those AGP gate functions are present in the encrypted archive package inspected here.
- No Ed25519 implementation, signing-key generation, signature verification, or signing-key recovery is present in this package.
- The archive package does not implement recipient-specific key wrapping. Possession of the owner key is sufficient to decrypt archives; a remote recipient needs a separately designed key-delivery/wrapping mechanism.

The separation is a legitimate modular design choice. It must not be represented as though the archive package already enforces AGP.

### AGP/ENDCAP design questions

1. The AGP draft's earlier token string uses a SHA-256 content hash, while ENDCAP deliberately stores no plaintext hash and uses a random object ID. The draft itself identifies this mismatch as unresolved. A random ENDCAP object ID or a ciphertext/manifest-derived identifier avoids making plaintext equality tests easier for a storage provider.
2. The AGP draft proposes an owner recovery path that bypasses grants. V1-2's recovery-kit feature restores the encryption owner key but explicitly does not implement an authorization bypass. These are different meanings of “recovery” and must remain distinct.
3. The AGP draft proposes a gate on every protected ENDCAP operation. That gate must be designed and tested as a separate integration layer; it is not a property of V1-2.
4. Threshold validation, recipient-key enrollment, trusted issuer keys, clock skew, revocation propagation, and replay persistence remain unresolved in the AGP draft.

## 6. Test evidence

### Tests that are present and passed

The existing suite exercises:
- Round-trip encryption and retrieval, including empty and boundary-size files.
- Wrong owner key.
- Chunk tampering.
- Manifest/wrapped-key tampering.
- Missing and truncated chunks.
- Swapped chunks and cross-object chunk substitution.
- Interrupted uploads and manifest-write failures.
- Duplicate committed object IDs.
- Malformed manifests and object IDs.
- Failure-safe retrieval and destination overwrite rules.
- Metadata confidentiality in the storage-provider view.
- Owner-key file handling and path-traversal key rejection.
- Metadata type/range/consistency validation.
- Stored-blob length checks.
- Writer and reader limit enforcement.
- Recovery-kit creation, restore, wrong-secret behavior, tampering, truncation, version checks, overwrite protection, and preservation of existing archive bytes.

### What the test suite does not establish

- Termux/Android behavior.
- Power-loss durability or actual filesystem crash consistency.
- Multi-process or concurrent-writer correctness.
- Security against a hostile local filesystem with symlink manipulation.
- Bounded memory use against malicious storage backends.
- Cryptographic protocol review by an independent specialist.
- Formal verification or production readiness.
- AGP authorization, recipient key delivery, or distributed revocation.

The tests simulate failed writes and verify manifest-last behavior, but simulated exceptions are not equivalent to abruptly cutting power during filesystem metadata updates.

## 7. Findings requiring attention

### Finding E1 — Symlink escape in LocalDirBackend path handling

**Severity:** High for a local store directory that can be modified by another untrusted local process; lower when the store root and all parent directories are strictly owner-controlled.

`LocalDirBackend._path()` performs a lexical absolute-path prefix check. It does not resolve or reject symlinks in path components. A directory symlink placed inside the store root can cause `put()` to write outside the configured root.

This was reproduced during the audit: a path such as `<store>/<object_id>` was made a symlink to an outside directory, and `put("<object_id>/chunk", ...)` wrote the chunk into that outside directory.

**Recommendation:** Harden local path traversal against symlinks (for example, directory-descriptor-relative operations with no-follow semantics where supported, or strict symlink rejection for every path component). Add regression tests for symlinked object directories and symlink races. Do not claim the current LocalDirBackend is safe against a hostile local filesystem.

### Finding E2 — `status()` overstates what it knows

**Severity:** Medium; semantic/API correctness.

`status()` returns `complete` whenever the manifest key exists. It does not parse or authenticate the manifest and does not check that all expected chunks exist or authenticate.

This was reproduced: after deleting the only chunk of a committed one-chunk archive, `status()` still returned `complete`, while `verify()` correctly raised `MissingDataError`.

**Recommendation:** Either rename the state to something like `manifest-present` / `committed-marker-present`, or clearly document that `complete` means only “manifest marker exists.” Reserve “verified” for a successful `verify()` operation.

### Finding E3 — Crash durability is not fully established by atomic per-blob replacement

**Severity:** Medium; storage durability.

The local backend writes and fsyncs each temporary blob, then uses `os.replace()`. The retrieval path similarly fsyncs the temporary output before replacement. The containing directory is not fsynced after rename. Atomic visibility during normal operation is not the same as durable ordering across sudden power loss.

**Recommendation:** Define the supported crash model. If power-loss durability is required, fsync containing directories after relevant renames (and carefully order chunk and manifest persistence). Add crash/fault-injection tests on supported filesystems. Until then, describe manifest-last as a logical commit protocol, not a proven power-loss transaction guarantee.

### Finding E4 — Concurrent writers are not serialized

**Severity:** Medium; concurrency integrity.

Two concurrent archive operations using the same caller-supplied object ID can both observe no manifest and interleave chunk writes before either writes its manifest. There is no reservation/locking protocol. The design document already lists concurrency control as not provided.

**Recommendation:** Explicitly reject or serialize concurrent writes for the same object ID, or define a backend-level atomic reservation/commit primitive. Add multi-process race tests before claiming safe concurrent use.

### Finding E5 — Backend reads are not memory-bounded

**Severity:** Medium to high depending on backend trust.

The storage interface's `get()` returns an entire blob as bytes. Length checks happen only after allocation. A malicious backend can force large memory allocations before the archive code rejects an oversized blob. The design document explicitly acknowledges this limitation.

**Recommendation:** Design a bounded/streaming read interface and enforce a maximum before materializing attacker-controlled data. Until implemented, limit backend trust and deployment scope.

### Finding E6 — Retrieval no-overwrite check has a narrow race

**Severity:** Low to medium; concurrent local processes.

When `overwrite=False`, retrieval checks whether the destination exists before creating the temporary file and checks again before `os.replace()`. Another process can create the destination between the second check and replacement, leaving a small race in which `os.replace()` overwrites it.

**Recommendation:** Use an atomic no-replace installation primitive where supported, or document the single-writer assumption and add a race test.

### Finding E7 — Recovery-kit checksum is a transcription aid, not an authentication factor

**Severity:** Informational; correctly documented.

The 8-hex-character checksum is 32 bits and is intended to catch transcription errors. Security comes from the 256-bit recovery secret and AES-GCM authentication, not from the short checksum. Documentation already makes this distinction.

### Finding E8 — Signing keys are outside this package

**Severity:** Scope clarification.

The design says AGP Ed25519 signing keys are separate from encryption keys. That is architecturally sensible, but this archive package does not generate, store, recover, or validate those signing keys. V1-2 owner-key recovery must not be described as complete recovery of the user's entire ENDCAP/AGP identity.

## 8. Architecture interpretation

The strongest accurate description today is:

> ENDCAP V1-2 is a local Python encrypted-archive prototype with chunked AES-256-GCM encryption, per-archive data keys wrapped by an owner key, encrypted metadata, manifest-last logical commit marking, authenticated retrieval, bounded format metadata, and a separate owner-key recovery-kit feature. Its storage backend is pluggable in the interface, but only local-directory and in-memory backends are supplied. AGP authorization, recipient key delivery, Ed25519 grant signing, distributed storage, redundancy, key rotation, and crash-durable transactions are not implemented in this package.

This is a substantive implementation, not merely a concept sketch. It is still a prototype, not a production archive service.

## 9. Recommended next actions

1. Preserve V1-1 and V1-2 as immutable source snapshots with their SHA-256 hashes.
2. Keep the actual encrypted archive core separate from the SkyNet identity/federation prototype in all architecture diagrams and publication claims.
3. Prioritize the LocalDirBackend symlink issue and add regression tests before using it with a storage root writable by other processes.
4. Clarify `status()` semantics so “manifest exists” is not confused with “archive verified.”
5. Define the crash-durability model and concurrency guarantees.
6. Design the bounded/streaming backend interface before large or adversarial storage use.
7. Specify AGP as a separate authorization gate and key-delivery layer; do not silently merge it into ENDCAP encryption.
8. Resolve the AGP resource identifier choice and owner-recovery terminology.
9. Run the full suite on the target Termux/Android environment and preserve the exact Python/cryptography versions and output.
10. Only after the above, consider an implementation revision. This audit did not modify the user's V1-1 or V1-2 code.

## 10. Evidence summary

| Evidence item | Result |
|---|---|
| V1-1 source archive integrity | SHA-256 recorded; duplicate archive matched exactly |
| V1-2 source archive integrity | SHA-256 recorded |
| V1-1 unittest suite | 81 passed |
| V1-2 unittest suite | 90 passed |
| V1-2 pytest suite | 90 passed |
| V1-2 CLI smoke test | keygen/archive/verify/retrieve/recovery-kit/recover-key passed |
| Byte-for-byte archive round trip | Passed in smoke test |
| Owner-key recovery restoring old archive | Covered by tests and CLI smoke test |
| Symlink path escape probe | Reproduced |
| Status false-complete probe | Reproduced |
| Termux validation | Not performed |
| Independent cryptographic audit | Not performed |
| Power-loss crash testing | Not performed |

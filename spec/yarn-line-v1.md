# spec/yarn-line-v1.md

## Yarn Lineage Specification v1.0

Status: DRAFT (LOCK EXTENSIONS)
Scope: Defines the canonical derivation rules, directives, and validation for æ lineage tracking via yarn lines.

---

## 1) Yarn Lineage Tracking

yarn lines are immutable records expressing where æ panels execute, their relationships, and their execution state.

Every valid yarn line consists of:
- Session ID (**SID**) to track execution origins.
- Unique User Hash (**UID**).
- Content Integrity Hash (**HASH**).

Example:
`SID:47x123-UID:e3b0-HASH:abc123`

---

## 2) Canonical Derivation Rules

### 2.1 SID (Session ID)
- Uniquely identifies the originating thread.
- Format: `Base32` or `Base58`, length defined by implementer.
- MUST include origin timestamp. Example derivation:
`SID = threadSeed + timestamp`

### 2.2 UID (User Identification Hash)
- Represents an immutable mapping of a user or credential space.
- Calculated with SHA256 hash. Example:
`UID = SHA256(username@domain)`

---

## 3) Yarn Directives

### 3.1 YARN::APPEND
Appends new execution nodes to the lineage without overwriting prior states.

Example signature:
`YARN::APPEND(SID, HASH) ::extend->+OK`

### 3.2 Failure Precondition Stop
If `UID` mismatch OR execution preconditions fail:
- NO nodes may append.
- Emit STOP marker:
`YARN::REFUSE`

---

## 4) Validation Canon

1. **Immutable lineage:** Yarn lines MUST NOT mutate after validation.
2. **Integrity hash:** Use SHA256 to checksum prior to execution.
3. **Execution stops** with failure.

---

Yarn lines enforce traceable, SHA-alligned **æ lineage**, ensuring valid history for panels and payload states.
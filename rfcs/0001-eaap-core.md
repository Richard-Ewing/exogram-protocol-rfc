# RFC-0001: Exogram Action Admissibility Protocol (EAAP)

- **RFC**: 0001
- **Title**: EAAP Core Protocol — Deterministic Execution Control for Autonomous AI
- **Author**: Richard Ewing (richard@exogram.ai)
- **Status**: Active
- **Created**: 2026-02-15
- **Updated**: 2026-03-18
- **Discussion**: https://github.com/Richard-Ewing/exogram-protocol-rfc/issues

---

## Abstract

This document specifies the Exogram Action Admissibility Protocol (EAAP), a four-layer deterministic control plane that sits between AI reasoning and real-world execution. EAAP provides Identity and Access Management (IAM) for non-human entities — autonomous AI agents — by enforcing truth verification, contradiction detection, constraint evaluation, and cryptographic execution gating before any agent action is permitted.

EAAP uses zero model inference for judgment. All execution gates are deterministic Python logic. The protocol is model-agnostic, framework-agnostic, and designed for production environments where AI agents perform state-changing operations.

## 1. Motivation

### 1.1 The Problem

AI agents are being deployed to production systems where they:
- Modify billing records and financial data
- Delete regulated or compliance-sensitive data
- Trigger operational workflows (deployments, notifications, escalations)
- Make commitments on behalf of organizations
- Access and transform personally identifiable information (PII)

These agents operate on probabilistic inference. They hallucinate facts, contradict themselves across sessions, silently rewrite context, and operate without persistent truth state. No existing infrastructure layer governs what an agent is *allowed* to do before it does it.

### 1.2 The Gap

Current AI infrastructure addresses adjacent concerns but not execution governance:

| Category | Example | What It Does | What It Does NOT Do |
|----------|---------|-------------|---------------------|
| Orchestration | LangChain, CrewAI, AutoGen | Routes agent steps | Does not govern admissibility |
| Agent Frameworks | NVIDIA NemoClaw, OpenClaw | Builds/executes agents | Does not verify truth or gate execution |
| Output Filtering | Guardrails AI, NeMo Guardrails | Validates model outputs | Does not maintain persistent truth state |
| Memory | Mem0, Zep, LangMem | Stores context | Does not verify facts or detect contradictions |
| Human IAM | Auth0, Okta | Governs human access | Does not address non-human entities |

**Orchestration ≠ governance.** The agent cannot act as its own security guard.

### 1.3 Design Principles

1. **Deterministic over probabilistic**: Execution gates use code, never model inference
2. **Fail closed**: Under uncertainty, deny — never default to allow
3. **Zero trust on model output**: All model output is treated as untrusted input
4. **Immutable auditability**: Every mutation is logged, chained, and tamper-detectable
5. **Separation of concerns**: The governance plane is independent of the inference plane

## 2. Protocol Architecture

### 2.1 Four-Layer Control Plane

```
┌─────────────────────────────────────────────────────────┐
│                    Agent / Model                         │
│              (Probabilistic Inference)                   │
└──────────────────────┬──────────────────────────────────┘
                       │ Proposed Action
                       ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 1: Ledger Governance                              │
│  ├─ PII Detection & Scrubbing (deterministic patterns)  │
│  ├─ AES-256-GCM Encryption (per-user Fernet keys)      │
│  ├─ Semantic Indexing (vector embeddings)                │
│  ├─ Conflict Detection (against existing ledger)        │
│  ├─ Confidence Scoring (with temporal decay)            │
│  ├─ Fact Locking (immutable constraints)                │
│  └─ Audit Event Logging (cryptographic chaining)        │
└──────────────────────┬──────────────────────────────────┘
                       ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 2: Meaning Engine                                 │
│  ├─ Namespace Isolation (strict user-scoped retrieval)  │
│  ├─ Deterministic Relevance Scoring                     │
│  ├─ Temporal Decay Weighting                            │
│  ├─ Conflict Surfacing                                   │
│  ├─ Context Health Classification                        │
│  └─ HMAC-Signed Snapshot Generation                     │
└──────────────────────┬──────────────────────────────────┘
                       ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 3: Judgment Engine                                │
│  ├─ Authority Validation                                 │
│  ├─ Fact Consistency Enforcement                         │
│  ├─ Constraint Evaluation                                │
│  ├─ Confidence Threshold Enforcement                    │
│  └─ Escalation Classification                            │
│                                                          │
│  ⚠ ZERO MODEL INFERENCE — Deterministic Python logic    │
└──────────────────────┬──────────────────────────────────┘
                       ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 4: Action Admissibility                           │
│  ├─ Claim Extraction from Payload                       │
│  ├─ Pre-flight Conflict Detection                       │
│  ├─ SHA-256 State Hashing                                │
│  ├─ Evaluation Record Creation                           │
│  ├─ Commit Validation (rejects on state drift)          │
│  └─ Immutable Action Ledger                              │
└──────────────────────┬──────────────────────────────────┘
                       ▼
              ALLOW / BLOCK / ESCALATE
```

### 2.2 Layer 1: Ledger Governance

**Purpose**: Enforce ledger integrity before any data enters the system.

**Operations**:

| Operation | Description | Deterministic |
|-----------|-------------|:---:|
| PII Scrubbing | Pattern-based detection of SSN, email, phone, credentials | ✅ |
| Encryption | AES-256-GCM with per-user Fernet keys derived from master key | ✅ |
| Semantic Indexing | Vector embedding generation for similarity search | ✅ |
| Conflict Detection | Cosine similarity search against existing entries | ✅ |
| Confidence Scoring | Initial confidence with temporal decay function | ✅ |
| Fact Locking | Locked entries cannot be modified without explicit unlock | ✅ |
| Audit Logging | Cryptographically chained event log entry | ✅ |

**Rule**: No silent overwrites. Contradictions require explicit resolution by a human or authorized process.

### 2.3 Layer 2: Meaning Engine

**Purpose**: Assemble bounded, deterministic context for evaluation.

Context assembly is mathematical, not generative. The Meaning Engine:

1. Retrieves facts scoped to the requesting user's namespace
2. Applies deterministic relevance scoring
3. Weights results by temporal decay (recent facts score higher)
4. Surfaces any conflicts within the assembled context
5. Classifies overall context health (healthy, degraded, conflicted)
6. Generates an HMAC-signed snapshot of the context state

**Rule**: Context assembly uses no model inference. Output is deterministic given the same inputs.

### 2.4 Layer 3: Judgment Engine

**Purpose**: Evaluate admissibility through deterministic logic gates.

The Judgment Engine executes a series of Python logic gates:

```python
def evaluate(action, context, constraints):
    # Gate 1: Authority
    if not has_authority(action.actor, action.scope):
        return BLOCK("insufficient_authority")

    # Gate 2: Fact Consistency
    conflicts = detect_conflicts(action.claims, context.facts)
    if conflicts:
        return BLOCK("fact_conflict", conflicts=conflicts)

    # Gate 3: Constraint Evaluation
    violations = check_constraints(action, constraints)
    if violations:
        return BLOCK("constraint_violation", violations=violations)

    # Gate 4: Confidence Threshold
    if context.confidence < MINIMUM_CONFIDENCE:
        return ESCALATE("low_confidence")

    # Gate 5: Escalation Check
    if requires_escalation(action):
        return ESCALATE("requires_human_review")

    return ALLOW(evaluation_id=generate_id())
```

**Rule**: Zero model inference. Every gate is a Python conditional. The output is deterministic.

### 2.5 Layer 4: Action Admissibility

**Purpose**: Guarantee execution integrity between evaluation and commit.

**Evaluation Phase**:
1. Extract claims from the proposed action payload
2. Execute pre-flight conflict detection
3. Compute SHA-256 state hash over relevant objects, policy version, namespace, and time window
4. Persist evaluation record with the state hash
5. Return ALLOW/BLOCK/ESCALATE with `evaluation_id`

**Commit Phase**:
1. Retrieve evaluation record by `evaluation_id`
2. Verify evaluation has not expired (TTL check)
3. Recompute full state hash from current state
4. Compare computed hash with evaluation hash
5. If mismatch → reject with `409 Conflict` (state drift detected)
6. Persist immutable action ledger record
7. Return `committed`

**State Hash Formula**:

```
state_hash = SHA-256(
    sorted(relevant_objects) ||
    policy_version            ||
    namespace_id              ||
    floor(timestamp, window)
)
```

**Rule**: Layer 4 is the final execution gate. No action bypasses it.

## 3. Protocol Invariants

These invariants are mandatory, non-configurable, and cannot be weakened without a major version change:

| # | Invariant | Description |
|---|-----------|-------------|
| 1 | PII Air Gap | No detected PII enters persistent storage or vector embeddings |
| 2 | Explicit Source | All stored facts require provenance attribution |
| 3 | Encryption at Rest | All content encrypted with per-user keys |
| 4 | Namespace Isolation | Retrieval and evaluation scoped strictly to user namespace |
| 5 | No Silent Overwrite | Conflicting facts require explicit resolution |
| 6 | Conflict Logging | All contradictions produce durable, auditable records |
| 7 | Immutable Audit Chain | Cryptographically chained audit events, tamper-detectable |
| 8 | Deterministic Judgment | Execution gates use code, not model inference |
| 9 | Confidence Decay | Facts degrade in authority over time unless reinforced |
| 10 | Constraint Binding | Locked facts cannot be violated without explicit unlock |
| 11 | State Hash Integrity | Execution requires identical state between evaluation and commit |
| 12 | Evaluation Expiry | Approvals expire after defined TTL, no stale tokens |
| 13 | Escalation Routing | Blocked actions route to structured escalation targets |
| 14 | Hard Deletion (GDPR) | Full deletion removes vectors, ciphertext, and all records |

## 4. Threat Model

EAAP assumes the following adversarial conditions. Under **all** conditions, EAAP **fails closed** (never defaults to allow):

### 4.1 Model Unreliability
Language models hallucinate facts, contradict stored information, and generate false statements with high confidence. EAAP treats all model output as untrusted input that must be verified against the ledger before any state change is permitted.

### 4.2 Prompt Injection
Attackers craft inputs that override constraints, induce self-contradiction, mask harmful instructions behind benign context, or manipulate tool usage patterns. EAAP's deterministic logic gates are immune to prompt injection because they execute code, not natural language processing.

### 4.3 State Drift (TOCTOU)
Between evaluation and execution, system state may change: roles are modified, constraints are updated, facts are added or retracted, new conflicts emerge. The SHA-256 state hash comparison at commit time detects any such drift and rejects the action.

### 4.4 Infrastructure Degradation
Model provider outages, embedding service unavailability, and database connectivity failures. EAAP activates circuit breakers and returns `503 Service Unavailable` rather than degrading to permissive mode.

### 4.5 Insider Risk
Manual database modification, audit log tampering, and replay of previously approved action tokens. Cryptographic audit chaining makes tampering detectable. Evaluation expiry prevents token replay.

## 5. API Surface

### 5.1 Core Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/v2/vault/store` | Store a verified fact with encryption, PII scrubbing, and conflict detection |
| `POST` | `/v2/vault/search` | Semantic search across encrypted memory vault |
| `POST` | `/v2/actions/evaluate` | Evaluate a proposed action against constraints |
| `POST` | `/v2/actions/commit` | Commit an evaluated action (rejects on state drift) |
| `GET` | `/v2/ledger/entries` | List ledger entries with filtering and pagination |

### 5.2 Authentication

```
Authorization: Bearer sk_exo_...
```

### 5.3 Response Codes

| Code | Meaning |
|------|---------|
| `200` | Action evaluated or committed successfully |
| `201` | Fact stored successfully |
| `400` | Malformed request |
| `401` | Invalid or missing API key |
| `403` | Action blocked by governance layer |
| `409` | State drift detected — evaluation hash mismatch at commit |
| `429` | Rate limit exceeded |
| `503` | Infrastructure degradation — fail closed |

## 6. Framework Integration Points

EAAP defines interception points for integration with agent frameworks:

| Framework | Interception Point |
|-----------|-------------------|
| LangChain | Tool execution callbacks |
| AutoGen | Function call hooks |
| CrewAI | Task delegation middleware |
| OpenAI Assistants | Function calling wrapper |
| Anthropic Claude | Tool use interception |
| Google Vertex AI | Function calling middleware |
| LlamaIndex | Query engine pre-processor |
| NVIDIA NemoClaw | Agent action middleware |
| OpenClaw | Agent action middleware |
| Custom REST | HTTP middleware / API gateway |

## 7. Security Considerations

### 7.1 Encryption
All data at rest is encrypted using AES-256-GCM with per-user Fernet keys derived from a master encryption key using PBKDF2 with user-specific salts.

### 7.2 PII Handling
PII detection uses deterministic pattern matching (regex), not LLM-based classification. Detected PII is scrubbed before storage. The original PII is never persisted.

### 7.3 Audit Integrity
Audit events are cryptographically chained. Each event includes a hash of the previous event. Tampering with any event breaks the chain and is detectable.

### 7.4 Namespace Isolation
Every operation is scoped to a user namespace. Cross-namespace data access is architecturally impossible — queries are parameterized at the database level.

## 8. Conformance

An implementation is considered **EAAP-conformant** if it:

1. Implements all four layers (L1–L4) with the specified operations
2. Enforces all 14 protocol invariants without exception
3. Uses zero model inference in the Judgment Engine (L3)
4. Implements SHA-256 state hash comparison for commit validation
5. Fails closed under all error conditions
6. Produces an immutable, cryptographically chained audit trail

## 9. References

- [EAAP Protocol Overview](https://exogram.ai/protocol) — Visual architecture walkthrough
- [RFC-0001 Interactive](https://exogram.ai/rfc/0001) — Web-rendered specification
- [API Reference](https://exogram.ai/docs/api) — REST API documentation
- [Architecture Deep Dive](https://exogram.ai/architecture) — Four-layer implementation details

## 10. Copyright

This specification is licensed under the Apache License, Version 2.0. See [LICENSE](../LICENSE).

---

*Author: Richard Ewing (richard@exogram.ai)*
*Organization: Exogram (https://exogram.ai)*

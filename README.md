<p align="center">
  <img src="https://exogram.ai/favicon.ico" width="48" height="48" alt="Exogram" />
</p>

<h1 align="center">Exogram Action Admissibility Protocol (EAAP)</h1>

<p align="center">
  <strong>An open protocol for deterministic governance of autonomous AI agents.</strong>
</p>

<p align="center">
  <a href="https://exogram.ai/rfc/0001">RFC-0001</a> ·
  <a href="https://exogram.ai/protocol">Protocol Overview</a> ·
  <a href="https://exogram.ai/architecture">Architecture</a> ·
  <a href="#quick-start">Quick Start</a>
</p>

---

## The Problem

AI agents are being deployed to production systems where they can modify billing records, delete regulated data, trigger operational workflows, and make commitments on behalf of organizations.

These agents operate on probabilistic inference. They hallucinate. They contradict themselves across sessions. They silently rewrite context. And there is no infrastructure layer that governs what they are allowed to do before they do it.

**Orchestration frameworks route actions. Nothing governs them.**

## The Protocol

EAAP (Exogram Action Admissibility Protocol) is a four-layer deterministic control plane that sits between AI reasoning and real-world execution. It provides Identity and Access Management (IAM) for non-human entities.

Every proposed agent action passes through four layers before execution is permitted:

| Layer | Name | Purpose |
|-------|------|---------|
| **L1** | Ledger Governance | PII scrubbing, encryption, conflict detection, immutable versioning |
| **L2** | Meaning Engine | Deterministic context assembly with temporal decay and namespace isolation |
| **L3** | Judgment Engine | Constraint evaluation via deterministic Python logic gates — zero model inference |
| **L4** | Action Admissibility | SHA-256 state hashing, execution token generation, commit validation |

### Core Invariants

The protocol enforces 14 non-negotiable invariants:

1. **PII Air Gap** — No detected PII enters persistent storage or vector embeddings
2. **Explicit Source** — All stored facts require provenance attribution
3. **Encryption at Rest** — All content encrypted with per-user keys
4. **Namespace Isolation** — Retrieval scoped strictly to user namespace
5. **No Silent Overwrite** — Conflicting facts require explicit resolution
6. **Conflict Logging** — All contradictions produce durable, auditable records
7. **Immutable Audit Chain** — Cryptographically chained events, tamper-detectable
8. **Deterministic Judgment** — Execution gates use code, not model inference
9. **Confidence Decay** — Facts degrade in authority over time unless reinforced
10. **Constraint Binding** — Locked facts cannot be violated without explicit unlock
11. **State Hash Integrity** — Execution requires identical state between evaluation and commit
12. **Evaluation Expiry** — Approvals expire after defined TTL
13. **Escalation Routing** — Blocked actions route to structured escalation targets
14. **Hard Deletion (GDPR)** — Full deletion removes vectors, ciphertext, and all records

### Evaluation → Commit Flow

```
Agent proposes action
    │
    ▼
┌─────────────────────────┐
│  L1: Ledger Governance  │  PII scrub → Encrypt → Conflict check → Version
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│  L2: Meaning Engine     │  Namespace isolate → Temporal weight → HMAC snapshot
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│  L3: Judgment Engine    │  Authority → Consistency → Constraints → Confidence
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│  L4: Action Admissibility│  State hash → Token → Commit validation
└──────────┬──────────────┘
           ▼
   ALLOW / BLOCK / ESCALATE
```

### State Hash Formula

```
state_hash = SHA-256(
    sorted(relevant_objects) ||
    policy_version            ||
    namespace_id              ||
    floor(timestamp, window)
)
```

If the state hash at commit time differs from the state hash at evaluation time, the commit is rejected with `409 Conflict`. This prevents Time-of-Check to Time-of-Use (TOCTOU) attacks.

## RFCs

| RFC | Title | Status |
|-----|-------|--------|
| [RFC-0001](rfcs/0001-eaap-core.md) | EAAP Core Protocol — Deterministic Execution Control for Autonomous AI | **Active** |

## Quick Start

### For Implementers

The protocol is open. You are free to implement EAAP in any language, for any platform, under the Apache 2.0 license. The [full specification](rfcs/0001-eaap-core.md) defines every data payload, error code, and security consideration.

```
# Clone the spec
git clone https://github.com/Richard-Ewing/exogram-protocol-rfc.git

# Read the core RFC
cat rfcs/0001-eaap-core.md
```

### For Teams That Want It Now

[**Exogram.ai**](https://exogram.ai) provides a fully managed, enterprise-ready implementation of the EAAP protocol. It includes:

- **Hosted infrastructure** — no deployment, no ops
- **REST API** — integrate in under 5 minutes
- **MCP server** — native Claude Desktop integration
- **ChatGPT Custom GPT** — governed memory inside ChatGPT
- **Chrome Extension** — capture facts from any webpage
- **Free tier** — 500 evaluations/month, no credit card

The protocol is free. The infrastructure is optional. Build it yourself or let us run it.

→ [Get started at exogram.ai](https://exogram.ai/signup)

## Threat Model

EAAP assumes the following adversarial conditions. Under all conditions, the protocol **fails closed** (never defaults to allow):

| Threat | Description |
|--------|-------------|
| **Model Unreliability** | Language models hallucinate, contradict stored facts, generate false statements |
| **Prompt Injection** | Attackers override constraints, mask harmful instructions, manipulate tool usage |
| **State Drift (TOCTOU)** | Between evaluation and execution: roles change, constraints mutate, facts update |
| **Infrastructure Degradation** | Model provider outages, embedding unavailability, circuit breaker activation |
| **Insider Risk** | Manual database modification, audit log tampering, replay of approved actions |

## Contributing

We welcome architectural feedback, schema corrections, and security reviews.

- **Architectural debate** → [Open a GitHub Issue](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues)
- **Schema corrections** → [Submit a Pull Request](https://github.com/Richard-Ewing/exogram-protocol-rfc/pulls)
- **Security vulnerabilities** → See [SECURITY.md](SECURITY.md)

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting.

## License

This protocol specification is licensed under [Apache License 2.0](LICENSE). You are free to implement, extend, and distribute your own implementations.

## Links

- [Exogram.ai](https://exogram.ai) — Managed EAAP implementation
- [Protocol Overview](https://exogram.ai/protocol) — Visual architecture walkthrough
- [RFC-0001 (Web)](https://exogram.ai/rfc/0001) — Interactive spec
- [API Reference](https://exogram.ai/docs/api) — REST API documentation
- [Architecture](https://exogram.ai/architecture) — Four-layer deep dive

---

<p align="center">
  <sub>The protocol is open. The standard is free. The reference implementation is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

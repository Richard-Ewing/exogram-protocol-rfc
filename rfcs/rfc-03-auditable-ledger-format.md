# RFC-03: The Auditable Ledger Format

**Status:** Draft  
**Author:** Richard Ewing  
**Created:** 2026-05-27  
**Standard:** Exogram Protocol v1

---

## Abstract

This RFC proposes a verifiable, append-only standard for logging AI execution history — transforming passive AI memory into enterprise-grade accountability infrastructure.

## Goal

Create a verifiable, append-only standard for logging AI execution history that captures not just what happened, but *why* it happened and *who authorized it*.

## Core Challenge

Standard AI logs just show input (prompt) and output (response). The Exogram ledger must capture **State Hash** + **Active Governance Policy** + **Attempted Action** + **Approval/Denial Code**. This RFC designs the exact data structure required for an enterprise compliance team to trace exactly *why* an agent took an action.

## Design Principles

1. **Append-Only** — Ledger entries are immutable. No modification, no deletion (except GDPR hard-delete).
2. **Cryptographically Chained** — Each entry references the hash of the previous entry, creating a tamper-detectable chain.
3. **Complete Provenance** — Every entry captures the full evaluation context: who, what, when, why, and the governance decision.
4. **Queryable** — The ledger must support efficient querying for compliance audits, incident response, and forensic analysis.
5. **Per-Request Telemetry** — Every evaluation logs `compute_latency_ms`, `agent_id`, `raw_intent`, and the policy version.

## Ledger Entry Schema

```json
{
  "ledger_entry": {
    "entry_id": "uuid-v4",
    "timestamp": "ISO-8601",
    "previous_hash": "sha256:...",
    "entry_hash": "sha256:...",
    
    "agent": {
      "agent_id": "agt_8f72c91a",
      "model": "claude-4-opus",
      "framework": "langchain-v0.3"
    },
    
    "evaluation": {
      "raw_intent": "Delete all records from users table where last_login < 2025-01-01",
      "action": "DELETE_RECORDS",
      "target_system": "production_postgres",
      "state_hash_at_evaluation": "sha256:...",
      "state_hash_at_commit": "sha256:...",
      "state_match": true
    },
    
    "governance": {
      "policy_version": "v1.4.2",
      "rules_evaluated": 8,
      "result": "BLOCKED",
      "reason_code": "RULE_04: NO_DESTRUCTIVE_ACTIONS_IN_PROD",
      "compute_latency_ms": 0.07
    },
    
    "outcome": {
      "execution_permitted": false,
      "execution_token": null,
      "escalation_target": "security-team@company.com"
    }
  }
}
```

## Why Standard Logs Are Insufficient

| Feature | Standard AI Logs | Exogram Auditable Ledger |
|---------|-----------------|-------------------------|
| What happened | ✅ Input/Output | ✅ Full action detail |
| Why it happened | ❌ | ✅ Policy rule + reason code |
| Who authorized it | ❌ | ✅ Governance decision chain |
| State at decision time | ❌ | ✅ SHA-256 state hash |
| Tamper detection | ❌ | ✅ Cryptographic chaining |
| Compliance-ready | ❌ | ✅ SOC 2 / GDPR compatible |

## Compliance Use Cases

1. **SOC 2 Audit** — Auditor asks: "Show me every action Agent X took in the last 90 days and why each was permitted."
2. **Incident Response** — Security team asks: "What state was the system in when Agent Y attempted to delete production data?"
3. **GDPR Right to Erasure** — User requests deletion. The ledger must support hard-delete of all user-associated vectors, ciphertext, and records while maintaining the audit chain integrity.

## Open Questions

- What is the optimal storage backend for append-only ledger entries at scale?
- How should ledger entries be compressed for long-term archival?
- What is the retention policy for ledger entries in different compliance regimes?

---

**Related:** [Exogram Architecture](https://exogram.ai/architecture) · [Security & Compliance](https://exogram.ai/security-and-compliance) · [Trust Center](https://exogram.ai/trust-center)

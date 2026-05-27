# RFC-02: Deterministic Admissibility Gateway

**Status:** Draft  
**Author:** Richard Ewing  
**Created:** 2026-05-27  
**Standard:** Exogram Protocol v1

---

## Abstract

This RFC proposes an execution gateway that processes go/no-go decisions at sub-runtime latencies, enabling autonomous AI agents to be safely deployed in production environments.

## Goal

Establish a deterministic admissibility gateway that evaluates whether an agent's proposed action should be permitted — using fast, binary policy rules instead of probabilistic LLM-as-a-judge approaches.

## Core Challenge

If the admissibility check takes too long, autonomous loops break down. Probabilistic LLM-as-a-judge approaches are too slow and unreliable. This RFC proposes moving governance checks to deterministic policy engines (fast, binary rules) to safely gate API and tool calls natively.

## Design Principles

1. **Deterministic** — The gateway must produce the same result given the same inputs. Zero randomness in enforcement.
2. **Sub-millisecond** — Admissibility evaluation must complete in under 1ms to avoid breaking autonomous execution loops.
3. **Fail-closed** — If the gateway cannot evaluate, the action is denied. Never default to allow.
4. **Zero Model Inference** — The judgment engine uses server-side code logic gates, not LLM inference. No probabilistic evaluation.
5. **Cryptographic Verification** — Each approved action generates a SHA-256 state hash and execution token.

## Architecture

```
Agent proposes action
    │
    ▼
┌─────────────────────────────┐
│  Policy Rule Engine         │  8 deterministic rules
│  (Python logic gates)       │  Zero LLM inference
└──────────┬──────────────────┘
           │
    ┌──────┴──────┐
    │             │
  ALLOW        BLOCK
    │             │
    ▼             ▼
Generate      Return 403
Exec Token    + Reason Code
    │
    ▼
SHA-256 State Hash
    │
    ▼
Commit Validation
```

## Evaluation Payload

```json
{
  "evaluation_request": {
    "agent_id": "agt_8f72c91a",
    "action": "WRITE_DATABASE",
    "target": "production_users_table",
    "raw_intent": "Update user email to new value",
    "context_hash": "sha256:...",
    "policy_version": "v1.4.2"
  },
  "evaluation_response": {
    "permitted": false,
    "reason": "RULE_04_VIOLATION: DESTRUCTIVE_ACTION_IN_PROTECTED_NAMESPACE",
    "compute_latency_ms": 0.07,
    "state_hash": "sha256:...",
    "execution_token": null
  }
}
```

## Performance Requirements

| Metric | Target | Current |
|--------|--------|---------|
| Median Compute Latency | < 1ms | 0.07ms |
| Sustained Throughput | > 100 RPS | 137 RPS |
| False Positive Rate | 0% | 0% |
| False Negative Rate | 0% | 0% |

## Open Questions

- How should policy rules be versioned and deployed without downtime?
- What is the governance model for adding/modifying policy rules?
- How should multi-agent chains be evaluated (agent A calls agent B)?

---

**Related:** [Exogram Architecture](https://exogram.ai/architecture) · [Protocol Overview](https://exogram.ai/protocol) · [Proving Ground](https://exogram.ai/proving-ground)

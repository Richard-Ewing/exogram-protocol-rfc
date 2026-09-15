# Exogram: Autonomous AI Governance & Context Architecture

**Mission:** AI that remembers reality. Durable, user-controlled context and deterministic execution authority for autonomous agents.

[![Status: Active Specification](https://img.shields.io/badge/Status-Active_Specification-blue.svg)](#) [![Category: Authority Runtime](https://img.shields.io/badge/Category-Authority_Runtime-green.svg)](#) [![Standard: Exogram Protocol v1](https://img.shields.io/badge/Standard-Exogram_Protocol_v1-purple.svg)](#)

Exogram is the deterministic authority runtime designed to sit beneath autonomous models. It provides the immutable record, capability boundaries, and verifiable execution state required to make autonomous systems operationally safe to deploy at scale.

**Strategic Stance:** Exogram does not replace model intelligence. Models are generative reasoning engines. Exogram enforces boundaries, continuity, and cryptographic truth beneath them.

---

## 1. The Core Problem

> **The reasoning capability of frontier models improves constantly. The auditability of their actions does not.**

Autonomous agents are routinely granted access to databases, payment gateways, and shell environments. However, when an agent hallucinates a parameter, attempts a bulk deletion, or enters an infinite execution loop, prompts cannot guarantee safety.

Traditional "AI memory" relies on similarity search across unstructured text vectors, leading to context poisoning, drift, and state desynchronization. Autonomous execution requires an **immutable ledger**. If an agent cannot verify what changed, what constraints exist, or what authority it holds, it becomes an operational hazard.

---

## 2. The Four-Layer Architecture

Exogram provides a continuous memory and verification substrate designed to organize, govern, and verify AI agent executions.

```
┌─────────────────────────────────────────────────────────────┐
│ Layer I: The Thinker (AI Inference & Proposal)              │
│ Probabilistic model generates action intent or tool payload │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer II: The Cognitive Filter (Persistent Knowledge Graph) │
│ Bounded context assembly via 2-hop BFS on SQL-backed ledger │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer III: The Gate (Action Authorization Runtime)           │
│ Sub-0.07ms deterministic invariant check (ALLOW / DENY)     │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer IV: The Proof (Cryptographic Audit Ledger)            │
│ Chained SHA-256 state hashes, immutable event ledger        │
└─────────────────────────────────────────────────────────────┘
```

### Layer I: The Thinker (AI Proposal)
Your model plans, reasons, and proposes what tool or API mutation to execute next.

### Layer II: The Cognitive Filter (Persistent Knowledge Graph)
Every fact your AI learns is stored as a signed, timestamped entry in an immutable ledger and knowledge graph. Exogram uses 2-hop BFS semantic search to eliminate "Lost in the Middle" syndrome. Prior state versions remain visible; context is structured, not hallucinated.

*(Explore the Live Interactive Knowledge Graph Substrate at [exogram.ai/rfc/0001](https://exogram.ai/rfc/0001))*

### Layer III: The Gate (Action Authorization)
Before any tool call executes, Exogram evaluates the request against compile-time policy rules, blocking dangerous mutations in sub-0.07ms without invoking another LLM.

### Layer IV: The Proof (Cryptographic Audit)
Every decision is cryptographically signed and chained. Regulators, developers, and auditors receive tamper-evident proof of why an agent acted and what evidence supported the decision.

---

## 3. The Execution Loop

Exogram intercepts the autonomous execution loop to guarantee persistence and deterministic trust.

**Unprotected Flow (High Risk, Unbounded Failure):**
```
Prompt ──► Model ──► Unvalidated Tool Mutation ──► Potential Silent Failure
```

**Governed Autonomy Flow (Verifiable, Continuous, Safe):**
```
Prompt ──► [Context Assembly] ──► Model ──► [Action Authorization Gateway] ──► [Immutable Audit Ledger] ──► Physical Tool Execution
```

---

## 4. Technical Schemas (RFC-0001 Specification)

### Action Authorization Request
When an agent attempts to execute an action, the payload is evaluated by the Exogram Authority Runtime before hitting production APIs:

```json
{
  "execution_request": {
    "agent_id": "agt_8f72c91a",
    "target_system": "aws_production_db",
    "action": "DROP_TABLE",
    "context_hash": "a1b2c3d4e5f67890abcdef...",
    "action_authorization": {
      "policy_verdict": "DENIED",
      "latency_ms": 0.054,
      "rule_violated": "SEC_RULE_04: NO_DESTRUCTIVE_MUTATIONS_ON_PROD_CLUSTER",
      "action_permitted": false
    }
  }
}
```

### Verified Performance Benchmarks

- **137 RPS** sustained throughput per node
- **0.07ms** deterministic enforcement latency
- **14** protocol invariants enforced
- **8** deterministic policy gates — zero probabilistic LLM inference in the critical execution path
- **Per-request audit telemetry**: `compute_latency_ms`, `agent_id`, `state_hash`, `verdict` recorded in SQLite WAL ledger
- **Fail-closed invariant**: Default deny under network degradation, timeouts, or policy conflicts

---

## 5. Why This Matters Now

Frontier models are converging in reasoning capability. The sustainable moat for autonomous systems is the persistent operational infrastructure beneath the model layer.

We are giving autonomous intelligence the keys to infrastructure without building deterministic brakes. Exogram bridges this gap by ensuring AI remembers what matters, understands what changed, and provides cryptographic proof behind every action.

---

## 6. Open Requests for Comment (RFCs)

We design in public. The Exogram protocol standards are documented in the open RFC series:

| RFC | Title | Status | Link |
|:---|:---|:---|:---|
| **RFC 0001** | Execution Authority Protocol for Agentic AI | **Active Specification** | [0001-exogram-execution-authority.md](0001-exogram-execution-authority.md) |
| **RFC-01** | The Persistent Context Schema (EXO-STATE) | **Draft** | [rfcs/rfc-01-persistent-context-schema.md](rfcs/rfc-01-persistent-context-schema.md) |
| **RFC-02** | Target Validation Gateway | **Draft** | [rfcs/rfc-02-target-validation-gateway.md](rfcs/rfc-02-target-validation-gateway.md) |
| **RFC-03** | The Auditable Ledger Format | **Draft** | [rfcs/rfc-03-auditable-ledger-format.md](rfcs/rfc-03-auditable-ledger-format.md) |

---

## Reference Implementation & Resources

- **Website**: [exogram.ai](https://exogram.ai) — AI that remembers reality
- **Web RFC-0001 Spec**: [exogram.ai/rfc/0001](https://exogram.ai/rfc/0001) — Interactive visual specification
- **Protocol Overview**: [exogram.ai/protocol](https://exogram.ai/protocol) — Visual architecture walkthrough
- **Product Overview**: [exogram.ai/product](https://exogram.ai/product) — Persistent context & memory features
- **How It Works**: [exogram.ai/how-it-works](https://exogram.ai/how-it-works) — The 6-step cognitive loop
- **Developers**: [exogram.ai/developers](https://exogram.ai/developers) — SDKs, APIs, and quickstart guides
- **Trust Center**: [exogram.ai/trust-center](https://exogram.ai/trust-center) — Security architecture & compliance matrix

---

## Contributing

We welcome architectural review, schema feedback, and RFC contributions from the agentic AI community:

- **Architectural Discussion** → [Open a GitHub Issue](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues)
- **Schema Corrections** → [Submit a Pull Request](https://github.com/Richard-Ewing/exogram-protocol-rfc/pulls)
- **Security Vulnerabilities** → See [SECURITY.md](SECURITY.md)

---

<p align="center">
  <sub>The protocol is open. The standard is vendor-neutral. The reference runtime is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

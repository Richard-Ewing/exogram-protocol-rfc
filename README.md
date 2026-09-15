# Exogram: Verifiable Reality & Memory Protocol for Large Language Models

**Mission:** AI that remembers reality. Durable, user-controlled context and deterministic execution authority for frontier models and autonomous agents.

[![Status: Active Specification](https://img.shields.io/badge/Status-Active_Specification-blue.svg)](#) [![Category: Authority Runtime](https://img.shields.io/badge/Category-Authority_Runtime-green.svg)](#) [![Standard: Exogram Protocol v1](https://img.shields.io/badge/Standard-Exogram_Protocol_v1-purple.svg)](#)

Exogram is an open protocol and reference runtime designed to anchor Large Language Models in persistent reality. It provides the immutable memory ledger, topological entity graph, epistemic sentence grounding, and deterministic execution boundaries required to make AI genuinely reliable across long-horizon work.

**Strategic Stance:** Exogram does not replace model intelligence. Frontier models (Claude, GPT, Gemini, Llama) are generative reasoning engines. Exogram enforces continuity, evidence attribution, and cryptographic truth beneath them.

---

## 1. The Core Problem: Why LLMs Need Reality

> **The reasoning capability of frontier models improves constantly. Their ability to remember reality across time does not.**

Frontier models excel within a single conversation window. But when applied to continuous work, software development, or enterprise operations, they suffer from fundamental architectural failures:

1. **Ephemeral Amnesia**: Every session starts blank or relies on traditional similarity search (RAG) that dumps disconnected text fragments into the prompt. This introduces high latency, heavy token tax, and semantic drift.
2. **Hallucinated Continuity**: Without temporal ground truth, models confuse project versions, hallucinate past agreements, and suffer from "Lost in the Middle" degradation.
3. **Unverifiable Reasoning**: Models present answers with uniform confidence, unable to prove which primary sources or verified facts justified their claims.
4. **Ungoverned Execution**: When granted agentic tool capabilities (APIs, databases, file writes), models execute probabilistic guesses against production endpoints without deterministic safety bounds.

---

## 2. The Four-Layer Architecture for LLM Reality & Autonomy

Exogram provides a continuous memory, grounding, and verification substrate designed to sit beneath any Large Language Model.

```
┌─────────────────────────────────────────────────────────────┐
│ Layer I: The Reasoning Engine (LLM Inference & Proposal)    │
│ Probabilistic model generates reasoning, text, or tool calls│
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer II: The Cognitive Filter (Temporal Entity Graph)       │
│ Bounded context assembly via 2-hop BFS on immutable ledger  │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer III: The Authority Runtime (Governed Autonomy Gate)   │
│ Sub-0.07ms deterministic invariant check (ALLOW / DENY)     │
└──────────────────────────────┬──────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ Layer IV: The Proof (Cryptographic State & Audit Chain)     │
│ Chained SHA-256 state hashes, immutable event ledger        │
└─────────────────────────────────────────────────────────────┘
```

### Layer I: The Reasoning Engine (LLM Inference)
Your chosen frontier model reasons, synthesizes, and proposes responses or tool mutations. The model focuses purely on synthesis; it is relieved of the burden of holding all ungrounded historical state in its raw context window.

### Layer II: The Cognitive Filter (Persistent Knowledge Graph & Epistemic Grounding)
Every fact learned across conversations and uploaded documents is stored as a signed, timestamped entry in an encrypted SQLite WAL ledger and topological entity graph.
- **Topological 2-Hop BFS**: Replaces unbounded cosine vector retrieval with bounded graph traversal, eliminating "Lost in the Middle" syndrome and context poisoning.
- **Epistemic Sentence Grounding**: Response claims are linked directly to underlying ledger entries with interactive citation inspection and confidence attribution.

*(Explore the Live Interactive Knowledge Graph Substrate at [exogram.ai/rfc/0001](https://exogram.ai/rfc/0001))*

### Layer III: The Authority Runtime (Governed Autonomy)
Before any tool call, code mutation, or API request executes, Exogram evaluates the request against compile-time policy rules, blocking destructive operations in sub-0.07ms without invoking another probabilistic LLM-as-a-judge.

### Layer IV: The Proof (Cryptographic State & Audit Chain)
Every response state and execution decision is cryptographically hashed and chained. Users, developers, and compliance auditors receive tamper-evident proof of the exact context state that justified the model's output.

---

## 3. Product & Ecosystem Integration

Exogram operationalizes this protocol across consumer, developer, and agentic workflows:

- **Exogram.ai LLM Workspace**: A minimal, visually calm AI environment (like Claude, Gemini, or Perplexity) featuring split-pane canvas editing, top source shelves, interactive citation popovers, and neural memory inspection.
- **FastMCP Distribution**: Universal Model Context Protocol server support (`npx exogram` or Python FastMCP) enabling Claude Desktop, Cursor, ChatGPT, and custom agents to natively read and write to Exogram's reality substrate.
- **Local Ledger Substrate**: Zero-cloud deployment mode via local SQLite WAL with PBKDF2/Fernet encryption at rest.

---

## 4. Technical Schemas (RFC-0001 Specification)

### Action Authorization Request
When an LLM attempts to execute an action, the payload is evaluated by the Exogram Authority Runtime before hitting physical infrastructure:

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

Frontier models are converging in baseline reasoning capability. The enduring differentiator for intelligent software is not the underlying model weight—it is the persistent operational infrastructure beneath the model.

Exogram bridges this gap: ensuring AI remembers what matters, understands what changed, and provides verifiable proof behind every answer and action.

---

## 6. Open Requests for Comment (RFCs)

We design in public. The Exogram protocol standards are documented in the open RFC series:

| RFC | Title | Status | Link |
|:---|:---|:---|:---|
| **RFC 0001** | Verifiable Reality & Execution Authority Protocol for Large Language Models | **Active Specification** | [0001-exogram-execution-authority.md](0001-exogram-execution-authority.md) |
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

We welcome architectural review, schema feedback, and RFC contributions from the AI community:

- **Architectural Discussion** → [Open a GitHub Issue](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues)
- **Schema Corrections** → [Submit a Pull Request](https://github.com/Richard-Ewing/exogram-protocol-rfc/pulls)
- **Security Vulnerabilities** → See [SECURITY.md](SECURITY.md)

---

<p align="center">
  <sub>The protocol is open. The standard is vendor-neutral. The reference runtime is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

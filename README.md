# Exogram Protocol

**An open specification for persistent memory, living knowledge graphs, and verifiable action boundaries in Large Language Models.**

[![Status: Active](https://img.shields.io/badge/Status-Active_Specification-emerald.svg)](#) [![Category: LLM Memory Protocol](https://img.shields.io/badge/Category-LLM_Memory_Protocol-blue.svg)](#) [![Standard: Exogram Protocol v1](https://img.shields.io/badge/Standard-Exogram_Protocol_v1-purple.svg)](#) [![Website](https://img.shields.io/badge/Website-exogram.ai-indigo.svg)](https://exogram.ai)

---

## 1. The Problem: AI Amnesia & Unbounded Action

You ask an AI assistant a question. It gives you a plausible answer. But it doesn't remember what you discussed yesterday. It doesn't know your preferences, your projects, or your team. And when granted the ability to call tools or interact with APIs, nothing prevents it from taking destructive actions based on a confident guess.

Every major language model suffers from two core flaws:
1. **Total Session Amnesia:** Frontier models become smarter inside a single conversation, but they wake up blank in the next. Context windows compress, truncate, and drop critical details. You waste hours re-prompting your background, tone, and constraints.
2. **Unverified Action Execution:** When models are connected to tools (databases, email, financial APIs), they evaluate textual plausibility rather than external ground truth. A single hallucination or indirect prompt injection can trigger irreversible real-world damage.

**The Exogram Protocol solves both problems.** Not by replacing the model, but by establishing a four-layer architecture beneath it: **persistent memory**, **living knowledge graphs**, and **verifiable action boundaries**.

---

## 2. The 4-Layer Personal AI Architecture

The Exogram Protocol structures modern AI applications into four explicit, decoupled layers:

```
┌─────────────────────────────────────────────────────────────┐
│ LAYER 1: INTELLIGENCE MODELS                                │
│ Claude 3.7 Sonnet · GPT-4.5 · Gemini 2.5 Flash · Local SLMs │
│ (Probabilistic reasoning, text generation, and planning)    │
└──────────────────────────────┬──────────────────────────────┘
                               │ Structured Intent & Synthesis
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ LAYER 2: ORCHESTRATION & CONNECTORS                         │
│ Model Context Protocol (MCP) · Google Drive · Gmail · Tools │
│ (Standard tool routing, execution pipelines, user interface)│
└──────────────────────────────┬──────────────────────────────┘
                               │ Verified Retrieval & State
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ LAYER 3: MEMORY VAULT & LIVING KNOWLEDGE GRAPH              │
│ Encrypted Fact Ledger · 2-Hop Graph Traversal · Dream Cycle │
│ (Deduplicated, cryptographically sealed, persistent context)│
└──────────────────────────────┬──────────────────────────────┘
                               │ 0.07ms Policy Invariants
                               ▼
┌─────────────────────────────────────────────────────────────┐
│ LAYER 4: SYSTEMS OF RECORD & VERIFIED ACTION BOUNDARIES     │
│ Databases · Payment APIs · Filesystems · User Hardware      │
│ (State hash verification, action authorization, audit trail)│
└─────────────────────────────────────────────────────────────┘
```

### Layer 1: Intelligence Models
The language model does what it does best: language comprehension, creative reasoning, synthesis, and planning. The protocol is completely vendor-agnostic and supports cloud frontier models (Claude, OpenAI, Gemini) and local SLMs (Phi-4, Gemma 2, Llama 3) with seamless provider failover.

### Layer 2: Orchestration & Connectors
Connectors bridge the AI to real work. The reference implementation standardizes on the **Model Context Protocol (MCP)**, allowing desktop clients (Claude Desktop, Cursor, Windsurf) and custom workflows to interact with user tools, files, and communications under explicit permission boundaries.

### Layer 3: Memory Vault & Living Knowledge Graph
Instead of dumping loosely related text chunks into the prompt via traditional vector search, Exogram maintains:
- **An Encrypted Fact Ledger:** SQLite WAL with AES-256 / Fernet encryption where every entry is a timestamped, deduplicated fact with decaying confidence unless reinforced.
- **A Topological Knowledge Graph:** Automatically wires extracted people, organizations, projects, and events into a 2-hop entity graph.
- **Epistemic Sentence Grounding:** Statements in the model's response are cited and linked to verified source evidence.
- **Autonomous Dream Cycles:** Background maintenance sweeps every 6 hours deduplicate entities, prune decayed associations, and reinforce verified relationships.

### Layer 4: Systems of Record & Verified Action Boundaries
When an AI proposes a state-changing action (database write, API transfer, file mutation), the request passes through a deterministic policy gate before touching production systems:
- **0.07ms CPU Latency:** Rules are evaluated in compiled code, not another slow LLM call.
- **State Hash Binding ($\mathcal{H}$):** Execution tokens are bound to a SHA-256 state hash at evaluation time. If underlying data shifts before execution, the token is invalidated to prevent race conditions.
- **Immutable Audit Trail:** Every decision, evaluation, and mutation produces a tamper-evident audit record.

---

## 3. The Reference Implementation

[Exogram.ai](https://exogram.ai) is the official reference implementation of this protocol:

- **AI Workspace (`/chat`):** A consumer and team conversational interface with zero amnesia, inline source citations, and an interactive 2-hop knowledge graph.
- **Model Context Protocol (MCP) Server:** Universal distribution for Claude Desktop and Cursor via `npx mcp-server-exogram` or Python FastMCP.
- **Local-First SQLite Vault:** Run 100% private, on-device memory ledgers with local models.

Explore the reference implementation at **[exogram.ai](https://exogram.ai)**.

---

## 4. Specification Documents

| Document | Title | Status |
| :--- | :--- | :--- |
| **[RFC 0001](0001-exogram-protocol-specification.md)** | Persistent Memory, Epistemic Grounding & Action Authorization | Active Standard |
| **[Layer 1 Guide](docs/layer-1-intelligence.md)** | Intelligence Models & Model Agnosticism | Informational |
| **[Layer 2 Guide](docs/cognitive-filter.md)** | Memory Vaults, Knowledge Graphs & The Cognitive Filter | Informational |
| **[Layer 3 Guide](docs/layer-3-orchestration.md)** | Orchestration, Connectors & Model Context Protocol | Informational |
| **[Layer 4 Guide](docs/layer-4-action-boundaries.md)** | Systems of Record & Verified Action Boundaries | Informational |
| **[Developer Tooling](docs/developer-agent-tooling.md)** | Python SDK, CLI & MCP Integration Patterns | Developer Guide |
| **[Full Stack Synthesis](docs/synthesis-the-full-stack.md)** | The Complete 4-Layer Personal AI Architecture | Architecture |

---

## 5. Quick Reference & Core Invariants

The protocol enforces 6 foundational invariants:

1. **The Provenance Law:** No fact is authoritative without verifiable source attribution.
2. **The Epistemic Grounding Law:** An inference cannot masquerade as an established truth.
3. **The Zero-Amnesia Law:** Core user preferences and entity relationships persist across sessions.
4. **The State Integrity Law:** Actions require state hash parity between evaluation and commit.
5. **The Deterministic Gate Law:** Tool actions are validated by compiled code, not probabilistic LLM calls.
6. **The User Sovereignty Law:** Users retain total cryptographic ownership, one-click export, and GDPR hard deletion rights.

---

## 6. Contributing & Community

- **Discussions:** [GitHub Discussions](https://github.com/Richard-Ewing/exogram-protocol-rfc/discussions)
- **Issues & Schema Updates:** [GitHub Issues](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues)
- **Security Disclosures:** [SECURITY.md](SECURITY.md)

---

<p align="center">
  <sub>The protocol is open. The standard is vendor-neutral. The reference implementation is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

# Exogram Protocol

**An open specification for persistent memory, grounded answers, and safe execution in Large Language Models.**

[![Status: Active](https://img.shields.io/badge/Status-Active_Specification-blue.svg)](#) [![Category: LLM Memory Protocol](https://img.shields.io/badge/Category-LLM_Memory_Protocol-green.svg)](#) [![Standard: Exogram Protocol v1](https://img.shields.io/badge/Standard-Exogram_Protocol_v1-purple.svg)](#)

---

## The Problem

You ask an AI a question. It gives you an answer. But it doesn't tell you where the answer came from. It doesn't remember what you told it yesterday. And if you give it the ability to take actions on your behalf, nothing stops it from doing something catastrophically wrong based on a confident guess.

Every major LLM has this problem. The models keep getting smarter inside a single conversation. But they don't accumulate knowledge about you across conversations. They don't connect the dots between what they know. They don't cite primary sources. And when they act, they act without guardrails.

Exogram is a protocol designed to fix these gaps. Not by replacing the model, but by putting a memory layer, a grounding layer, and an execution safety layer beneath it.

---

## What the Protocol Does

Exogram sits between the user and the language model. Every query passes through four layers before a response is generated:

```
┌───────────────────────────────────────────────────────────┐
│  Layer 1: Model Inference                                  │
│  The LLM reasons and generates a response.                 │
└────────────────────────────┬──────────────────────────────┘
                             ▼
┌───────────────────────────────────────────────────────────┐
│  Layer 2: Memory & Entity Graph                            │
│  Pulls verified facts and relationships from a personal    │
│  knowledge graph instead of relying on raw vector search.  │
└────────────────────────────┬──────────────────────────────┘
                             ▼
┌───────────────────────────────────────────────────────────┐
│  Layer 3: Authority Runtime                                │
│  Checks proposed actions against safety rules before       │
│  anything executes. No LLM involved in the safety check.   │
└────────────────────────────┬──────────────────────────────┘
                             ▼
┌───────────────────────────────────────────────────────────┐
│  Layer 4: Audit Trail                                      │
│  Cryptographic hash chain records what was known, what     │
│  was decided, and what evidence justified it.              │
└───────────────────────────────────────────────────────────┘
```

### Layer 1: Model Inference
The language model does what it does best. It reads, reasons, and generates text. Exogram doesn't constrain the model's intelligence. It constrains what the model is allowed to *do* with that intelligence.

### Layer 2: Memory & Entity Graph
This is the core differentiator. Instead of dumping loosely related text chunks into the prompt via traditional RAG, Exogram maintains a timestamped, encrypted ledger of verified facts and a topological entity graph connecting people, projects, decisions, events, and documents.

When you ask a question, the system traverses this graph to assemble bounded, relevant context. Your wife's birthday. Your deployment history. The last time a project failed integration tests and why. This context arrives pre-assembled so you never have to write a 300-word prompt just to get a useful answer.

Every claim in the response can be traced back to a specific ledger entry. The system calls this *epistemic sentence grounding*: individual statements in the model's output are linked to the evidence that supports them.

### Layer 3: Authority Runtime (Governed Autonomy)
When the model proposes an action (an API call, a database write, a file mutation), that action passes through a deterministic policy gate before it executes. The gate evaluates safety rules using code, not another LLM call. If the action violates a policy, it's blocked.

This matters because schema validators only check data structure, not intent. A syntactically valid `DROP TABLE` request passes JSON validation. The Authority Runtime catches it because it evaluates what the action *means*, not just whether it's well-formed.

### Layer 4: Audit Trail
Every response, every action decision, every context snapshot generates a SHA-256 hash chained to the previous state. This creates a tamper-evident record of what the model knew at the time it answered. Useful for compliance. Useful for debugging. Useful for the user who wants to understand *why* the AI said what it said.

---

## The Reference Implementation

Exogram.ai is the reference implementation of this protocol:

- **AI Workspace**: A conversational interface with persistent memory, source citations, inline evidence inspection, and a live knowledge graph you can explore.
- **FastMCP Server**: Universal Model Context Protocol distribution. Connect Claude Desktop, Cursor, ChatGPT, or your own agents to Exogram's memory substrate via `npx exogram` or Python FastMCP.
- **Local-First Option**: Deploy the memory ledger locally on SQLite WAL with PBKDF2/Fernet encryption. No cloud dependency required.

Try it at [exogram.ai](https://exogram.ai). Read the interactive specification at [exogram.ai/rfc/0001](https://exogram.ai/rfc/0001).

---

## RFCs

| RFC | Title | Status |
|:---|:---|:---|
| **0001** | [Persistent Memory, Epistemic Grounding & Execution Authority](0001-exogram-execution-authority.md) | Active |
| **01** | [Persistent Context Schema (EXO-STATE)](rfcs/rfc-01-persistent-context-schema.md) | Draft |
| **02** | [Target Validation Gateway](rfcs/rfc-02-target-validation-gateway.md) | Draft |
| **03** | [Auditable Ledger Format](rfcs/rfc-03-auditable-ledger-format.md) | Draft |

---

## Resources

- [exogram.ai](https://exogram.ai)
- [exogram.ai/rfc/0001](https://exogram.ai/rfc/0001) — Interactive visual spec
- [exogram.ai/how-it-works](https://exogram.ai/how-it-works) — Product walkthrough
- [exogram.ai/developers](https://exogram.ai/developers) — SDKs and API reference

---

## Contributing

- [Open an issue](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues) for architectural discussion
- [Submit a PR](https://github.com/Richard-Ewing/exogram-protocol-rfc/pulls) for schema corrections
- Security vulnerabilities → [SECURITY.md](SECURITY.md)

---

<p align="center">
  <sub>The protocol is open. The standard is vendor-neutral. The reference implementation is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

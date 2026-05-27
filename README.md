# Exogram: Persistent Infrastructure for Autonomous Intelligence

**Mission:** To make autonomous intelligence persistent and verifiable.

[![Status: Alpha Architecture](https://img.shields.io/badge/Status-Alpha_Architecture-blue.svg)](#) [![Category: Trust Infrastructure](https://img.shields.io/badge/Category-Execution_Trust_Infrastructure-green.svg)](#) [![Standard: Exogram Protocol v1](https://img.shields.io/badge/Standard-Exogram_Protocol_v1-purple.svg)](#)

Exogram is the persistent intelligence substrate designed to sit beneath autonomous models. It provides the memory, continuity, governance, and verifiable execution state required to make autonomous systems operationally safe to deploy at scale.

**Strategic Stance:** Exogram does not replace model intelligence. Models are incredible cognition engines. Exogram preserves operational continuity, governance, and trust across them. We are building the SSL certificate for agentic execution.

---

## 1. The Core Vulnerability

> **The intelligence of frontier models improves constantly, but the continuity of the context never does.**

We are entering a world where users and autonomous agents live across multiple language models, fragmented workflows, and disparate execution environments. Yet every AI product still starts from zero. Operational context is currently trapped inside vendor silos. 

The industry currently treats context as a user convenience. That is a critical miscalculation. As agents move from being passive chatbots to persistent, autonomous operators touching real infrastructure, passive memory ceases to be sufficient. 

What the industry currently calls "memory" is fundamentally inadequate. Autonomous execution requires an **auditable ledger**. If an autonomous system forgets its constraints, loses its operational history, or drops its permission boundaries as it moves between environments, it stops being reliable infrastructure. It becomes an operational hazard. 

---

## 2. The Four-Layer Architecture

Exogram is a comprehensive infrastructure stack designed to intercept, govern, and verify autonomous execution.

### Layer I: Persistent Context (The State Graph)
The foundational baseline that maintains identity, goals, and operational state across completely different models and platforms. Exogram unifies disconnected memory silos into a single, portable, and persistent state graph.

### Layer II: Dynamic Governance (The Policy Engine)
The policy layer that defines the rigid operational boundaries, permission rules, and execution constraints for any given agent. Translates human intent into deterministic operational boundaries.

### Layer III: Deterministic Admissibility (The Execution Gateway)
The runtime execution bouncer. Instead of asking if a probabilistic model *can* perform an action, this layer deterministically evaluates whether the execution *should* be allowed to occur at all, intercepting out-of-bounds actions before they hit your infrastructure.

### Layer IV: The Auditable Ledger (Memory v2)
An append-only, verifiable history of every action, context shift, and governance decision. It provides execution traceability, transforming passive AI memory into enterprise-grade accountability.

---

## 3. The Execution Loop

Exogram intercepts the standard AI execution loop to inject persistence and deterministic trust.

**Standard Flow (High Risk, Zero Memory):**
```
Prompt -> Model -> Execution -> Result
```

**Exogram Flow (Trusted, Continuous, Verifiable):**
```
Prompt -> [Exogram State Injection] -> Model -> [Exogram Admissibility Gateway] -> [Auditable Ledger Log] -> Execution -> Result
```

---

## 4. Technical Schemas (Alpha Drafts)

### The Admissibility Request
When an agent attempts to execute an action, it must pass through the Exogram Admissibility Gateway.

```json
{
  "execution_request": {
    "agent_id": "agt_8f72c91a",
    "target_system": "aws_production_db",
    "action": "DROP_TABLE",
    "context_hash": "a1b2c3d4e5f6...",
    "exogram_admissibility": {
      "policy_check": "FAILED",
      "reason": "VIOLATES_DYNAMIC_GOVERNANCE_RULE_04: NO_DESTRUCTIVE_ACTIONS_IN_PROD",
      "action_permitted": false
    }
  }
}
```

### Key Metrics

- **137 RPS** sustained throughput
- **0.07ms** deterministic enforcement latency
- **14** protocol invariants enforced
- **8** deterministic policy rules — zero LLM inference
- **Per-request telemetry**: `compute_latency_ms`, `agent_id`, `raw_intent` logged to immutable audit ledger
- Fail-closed under all error conditions

---

## 5. Why This Matters Now

As frontier models proliferate and capability converges, the strategic value shifts increasingly toward the persistent operational infrastructure sitting beneath the model layer.

We are giving autonomous intelligence the keys to the car without building the brakes. Today humans repeatedly adapt themselves to disconnected AI systems. Eventually, autonomous systems will adapt themselves to persistent, auditable human context.

---

## 6. Project Roadmap & RFCs

We are building in public. Below are the open Requests for Comment (RFCs) regarding the Exogram Protocol:

| RFC | Title | Status |
|-----|-------|--------|
| [RFC-01](rfcs/rfc-01-persistent-context-schema.md) | The Persistent Context Schema (EXO-STATE) | **Draft** |
| [RFC-02](rfcs/rfc-02-deterministic-admissibility-gateway.md) | Deterministic Admissibility Gateway | **Draft** |
| [RFC-03](rfcs/rfc-03-auditable-ledger-format.md) | The Auditable Ledger Format | **Draft** |

For access to the private alpha, or to contribute to the protocol design, contact the Exogram team.

---

## Links

- [Exogram.ai](https://exogram.ai) — Managed EAAP implementation
- [Protocol Overview](https://exogram.ai/protocol) — Visual architecture walkthrough
- [RFC-0001 (Web)](https://exogram.ai/rfc/0001) — Interactive spec
- [API Reference](https://exogram.ai/docs/api) — REST API documentation
- [Architecture](https://exogram.ai/architecture) — Governance architecture deep dive
- [Changelog](https://exogram.ai/changelog) — Release history
- [AI Governance Glossary](https://exogram.ai/glossary) — 27 defined terms
- [Learning Hub](https://exogram.ai/learn) — Educational guides
- [Comparison Hub](https://exogram.ai/compare) — Exogram vs 18 alternatives
- [Integration Guides](https://exogram.ai/integrations) — MCP, ChatGPT, LangChain, REST API
- [Production Readiness Analyzer](https://exogram.ai/analyze) — Code risk assessment

---

## Contributing

We welcome architectural feedback, schema corrections, and security reviews.

- **Architectural debate** → [Open a GitHub Issue](https://github.com/Richard-Ewing/exogram-protocol-rfc/issues)
- **Schema corrections** → [Submit a Pull Request](https://github.com/Richard-Ewing/exogram-protocol-rfc/pulls)
- **Security vulnerabilities** → See [SECURITY.md](SECURITY.md)

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting.

---

<p align="center">
  <sub>The protocol is open. The standard is free. The reference implementation is <a href="https://exogram.ai">Exogram.ai</a>.</sub>
</p>

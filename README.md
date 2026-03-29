# Exogram Protocol RFC

[Official Exogram Platform](https://exogram.ai)

## The Missing 4th Layer in AI Architecture

The industry has standardized around three layers: Models (intelligence), Memory (retrieval), and Orchestration (routing). But probabilistic entities are being given direct write-access to deterministic infrastructure (databases, APIs, payment gateways).

**The Exogram Protocol** defines the **Execution Authority Layer**. Sits explicitly between the Agentic Orchestrator and the Target Environment. It intercepts generated tool-call payloads, enforces mathematically deterministic constraints in 0.07ms, and permanently eliminates schema hallucination, TOCTOU state drift, and indirect prompt injection.

### Why Not Just Use Prompt Engineering or Constitutional AI?
Constitutional AI reduces the *probability* of a bad action. Execution Authority guarantees it deterministically. A perfectly safe prompt can still result in a hallucinated, destructive JSON payload.

### Core RFC Documents
- [0001: Execution Authority Protocol Specifications](./0001-exogram-execution-authority.md)

## Contributing
We welcome push requests and comments on the fundamental mathematical specifications of deterministic AI execution gating.

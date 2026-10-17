# Exogram Protocol (`RFC-0001`)

**The Open Architecture for Personal Neural Networks, Multi-Lab Agent Swarms, Interactive Living UI Tiles, and Deterministic AI Action Governance.**

[![Status: Active Standard](https://img.shields.io/badge/Status-Active_Specification-059669?style=for-the-badge)](https://exogram.ai)
[![Live Workspace](https://img.shields.io/badge/Live_Runtime-exogram.ai%2Fdashboard%2Fchat-6d28d9?style=for-the-badge)](https://exogram.ai/dashboard/chat)
[![Python SDK](https://img.shields.io/badge/Python_SDK-exogram--sdk-2563eb?style=for-the-badge)](https://github.com/Richard-Ewing/exogram-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-0f172a?style=for-the-badge)](#)

> ### ⚡ The 5-Second Summary
> **Standard AI chatbots suffer from three fatal flaws: they wake up with amnesia every session, they dump walls of dead Markdown instead of doing real work, and they break whenever a single model API rate-limits.**
>
> **Exogram** defines a closed-loop, non-linear architecture where four layers continuously feed one another:
> 1. **The Personal Neural Network (`Work` · `People` · `Life`)** — Multi-hop associative memory combining **OpenViking L0/L1/L2** clause pruning, **HippoRAG 2** spectral Personalized PageRank ($D^{-1/2} A D^{-1/2}$) hub-node damping, and **4-Way Reciprocal Rank Fusion (RRF)**.
> 2. **The 7-Lab Specialist Agent Swarm & Capability Router** — Parallel domain agents (`Dots`, `Claude`, `GrokBot`, `OpenClaw`, `Perplexity`, `Kimi`, `Hermes`) backed by **RouteLLM** capability gating and zero-downtime failover across Gemini, Claude, OpenAI, Grok, GitHub Models, Groq, Cerebras, SambaNova, NVIDIA NIM, and OpenRouter.
> 3. **AG-UI Turn Blackboard & Interactive Living Tiles** — Dual-track SSE streaming that compiles verified turn state into interactive UI deliverables (`action_draft`, `checklist`, `decision_matrix`, `places_court`, `comparison_table`).
> 4. **EAAP Deterministic Authority Kernel (`0.07ms`)** — Cryptographic SHA-256 state-hash verification and human-in-the-loop approval gates before any consequential tool action executes.

---

## 1. Closed-Loop Non-Linear Architecture

Unlike linear RAG pipelines (`Query -> Vector Search -> Prompt -> Text`), every layer in the Exogram Runtime informs and reconciles with every other layer during a single turn:

```text
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: LAYA PREFLIGHT & PERSONAL NEURAL NETWORK (Work · People · Life Spheres)       │
│  • OpenViking L0/L1/L2 Context Tiering: Entity-signature deduplication & clause prune  │
│  • HippoRAG 2 Spectral PPR: Symmetric degree damping 1/√((1+deg(u))(1+deg(v)))         │
│  • 4-Way Reciprocal Rank Fusion (k=60): Pinecone + Lexical + Layer-2 Graph + Profile   │
└───────────────────┬────────────────────────────────────────────────────▲───────────────┘
                    │ Privacy-Minimized Context Packet                   │ Post-Response
                    ▼                                                    │ Used/Available
┌────────────────────────────────────────────────────────────────────────┴───────────────┐
│ LAYER 2: 7-LAB SPECIALIST AGENT SWARM & ROUTELLM CAPABILITY POOL                       │
│  • Dots (Memory Graph Walker)   · Claude (Strategic Red-Team) · GrokBot (Counter-Audit)│
│  • OpenClaw (Live URL/DOM)      · Perplexity (Web Citations)  · Hermes (Action Stage)  │
│  • RouteLLM Capability Gating + 429 Cooldown Registry across 15+ Frontier & Free Pools │
└───────────────────┬────────────────────────────────────────────────────────────────────┘
                    │ Silent Inner Tool Loop (<think> & search chatter routed to Accordion)
                    ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 3: AG-UI TURN BLACKBOARD & INTERACTIVE LIVING TILES                              │
│  • Track A (Conversational Stream): Natural first-name intimacy, [1][2] citations      │
│  • Track B (Blackboard Compiler): Deterministic synthesis of action_draft, checklist,  │
│    decision_matrix, places_court, comparison_table, and Layer-3 Sandboxed Iframes      │
└───────────────────┬────────────────────────────────────────────────────────────────────┘
                    │ Consequential Action Dispatch
                    ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 4: EAAP DETERMINISTIC EXECUTION AUTHORITY KERNEL (0.07ms)                        │
│  • SHA-256 State-Hash Binding · Parameter Tamper Detection · Replay-Proof Tokens       │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. How Exogram Synthesizes Best-in-Class Open-Source Primitives

Exogram combines original runtime governance with proven algorithmic primitives from the open-source AI ecosystem:

| Stack Layer | Open-Source Inspiration | Exogram Production Implementation |
| :--- | :--- | :--- |
| **Context Tiering & Pruning** | [`volcengine/OpenViking`](https://github.com/volcengine/OpenViking) | **L0/L1/L2 Clause Pruning & Entity Signature Deduplication**: Strips unrelated composite memory clauses (e.g. media habits during a dinner prompt) and consolidates duplicate cards within the same `Work / People / Life` sphere. |
| **Multi-Hop Graph Recall** | [`OSU-NLP-Group/HippoRAG`](https://github.com/OSU-NLP-Group/HippoRAG) & [`getzep/graphiti`](https://github.com/getzep/graphiti) | **Spectral Personalized PageRank (PPR) Hub-Node Damping**: Treats the user's self-node as the teleportation origin and applies symmetric degree normalization $D^{-1/2} A D^{-1/2}$ with temporal decay (`computeDecay`). |
| **Capability-Aware Routing** | [`lm-sys/RouteLLM`](https://github.com/lm-sys/RouteLLM) & [`BerriAI/litellm`](https://github.com/BerriAI/litellm) | **Task-Profile Capability Gating & Cooldown Slots**: Isolates code-only models to `coding` turns, prioritizes high-throughput generalists (`Gemini`, `Groq`, `Cerebras`, `SambaNova`, `NVIDIA NIM`, `GitHub Models`), and extracts inline `<think>` blocks into `ThinkingAccordion`. |
| **Silent Tool Loops** | [`NousResearch/hermes-agent`](https://github.com/NousResearch/hermes-agent) | **Bounded Silent Tool Execution**: Caps inner tool rounds, routes intermediate search narration to `thinking_step`, and omits `tools` on the final synthesis pass to guarantee a complete human response. |
| **Interactive Living Tiles** | [`ag-ui-protocol/ag-ui`](https://github.com/ag-ui-protocol/ag-ui) & [`vercel-labs/json-render`](https://github.com/vercel-labs/json-render) | **Turn Blackboard Tile Synthesis**: Compiles schema-validated Living Tiles (`action_draft`, `checklist`, `decision_matrix`, `places_court`) directly from verified turn state even when failover models omit tool calls. |

---

## 3. Canonical Living Tile Schemas

Exogram standardizes six primary interactive **Living Tile** contracts rendered inline beneath the conversational response:

1. **`action_draft`** — Ready-to-send outbound email, Slack, or message reply pre-populated with recipient, subject, body, and 1-click EAAP-governed approval actions.
2. **`checklist`** — Stateful, interactive execution board with checkable items, category tags, and persistent session state across follow-up turns.
3. **`decision_matrix`** — Multi-option weighted evaluation table with 0–100 differentiated scores, pros/cons, and explicit `Sourced` vs. `Estimated` provenance badges.
4. **`places_court`** — Verified local venue cards with ratings, price tiers, neighborhood tags, and sanitized Google Maps / website deep links.
5. **`comparison_table`** — Structured side-by-side matrix for technical, product, or financial comparisons.
6. **`generative_ui` (Layer-3 Sandbox)** — CSP-locked, cookie/storage-isolated iframe runtime for custom interactive calculators and visual simulations.

---

## 4. Specification Documents

| Document | Title | Status |
| :--- | :--- | :--- |
| **[RFC 0001](0001-exogram-protocol-specification.md)** | Persistent Memory, Epistemic Grounding & Action Authorization | Active Standard |
| **[Layer 1 Guide](docs/layer-1-intelligence.md)** | Intelligence Models, Capability Routing & Multi-Lab Failover | Informational |
| **[Layer 2 Guide](docs/layer-2-orchestration-connectors.md)** | Specialist Agent Swarms, FastMCP Connectors & AG-UI Streaming | Informational |
| **[Layer 3 Guide](docs/layer-3-memory-vault-graph.md)** | Personal Neural Network, OpenViking Pruning & HippoRAG PPR | Informational |
| **[Layer 4 Guide](docs/layer-4-action-boundaries.md)** | EAAP State-Hash Verification & Verified Action Boundaries | Informational |
| **[Developer Tooling](docs/developer-agent-tooling.md)** | Python SDK, CLI & MCP Integration Patterns | Developer Guide |
| **[Platform Architecture](docs/enterprise-ai-companies.md)** | Modern Platform & Developer Integration Patterns | Architecture |
| **[Full Stack Synthesis](docs/synthesis-the-full-stack.md)** | The Complete 4-Layer Personal AI Architecture | Architecture |

---

## 5. Six Core Protocol Invariants

1. **The Provenance Law:** Every retrieved claim and external web fact carries explicit source attribution (`[1]`, `[2]`, `Memory Vault`, or `Live Web`).
2. **The Per-Agent Privacy Law:** External web-scraping agents (`OpenClaw`, `Perplexity`) receive privacy-minimized queries stripped of private family and vault identifiers.
3. **The Zero-Amnesia Law:** Verified entities and relationships persist across sessions inside the 3-Sphere Personal Neural Network (`Work`, `People`, `Life`).
4. **The Post-Response Reconciliation Law:** The Context Inspector (`Used` vs. `Available`) reconciles against the final assistant response so unused memories never masquerade as active influences.
5. **The Deterministic Gate Law:** Consequential tool actions are gated by compiled EAAP state-hash verification (`0.07ms`), never by a probabilistic LLM judge.
6. **The User Sovereignty Law:** Users retain full cryptographic ownership, one-click export, session-only preference sliders, and hard-delete rights.

---

<p align="center">
  <sub>Architected by <a href="https://github.com/Richard-Ewing">Richard Ewing</a> · Live Production Workspace at <a href="https://exogram.ai/dashboard/chat">exogram.ai</a></sub>
</p>

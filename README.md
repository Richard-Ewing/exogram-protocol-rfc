# Exogram Protocol (`RFC-0001`)

**The Open Architecture Specification for Infinite-Hop Personal Neural Networks, Two-Tier Privacy Routing, A2UI Composable Living Tiles, and Instinct Action Governance.**

[![Status: Active Standard](https://img.shields.io/badge/Status-Active_Specification_v5-059669?style=for-the-badge)](https://exogram.ai)
[![Live Workspace](https://img.shields.io/badge/Live_Runtime-exogram.ai%2Fdashboard%2Fchat-4C2B4B?style=for-the-badge)](https://exogram.ai/dashboard/chat)
[![Python & TS SDK](https://img.shields.io/badge/Open_Core_SDK-exogram--sdk-2563eb?style=for-the-badge)](https://github.com/Richard-Ewing/exogram-sdk)
[![License: MIT](https://img.shields.io/badge/License-MIT-201B20?style=for-the-badge)](#)

> **🚀 Looking for the Runnable Python/TS SDK, FastMCP Server & 30-Second Local/Cloud Quickstart?** Star and clone **[Richard-Ewing/exogram-sdk](https://github.com/Richard-Ewing/exogram-sdk)**.

<p align="center">
  <img src="docs/assets/knowledge-graph-viz.png" alt="Exogram Plum Mineral AI Workspace & Infinite-Hop Personal Neural Network" width="100%" />
</p>

> ### ⚡ The 5-Second Summary
> **Standard AI assistants wake up with total amnesia on every new chat, dump walls of static Markdown instead of executing real work, and lack cryptographic isolation between private personal facts and public tool calls.**
>
> **Exogram Protocol (Master Plan v5)** defines a closed-loop personal intelligence and governed execution architecture across five core subsystems:
> 1. **Personal Neural Network (`Work · People · Life`)** — Infinite-Hop Associative Spreading Activation ($\text{decay}=0.72$, $1/\sqrt{\text{deg}}$ hub damping) + **HippoRAG 2** Spectral Personalized PageRank ($D^{-1/2} A D^{-1/2}$) + **4-Way Reciprocal Rank Fusion (RRF)** + **3-Horizon Episodic Memory** (`ephemeral_episode` 36h TTL, `recurring_event` `RRULE:FREQ=YEARLY`, `durable_trait`) + Read-Time Scalar Conflict Supersession + Instant User Correction (`/api/memory/undo`).
> 2. **Two-Tier Inference Gateway & Laya `<15ms` Deterministic Fast-Path** — `PERSONAL` subtasks route exclusively to Paid Gemini 3.8 Flash / 2.5 Pro; `PUBLIC_ONLY` subtasks pass through `stripVaultAndPiiFromPublicSubtask` + `compressPublicContextTokens` before routing to the Free-Token Pool. Laya resolves vault subjects, intent, and domain in `<15ms` in-memory for `<= 1.6s` P50 TTFT.
> 3. **6-Point Agent Contract & 6 Honest Kernels** — `Neural Graph Kernel`, `Generative UI Kernel`, `Live Web & Places Scout`, `Action & Draft Kernel`, `Analytical Synthesis Kernel`, and `Grounded Citation Kernel` with Post-Synthesis Citation Verification (`verifyAgentContributionsAgainstTurnOutput` — only genuinely cited kernels earn `Complete · Cited`).
> 4. **8–12 Semantic Tool Selector & A2UI Composable Living Tile Engine** — Scopes outbound tools to 5 core meta-tools (`render_live_widget`, `search_memory_vault`, `update_memory_vault`, `find_tool`, `extract_public_page_records`) + 5–7 semantic tools wrapped in normalized provenance envelopes (`provenance.untrusted_content`, `residual_unknowns`). Renders 13 schema-validated Living Tiles (`action_draft`, `checklist`, `decision_matrix`, `curated_places`, `comparison_table`, `retail_deals_tile`, `media_watch_tile`, `occasion_countdown_tile`, `memory_undo_tile`, `agent_hud_tile`, `branded_diagram_tile`, `hyperframes_video_tile`, `instinct_computer_tile`) with `validateTileSpecProvenance` and AG-UI progressive JSON patching.
> 5. **Instinct Autonomous Operator & `0.07ms` Pre-Mutation Gate** — Combines `bhouvana/Instinct` (`evaluateInstinctPreMutationGate` pre-mutation judgment gate on Vault writes), `Merit-Systems/OpenInstinct` (`[Approve Step]` and `[Take Over]` human-on-the-loop sentinel controls), `mariagorskikh/open-instinct` (`Household` vs. `Work` A2A scope), and SHA-256 state-hash execution tokens ($C_{tok}$).

---

## 1. Closed-Loop Non-Linear Architecture (Master Plan v5)

Unlike linear RAG pipelines (`Query -> Cosine Search -> Prompt -> Static Text`), every layer in the Exogram Runtime informs, constrains, and reconciles with every other layer within a single turn:

```text
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 1: LAYA <15ms DETERMINISTIC FAST-PATH & TWO-TIER INFERENCE GATEWAY                 │
│  • Laya Preflight: In-memory vault subject, intent & sphere resolution in <15ms          │
│  • Subtask Data Policy: PERSONAL -> Paid Gemini 3.8 Flash / 2.5 Pro (Zero Training)      │
│  • PUBLIC_ONLY -> stripVaultAndPiiFromPublicSubtask + compressPublicContextTokens        │
└───────────────────┬──────────────────────────────────────────────────────▲───────────────┘
                    │ Scoped Context Packet & 8-12 Semantic Tools          │ Post-Response
                    ▼                                                      │ Citation Check
┌──────────────────────────────────────────────────────────────────────────┴───────────────┐
│ LAYER 2: 6-POINT AGENT CONTRACT, 6 HONEST KERNELS & SEMANTIC TOOL SELECTOR               │
│  • Neural Graph Kernel       · Generative UI Kernel     · Live Web & Places Scout        │
│  • Action & Draft Kernel     · Analytical Synthesis     · Grounded Citation Kernel       │
│  • 5 Core Meta-Tools + 5-7 Matched Tools wrapped in provenance.untrusted_content         │
└───────────────────┬──────────────────────────────────────────────────────────────────────┘
                    │ Associative Memory Traversal & Conflict Supersession
                    ▼
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 3: INFINITE-HOP PERSONAL NEURAL NETWORK (Work · People · Life Spheres)             │
│  • Infinite-Hop Spreading Activation (decay=0.72, 1/√deg hub damping, 5 iterations)      │
│  • HippoRAG 2 Spectral PPR (D⁻¹/² A D⁻¹/²) + 4-Way Reciprocal Rank Fusion (k=60)         │
│  • 3-Horizon Episodic Lifecycle (36h TTL · RRULE:FREQ=YEARLY · durable_trait) + Undo     │
└───────────────────┬──────────────────────────────────────────────────────────────────────┘
                    │ Progressive AG-UI Patching & Consequential Action Dispatch
                    ▼
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ LAYER 4: A2UI LIVING TILE ENGINE, INSTINCT OPERATOR & 0.07ms EXECUTION KERNEL            │
│  • 13 Schema-Validated Living Tiles + validateTileSpecProvenance + Claim Entailment      │
│  • Instinct Pre-Mutation Gate (bhouvana/Instinct) + [Approve Step] / [Take Over]         │
│  • Household vs. Work A2A Trust Boundaries + 0.07ms SHA-256 State-Hash Tokens (C_tok)    │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. How Exogram Synthesizes Best-in-Class Open-Source Primitives

Exogram unites original cryptographic action governance with peer-reviewed algorithmic primitives across memory, routing, and generative interfaces:

| Stack Layer | Architectural Primitive | Exogram Production Implementation |
| :--- | :--- | :--- |
| **Infinite-Hop Graph Recall** | Associative Spreading Activation & [`OSU-NLP-Group/HippoRAG`](https://github.com/OSU-NLP-Group/HippoRAG) | **Infinite-Hop Spreading Activation ($\text{decay}=0.72$) & Spectral PPR ($D^{-1/2} A D^{-1/2}$)**: Traverses multi-hop entity connections across `Work`, `People`, and `Life` with $1/\sqrt{\text{deg}}$ hub-node damping so high-degree self/venture hubs never drown out specific personal facts. |
| **Context Tiering & Pruning** | [`volcengine/OpenViking`](https://github.com/volcengine/OpenViking) | **L0/L1/L2 Clause Pruning & Mega-Topic Cap**: Strips unrelated composite memory clauses, enforces read-time scalar conflict supersession (latest home location, acreage, or schedule wins), and caps work/venture mega-topics during personal turns. |
| **Two-Tier Privacy Routing** | [`lm-sys/RouteLLM`](https://github.com/lm-sys/RouteLLM) & Subtask Data Policy | **`PERSONAL` vs. `PUBLIC_ONLY` Gateway**: Routes private vault reasoning exclusively to zero-retention Paid Gemini 3.8 Flash / 2.5 Pro while sanitizing `PUBLIC_ONLY` subtasks via `stripVaultAndPiiFromPublicSubtask` before calling the multi-provider pool. |
| **A2UI Living Tiles & Diagrams** | [`ag-ui-protocol/ag-ui`](https://github.com/ag-ui-protocol/ag-ui), [`cathrynlavery/diagram-design`](https://github.com/cathrynlavery/diagram-design), [`heygen-com/hyperframes`](https://github.com/heygen-com/hyperframes) | **Progressive JSON Patching & Provenance Validation**: Streams 13 interactive Living Tiles including publication-grade Plum Mineral SVG diagrams (`branded_diagram_tile`) and deterministic 30fps HTML/SVG video briefings (`hyperframes_video_tile`). |
| **Instinct Autonomous Operator** | [`bhouvana/Instinct`](https://github.com/bhouvana/Instinct), [`Merit-Systems/OpenInstinct`](https://github.com/Merit-Systems/OpenInstinct), [`mariagorskikh/open-instinct`](https://github.com/mariagorskikh/open-instinct) | **Pre-Mutation Judgment Gate & Human-on-the-Loop Sentinel**: Evaluates vault writes via `evaluateInstinctPreMutationGate`, enforces `Household` vs. `Work` A2A boundaries, and requires `[Approve Step]` / `[Take Over]` plus $0.07\text{ms}$ $C_{tok}$ tokens for irreversible actions. |

---

## 3. Canonical A2UI Composable Living Tile Schemas

Exogram standardizes **13 schema-validated Living Tile contracts** rendered inline via `render_live_widget` and verified by `validateTileSpecProvenance` before reaching the workspace:

1. **`action_draft` (`action_draft_tile`)** — Ready-to-send outbound email, calendar invite, or message pre-populated with recipient, subject, body, and 1-click $C_{tok}$-governed approval.
2. **`checklist` (`checklist_tile`)** — Stateful, interactive execution board with checkable items, owner tags, and persistent state across turns (blocked on simple factual media lookups).
3. **`decision_matrix`** — Multi-option weighted evaluation table with differentiated 0–100 scores, tradeoffs, and explicit `Sourced` vs. `Estimated` provenance badges.
4. **`curated_places`** — Verified local venue cards with ratings, price tiers, neighborhood tags, and sanitized Google Maps / website deep links.
5. **`comparison_table`** — Structured side-by-side matrix for technical, product, or household comparisons.
6. **`retail_deals_tile`** — Grounded product and retail deal cards requiring verified price and merchant provenance.
7. **`media_watch_tile`** — Streaming availability, release status, and watch-queue cards for films, series, and books.
8. **`occasion_countdown_tile`** — Recurring anniversary, birthday, and milestone countdown cards backed by `RRULE:FREQ=YEARLY` episodic horizons.
9. **`memory_undo_tile`** — Instant epistemic correction card bound to `/api/memory/undo` so users can revert or supersede any vault assumption in one click.
10. **`agent_hud_tile`** — Transparent execution telemetry showing which of the 6 Honest Kernels ran and which earned `Complete · Cited` status.
11. **`branded_diagram_tile`** — Editorial SVG/HTML diagrams (`architecture`, `workflow`, `timeline`, `comparison`, `concept_map`, `property_zone_map`) rendered in Exogram's Plum Mineral palette (`#FAF7F2`, `#201B20`, `#4C2B4B`, `#AEBD9A`).
12. **`hyperframes_video_tile`** — Frame-accurate 30fps HTML/CSS/SVG motion briefings with `window.__renderFrame(frameIndex)` scrubbing.
13. **`instinct_computer_tile`** — Stateful browser/errand operator tile with step-by-step trajectory inspection, `[Approve Step]`, and `[Take Over]` controls.

---

## 4. Specification Documents

| Document | Title | Status |
| :--- | :--- | :--- |
| **[RFC 0001](0001-exogram-protocol-specification.md)** | Infinite-Hop Personal Neural Network, Epistemic Grounding & Instinct Action Governance | Active Standard (v5) |
| **[RFC 0002](0002-intent-based-permissioning.md)** | Personal & Workspace Scope Isolation (`PERSONAL` vs. `PUBLIC_ONLY` & `Household` vs. `Work` A2A) | Active Standard (v5) |
| **[RFC 0003](0003-cryptographic-execution-tokens.md)** | Cryptographic Execution Tokens ($C_{tok}$), Instinct Sentinel Gates & Instant Undo | Active Standard (v5) |
| **[Layer 1 Guide](docs/layer-1-intelligence.md)** | Two-Tier Inference Gateway (`PERSONAL` vs. `PUBLIC_ONLY`) & Laya `<15ms` Deterministic Preflight | Architecture |
| **[Layer 2 Guide](docs/layer-2-orchestration-connectors.md)** | 6-Point Agent Contract, 6 Honest Kernels, 8–12 Semantic Tool Selector & FastMCP | Architecture |
| **[Layer 3 Guide](docs/layer-3-memory-vault-graph.md)** | Infinite-Hop Associative Spreading Activation, HippoRAG 2 Spectral PPR & 3-Horizon Memory | Architecture |
| **[Layer 4 Guide](docs/layer-4-action-boundaries.md)** | A2UI Composable Living Tiles, Provenance Validator, Instinct Gate & `0.07ms` $C_{tok}$ Kernel | Architecture |
| **[Developer Tooling](docs/developer-agent-tooling.md)** | Official Python SDK (`pip install exogram`), FastMCP Server (`--local` SQLite WAL + Cloud) | Developer Guide |
| **[Platform Architecture](docs/enterprise-ai-companies.md)** | Governed Personal & Workspace AI Integration Patterns | Architecture |
| **[Full Stack Synthesis](docs/synthesis-the-full-stack.md)** | Mathematical & Systems Synthesis of the 4-Layer Master Plan v5 Stack | Architecture |
| **[RFC-01 Schema](rfcs/rfc-01-persistent-context-schema.md)** | `EXO-STATE`: Portable 3-Horizon Personal Context & Conflict Supersession Schema | Draft Standard |
| **[RFC-02 Gateway](rfcs/rfc-02-target-validation-gateway.md)** | Deterministic `0.07ms` Target Validation Gateway & Instinct Pre-Mutation Gate | Draft Standard |
| **[RFC-03 Ledger](rfcs/rfc-03-auditable-ledger-format.md)** | Chained Audit Ledger (`turn_traces`), Provenance Envelopes & `/api/memory/undo` | Draft Standard |

---

## 5. Six Core Protocol Invariants

1. **The Claim-Predicate Provenance Law:** Every retrieved claim and external fact carries explicit source attribution (`[1]`, `[2]`, `Memory Vault`, or `Live Web`), and context items only promote to `Used` when `scoreClaimPredicateEntailment` confirms predicate-level overlap.
2. **The Two-Tier Subtask Privacy Law:** `PERSONAL` subtasks never touch third-party free pools; `PUBLIC_ONLY` subtasks are scrubbed by `stripVaultAndPiiFromPublicSubtask` before leaving the personal boundary.
3. **The Infinite-Hop Zero-Amnesia Law:** Entities and relationships across `Work`, `People`, and `Life` are traversed via Infinite-Hop Associative Spreading Activation ($\text{decay}=0.72$, $1/\sqrt{\text{deg}}$ hub damping) and governed by 3-Horizon Episodic Memory TTLs.
4. **The Honest Kernel Attribution Law:** Only the 6 first-party kernels (`Neural Graph Kernel`, `Generative UI Kernel`, `Live Web & Places Scout`, `Action & Draft Kernel`, `Analytical Synthesis Kernel`, `Grounded Citation Kernel`) are dispatched, and `verifyAgentContributionsAgainstTurnOutput` ensures only genuinely cited kernels show `Complete · Cited`.
5. **The Instinct & `0.07ms` Deterministic Gate Law:** Vault writes pass through `evaluateInstinctPreMutationGate`, and external actions require SHA-256 state-hash execution tokens ($C_{tok}$) plus `[Approve Step]` / `[Take Over]` sentinel controls on irreversible steps.
6. **The Instant Correction & Sovereignty Law:** Users hold one-click epistemic undo (`/api/memory/undo`), local-first SQLite WAL portability, and cryptographic hard-delete rights at all times.

---

<p align="center">
  <sub>Architected by <a href="https://github.com/Richard-Ewing">Richard Ewing</a> · Runnable SDK at <a href="https://github.com/Richard-Ewing/exogram-sdk">Richard-Ewing/exogram-sdk</a> · Live Workspace at <a href="https://exogram.ai/dashboard/chat">exogram.ai</a></sub>
</p>

# Layer 2: 6-Point Agent Contract, 6 Honest Kernels & 8–12 Semantic Tool Selector

> ### ⚡ The 2-Second Summary
> Flooding an LLM with 50+ tools degrades reasoning accuracy and invites prompt injection. **Layer 2** scopes every turn to **8–12 semantically matched tools**, wraps external tool outputs in **`provenance.untrusted_content`** envelopes, and orchestrates **6 Honest First-Party Kernels** whose contributions are verified against the final turn citations.

---

## 1. Abstract

Layer 2 (`agent_swarm_router.ts` and `tool_discovery.ts`) governs how intelligence models interact with tools, external data sources, and specialized execution kernels.

Instead of exposing monolithic tool catalogs or opaque third-party bot personas, Layer 2 enforces three architectural guarantees:
1. **The 6-Point Agent Contract & 6 Honest Kernels:** Every kernel has a transparent, first-party architectural role and must pass post-synthesis citation verification (`verifyAgentContributionsAgainstTurnOutput`) to be marked `Complete · Cited`.
2. **The 8–12 Semantic Tool Selector:** Outbound tool declarations are dynamically scoped to 5 core meta-tools plus 5–7 semantically matched tools (`<= 12` per turn).
3. **Normalized Provenance Envelopes:** All external tool results carry explicit `provenance.untrusted_content` and `residual_unknowns` metadata.

---

## 2. The 6 Honest First-Party Kernels (`agent_swarm_router.ts`)

Exogram dispatches six specialized first-party kernels under the **6-Point Agent Contract**:

| Kernel Name | Primary Responsibility | Subtask Policy | Citation & Verification Contract |
| :--- | :--- | :--- | :--- |
| **`Neural Graph Kernel`** | Traverses the Infinite-Hop Personal Neural Network (`Work · People · Life`), applies HippoRAG 2 Spectral PPR, and resolves scalar conflicts. | `PERSONAL` | Claims must pass `scoreClaimPredicateEntailment` to promote from `Available` to `Used`. |
| **`Generative UI Kernel`** | Synthesizes and patches the 13 A2UI Composable Living Tiles (`branded_diagram_tile`, `hyperframes_video_tile`, `decision_matrix`, etc.). | `PERSONAL` | Validated by `validateTileSpecProvenance` and `rescueMalformedWidgetEnvelope`. |
| **`Live Web & Places Scout`** | Executes PII-scrubbed public web search, venue lookups, and `extract_public_page_records`. | `PUBLIC_ONLY` | Outputs wrapped in `provenance.untrusted_content`; verified via `[1]`, `[2]` citations. |
| **`Action & Draft Kernel`** | Prepares governed outbound communications (`action_draft_tile`), calendar blocks, and `instinct_computer_tile` trajectories. | `PERSONAL` | Gated by `[Approve Step]` / `[Take Over]` and $0.07\text{ms}$ $C_{tok}$ tokens. |
| **`Analytical Synthesis Kernel`** | Performs multi-constraint reasoning, weighted scoring, and financial/technical comparisons. | `PERSONAL` | Differentiates `Sourced` vs. `Estimated` cells in `decision_matrix` and `comparison_table`. |
| **`Grounded Citation Kernel`** | Audits claim-predicate overlap between retrieved context items and the final assistant response. | `PERSONAL` | Runs `verifyAgentContributionsAgainstTurnOutput` so only genuinely cited kernels show `Complete · Cited`. |

### Post-Synthesis Citation Verification
In conventional multi-agent UIs, every dispatched agent claims credit even if its output was ignored. In Exogram, `verifyAgentContributionsAgainstTurnOutput` inspects the final synthesized response and Living Tiles after generation:
- Kernels whose retrieved records or artifacts appear with predicate-level entailment in the turn output receive **`Complete · Cited`**.
- Kernels that executed in standby or whose candidate facts were not needed are honestly marked **`Standby · Uncited`**.

---

## 3. The 8–12 Semantic Tool Selector (`tool_discovery.ts`)

Before calling the foundation model, `tool_discovery.ts` selects at most **12 tools** for the outbound `functionDeclarations` payload:

### 3.1 The 5 Core Always-Available Meta-Tools
1. `render_live_widget` — Emits any of the 13 schema-validated A2UI Composable Living Tiles.
2. `search_memory_vault` — Queries the Infinite-Hop Personal Neural Network across `Work`, `People`, and `Life`.
3. `update_memory_vault` — Proposes a 3-Horizon episodic or durable memory mutation (gated by `evaluateInstinctPreMutationGate`).
4. `find_tool` — Dynamically expands domain-specific FastMCP connectors on demand if the turn requires a specialized integration.
5. `extract_public_page_records` — Sandboxed extraction of structured entities, prices, or venues from public web pages.

### 3.2 5–7 Semantically Matched Domain Tools
Based on Laya's `<15ms` intent resolution, 5 to 7 additional FastMCP tools (Gmail, Google Calendar, Google Drive, Editorial SVG Diagram Engine, HyperFrames Video Composer, or Instinct Browser Operator) are attached. Crucially, core tools and Living Tiles are **never** gated behind brittle keyword regexes; the model decides tool invocations natively via System 2 reasoning.

---

## 4. Normalized Provenance Envelopes

Every tool response returning into the reasoning loop is wrapped in a standardized provenance envelope:

```json
{
  "tool_name": "extract_public_page_records",
  "status": "ok",
  "data": {
    "venue_name": "Osteria Fiorella",
    "rating": 4.8,
    "price_tier": "$$$"
  },
  "provenance": {
    "source_type": "public_web",
    "untrusted_content": true,
    "citation_id": "web-01",
    "fetched_at": "2026-10-19T22:15:00Z"
  },
  "residual_unknowns": [
    "Private patio availability for groups over 6 requires direct phone confirmation."
  ]
}
```

- **`provenance.untrusted_content`:** Prevents indirect prompt injections inside scraped web pages from invoking `update_memory_vault` or mutating connectors.
- **`residual_unknowns`:** Explicitly surfaces what the tool could *not* verify so the assistant preserves epistemic honesty instead of guessing.

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [RFC 0002: Intent-Based Permissioning & Scope Isolation](../0002-intent-based-permissioning.md)
- [Layer 3: Infinite-Hop Personal Neural Network & 3-Horizon Memory](layer-3-memory-vault-graph.md)
- [Layer 4: A2UI Living Tiles, Instinct Operator & 0.07ms Action Boundaries](layer-4-action-boundaries.md)

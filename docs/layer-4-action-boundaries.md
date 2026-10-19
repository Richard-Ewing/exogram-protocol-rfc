# Layer 4: A2UI Composable Living Tiles, Instinct Operator & `0.07ms` Action Boundaries

> ### ⚡ The 2-Second Summary
> An AI that knows you should get real work done—not just output text. **Layer 4** compiles verified turn context into **13 A2UI Composable Living Tiles**, validates every tile via **`validateTileSpecProvenance`**, protects the Memory Vault with the **Instinct Pre-Mutation Gate**, and governs external actions with **`[Approve Step]` / `[Take Over]`** sentinel controls and **`0.07ms`** state-hash tokens ($C_{tok}$).

---

## 1. Abstract

Layer 4 is where reasoning becomes tangible output and governed action. In Master Plan v5, Layer 4 unites three deterministic subsystems:
1. **A2UI Composable Living Tile Engine & Provenance Validator (`tile_spec_validator.ts`, `ag_ui_protocol.ts`):** Streams progressive, interactive UI components inline—including editorial SVG diagrams (`branded_diagram_tile`) and 30fps motion briefings (`hyperframes_video_tile`)—while blocking ungrounded prices, fabricated ratings, or placeholder checklists.
2. **Instinct Pre-Mutation Judgment Gate (`bhouvana/Instinct` in `instinct_operator.ts`):** Evaluates candidate memory writes (`evaluateInstinctPreMutationGate`) before they touch persistent storage.
3. **Human-on-the-Loop Action Sentinel & `0.07ms` $C_{tok}$ Kernel (`Merit-Systems/OpenInstinct` & `mariagorskikh/open-instinct`):** Enforces `Household` vs. `Work` A2A boundaries, `[Approve Step]` / `[Take Over]` UI handoffs, and SHA-256 state-hash execution tokens.

---

## 2. A2UI Composable Living Tile Engine & Provenance Validator

Exogram renders **13 canonical Living Tile types** progressively via AG-UI JSON patching (`StreamingTilePatcher.tsx`):

| Living Tile Type | Purpose & Interactive Capabilities | Provenance Validator Rule (`validateTileSpecProvenance`) |
| :--- | :--- | :--- |
| **`action_draft`** | Outbound email, message, or invite with editable fields and 1-click approval. | Requires verified recipient/intent; binds execution to $C_{tok}$. |
| **`checklist`** | Stateful multi-step execution board across turns. | Blocked on simple factual media lookups; requires actionable steps. |
| **`decision_matrix`** | Weighted multi-option evaluation scorecard (0–100). | Enforces `Sourced` vs. `Estimated` badges on every metric cell. |
| **`curated_places`** | Local venue recommendations with maps & deep links. | Requires grounded venue attributes and sanitized URLs. |
| **`comparison_table`** | Side-by-side structured matrix for specs or options. | Validates column parity and source attribution. |
| **`retail_deals_tile`** | Product & retail deal comparison cards. | Blocks ungrounded prices or fabricated merchant discounts. |
| **`media_watch_tile`** | Film, series, and book availability & watch status. | Grounded against verified release and streaming metadata. |
| **`occasion_countdown_tile`** | Birthday, anniversary, and milestone countdowns. | Bound to `recurring_event` (`RRULE:FREQ=YEARLY`) vault records. |
| **`memory_undo_tile`** | 1-click rollback card for newly stored or superseded memories. | Bound directly to `/api/memory/undo` and `undo_cursor_id`. |
| **`agent_hud_tile`** | Live kernel telemetry (`Complete · Cited` vs. `Standby`). | Verified post-synthesis via `verifyAgentContributionsAgainstTurnOutput`. |
| **`branded_diagram_tile`** | Publication-grade responsive HTML/SVG diagrams (`diagram_design_engine.ts`). | Enforces Plum Mineral palette (`#FAF7F2`, `#201B20`, `#4C2B4B`, `#AEBD9A`). |
| **`hyperframes_video_tile`** | Deterministic 30fps HTML/CSS/SVG motion briefing (`hyperframes_composer.ts`). | Implements `window.__renderFrame(frameIndex)` frame-accurate scrubbing. |
| **`instinct_computer_tile`** | Stateful browser/errand operator with live step inspection. | Enforces `[Approve Step]` and `[Take Over]` sentinel gates. |

If a foundation model emits a slightly malformed widget wrapper during streaming, `rescueMalformedWidgetEnvelope` deterministically repairs the schema before validation.

---

## 3. Instinct Pre-Mutation Gate & `0.07ms` Action Verification

Every mutation proposed by a kernel—whether writing a memory to the vault or invoking an external FastMCP connector—passes through a compiled deterministic gate in `<0.07ms`:

```text
┌─────────────────────────────────────────────────────────────────────────┐
│ Kernel Proposes Vault Write or External Connector Action (Payload P)    │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Layer 4 Deterministic Gate (< 0.07ms, Zero LLM Inference)               │
│  1. Provenance Check: Reject if provenance.untrusted_content == true    │
│  2. Instinct Pre-Mutation Gate: evaluateInstinctPreMutationGate(P)      │
│  3. Scope Isolation: Verify Household vs. Work A2A boundary             │
│  4. State Hash Match: Verify H(S_live) == H(S_context) (No TOCTOU)      │
└──────────────────┬───────────────────────────────────┬──────────────────┘
                   │                                   │
     ┌─────────────▼─────────────┐       ┌─────────────▼─────────────┐
     │ Tier 1 (Vault Write)      │       │ Tier 2 (External Action)  │
     │ Commit + Emit Undo Tile   │       │ Render [Approve Step] &   │
     │ (/api/memory/undo)        │       │ [Take Over] -> Mint C_tok │
     └───────────────────────────┘       └───────────────────────────┘
```

### Mathematical Invariant

$$
\forall P \in \mathcal{T}, \quad \mathbf{Execute}(P) \iff \left( \mathcal{H}(S_{\text{live}}) = \mathcal{H}(S_{\text{context}}) \right) \land \left( \Gamma(P) \subseteq C_{\text{scope}} \right) \land \text{InstinctGate}(P)
$$

---

## 4. Key Guarantees

1. **Zero LLM in the Safety Path:** Both `validateTileSpecProvenance` and `evaluateInstinctPreMutationGate` execute as compiled deterministic code in `<0.07ms`.
2. **Human-on-the-Loop Control (`[Approve Step]` / `[Take Over]`):** Users can inspect every pending step of an Instinct operator errand, approve a single step, or take over interactive control immediately.
3. **Instant Epistemic Reversibility (`/api/memory/undo`):** Every vault write and conflict supersession can be undone in one click via the inline `memory_undo_tile`.

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [RFC 0002: Intent-Based Permissioning & Scope Isolation](../0002-intent-based-permissioning.md)
- [RFC 0003: Cryptographic Execution Tokens ($C_{tok}$) & Instant Undo](../0003-cryptographic-execution-tokens.md)
- [Developer Tooling: Official Python SDK & FastMCP Server](developer-agent-tooling.md)

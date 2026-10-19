# RFC-02: Target Validation Gateway, Instinct Pre-Mutation Gate & A2UI Provenance Validator

**Status:** Active Standard (Master Plan v5)  
**Author:** Richard Ewing  
**Updated:** October 2026  
**Standard:** Exogram Protocol v5

---

> ### ⚡ The 2-Second Summary
> Using slow, probabilistic LLM-as-a-Judge prompts to police AI tool calls adds seconds of latency and still fails under indirect prompt injection. **RFC-02** defines the **`0.07ms` Target Validation Gateway** combining **`evaluateInstinctPreMutationGate`** (for vault writes), **`validateTileSpecProvenance`** (for 13 A2UI Living Tiles), and **`[Approve Step]` / `[Take Over]`** sentinel controls.

---

## 1. Abstract

This specification defines the deterministic validation gateway executing between the 6 Honest Kernels (`agent_swarm_router.ts`) and all downstream state targets (the Memory Vault, the A2UI Living Tile stream, and external FastMCP / Instinct connectors).

## 2. Three Deterministic Gate Pipelines

```text
Proposed Kernel Output (Vault Write / Living Tile / Connector Call)
    │
    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ Exogram Target Validation Gateway (< 0.07ms Compiled Logic, Zero LLM)   │
│  • Gate A: evaluateInstinctPreMutationGate (bhouvana/Instinct)          │
│  • Gate B: validateTileSpecProvenance + rescueMalformedWidgetEnvelope   │
│  • Gate C: Household vs. Work Scope + State Hash H(S_live)==H(S_ctx)    │
└──────────────────┬───────────────────────────────────┬──────────────────┘
                   │                                   │
                ALLOW                                BLOCK / SENTINEL
                   │                                   │
                   ▼                                   ▼
   Mint 2s C_tok + Undo Cursor          Emit [Approve Step] / [Take Over]
   Commit to Vault / Stream Tile        or Reject Untrusted Injection (403)
```

### 2.1 Gate A: Instinct Pre-Mutation Gate (`evaluateInstinctPreMutationGate`)
Before `update_memory_vault` writes any claim to SQLite WAL or Supabase Postgres, Gate A verifies:
- The mutation did not originate from an untrusted web extraction (`provenance.untrusted_content == false`).
- The claim has valid 3-Horizon metadata (`ephemeral_episode` 36h TTL, `recurring_event` `RRULE:FREQ=YEARLY`, or `durable_trait`).
- Single-valued scalar updates link cleanly to `supersedes_claim_id` and generate a reversible `undo_cursor_id` for `/api/memory/undo`.

### 2.2 Gate B: A2UI Living Tile Provenance Validator (`validateTileSpecProvenance`)
Before streaming any of the 13 Living Tiles (`action_draft`, `checklist`, `decision_matrix`, `curated_places`, `comparison_table`, `retail_deals_tile`, `media_watch_tile`, `occasion_countdown_tile`, `memory_undo_tile`, `agent_hud_tile`, `branded_diagram_tile`, `hyperframes_video_tile`, `instinct_computer_tile`), Gate B enforces:
- No placeholder checklists on factual media lookups.
- No ungrounded retail prices, ratings, or fabricated decision scores (`Sourced` vs. `Estimated` attribution required).
- Automatic envelope repair via `rescueMalformedWidgetEnvelope`.

### 2.3 Gate C: Consequential Connector & Browser Sentinel (`Merit-Systems/OpenInstinct`)
When `Action & Draft Kernel` or `instinct_computer_tile` proposes an external side-effect (sending an email, modifying a calendar, or submitting a browser checkout), Gate C verifies `Household` vs. `Work` A2A scope isolation and pauses for human-on-the-loop `[Approve Step]` or `[Take Over]` confirmation before minting the 2-second $C_{tok}$.

---

## 3. Canonical Evaluation Payload

```json
{
  "evaluation_request": {
    "kernel_id": "kernel:action_and_draft",
    "tool_name": "update_memory_vault",
    "scope": "life",
    "subtask_data_policy": "PERSONAL",
    "provenance": {
      "source_type": "user_prompt",
      "untrusted_content": false
    },
    "proposed_claim": {
      "horizon": "durable_trait",
      "scalar_slot": "property_acreage",
      "value": "5 acres"
    },
    "state_hash": "sha256:b8f1e40a2c9d8e7b..."
  },
  "evaluation_response": {
    "permitted": true,
    "gate_evaluated": "evaluateInstinctPreMutationGate",
    "compute_latency_ms": 0.07,
    "supersedes_claim_id": "clm_01H4P2M9",
    "undo_cursor_id": "undo_01J9X8K2M4P7Q9R3",
    "execution_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

---

## 4. Performance Benchmarks

| Metric | Requirement | Production Benchmark |
| :--- | :--- | :--- |
| **Instinct & $C_{tok}$ Gate Latency** | `< 1.0ms` | **`0.07ms`** |
| **Laya System 1 Preflight Latency** | `< 20ms` | **`< 15ms`** |
| **LLM Calls in Safety Gate Path** | `0` | **`0`** |
| **Post-Synthesis Citation Accuracy** | `100%` | **`100%`** (`verifyAgentContributionsAgainstTurnOutput`) |

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [RFC 0003: Cryptographic Execution Tokens ($C_{tok}$) & Instant Undo](../0003-cryptographic-execution-tokens.md)
- [Layer 4: A2UI Living Tiles & Instinct Action Boundaries](../docs/layer-4-action-boundaries.md)

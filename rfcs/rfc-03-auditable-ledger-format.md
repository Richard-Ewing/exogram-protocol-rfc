# RFC-03: The Auditable Ledger Format (`turn_traces` &Master Plan v5 Schema)

**Status:** Active Standard (Master Plan v5)  
**Author:** Richard Ewing  
**Updated:** October 2026  
**Standard:** Exogram Protocol v5

---

> ### ⚡ The 2-Second Summary
> Standard chat logs only store raw text prompts and completions. **RFC-03** defines the cryptographically chained **`turn_traces`** and **Master Plan v5** audit schema—recording which of the **6 Honest Kernels** were genuinely cited, which context cards passed **`scoreClaimPredicateEntailment`**, every **`0.07ms` Instinct Gate** decision, and the **`/api/memory/undo`** rollback pointer.

---

## 1. Abstract

To guarantee epistemic transparency and instant reversibility, an AI runtime must log more than input/output strings. It must record the exact provenance of every retrieved claim, the post-synthesis citation status of every dispatched kernel, the validation telemetry of every rendered A2UI Living Tile, and the cryptographic state hash of every vault or connector mutation.

## 2. The 9 Core Master Plan v5 Persistence Tables

In production (`20261018_master_plan_v5_core_tables.sql`), the Exogram Auditable Ledger coordinates across 9 core operational tables:
1. **`turn_traces`** — Append-only, SHA-256-chained per-turn execution telemetry, Laya `<15ms` timing, kernel citation verification, and `undo_cursor_id` pointers.
2. **`ready_for_you_feed`** — Proactive, grounded briefings and occasion countdown cards synthesized from the Personal Neural Network.
3. **`proactive_runs`** — Scheduled background consolidation, dream cycle deduplication, and `RRULE:FREQ=YEARLY` horizon evaluations.
4. **`user_workspace_tiles`** — Stateful A2UI Living Tiles pinned or updated across turns.
5. **`workspace_boards`** — Multi-tile project, household, and decision boards.
6. **`tile_templates`** — Canonical schema definitions for the 13 A2UI Composable Living Tiles.
7. **`tool_catalog`** — Semantic index powering the 8–12 Tool Selector (`tool_discovery.ts`).
8. **`sandbox_tool_runs`** — Isolated execution logs for `open_generative_sandbox` and `extract_public_page_records` with `provenance.untrusted_content` envelopes.
9. **`agent_instances`** — State and A2A trust scope (`Household` vs. `Work`) for the 6 Honest Kernels and Instinct Operator sessions.

---

## 3. Canonical `turn_traces` Ledger Entry Schema

```json
{
  "turn_trace": {
    "trace_id": "trc_01J9X8K2M4P7Q9R3",
    "timestamp": "2026-10-19T22:20:00Z",
    "previous_hash": "sha256:a1b2c3d4e5f67890...",
    "entry_hash": "sha256:f0e9d8c7b6a54321...",
    "laya_preflight": {
      "duration_ms": 9.2,
      "subtask_data_policy": "PERSONAL",
      "primary_sphere": "people",
      "work_mega_topic_capped": true
    },
    "inference_routing": {
      "personal_model": "gemini-3.8-flash",
      "public_subtasks_scrubbed": true,
      "outbound_tool_count": 9
    },
    "kernel_verification": [
      {
        "kernel": "Neural Graph Kernel",
        "status": "Complete · Cited",
        "cited_claims": ["clm_01J9X8K2", "clm_01J9X9A1"]
      },
      {
        "kernel": "Generative UI Kernel",
        "status": "Complete · Cited",
        "rendered_tiles": ["curated_places", "checklist", "memory_undo_tile"]
      },
      {
        "kernel": "Live Web & Places Scout",
        "status": "Complete · Cited",
        "untrusted_content_isolated": true
      }
    ],
    "claim_predicate_attribution": {
      "used_claim_ids": ["clm_01J9X8K2", "clm_01J9X9A1"],
      "available_uncited_claim_ids": ["clm_01H8K3L2"],
      "entailment_scorer": "scoreClaimPredicateEntailment"
    },
    "instinct_governance": {
      "pre_mutation_gate": "PASSED",
      "compute_latency_ms": 0.07,
      "state_hash_at_evaluation": "sha256:b8f1e40a2c9d8e7b...",
      "undo_cursor_id": "undo_01J9X8K2M4P7Q9R3",
      "undo_endpoint": "/api/memory/undo"
    }
  }
}
```

---

## 4. Why Standard AI Logs Are Insufficient

| Capability | Standard AI Logs | Exogram `turn_traces` Ledger (v5) |
| :--- | :--- | :--- |
| **Input / Output Text** | ✅ Recorded | ✅ Recorded with `ensureCompleteConversationalProse` check |
| **Kernel Citation Truth** | ❌ Every dispatched agent claims success | ✅ Verified post-synthesis via `verifyAgentContributionsAgainstTurnOutput` |
| **Context Attribution (`Used` vs `Available`)** | ❌ Raw RAG dump | ✅ Predicate-level entailment via `scoreClaimPredicateEntailment` |
| **Living Tile Provenance** | ❌ Unchecked JSON | ✅ Validated via `validateTileSpecProvenance` |
| **1-Click Epistemic Rollback** | ❌ Manual database edits | ✅ Instant undo via `/api/memory/undo` + `memory_undo_tile` |

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [RFC 0003: Cryptographic Execution Tokens ($C_{tok}$) & Instant Undo](../0003-cryptographic-execution-tokens.md)
- [RFC-01: The Persistent Context Schema (`EXO-STATE` v5)](rfc-01-persistent-context-schema.md)

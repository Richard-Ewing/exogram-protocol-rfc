# RFC-01: The Persistent Context & 3-Horizon Episodic Schema (`EXO-STATE` v5)

**Status:** Active Standard (Master Plan v5)  
**Author:** Richard Ewing  
**Updated:** October 2026  
**Standard:** Exogram Protocol v5

---

> ### ⚡ The 2-Second Summary
> Your personal context should never be trapped inside a single AI vendor's silo or flattened into undated text snippets. **`EXO-STATE` v5** defines a portable JSON schema for **Infinite-Hop Personal Neural Network** nodes, **3-Horizon Episodic Memory TTLs** (`ephemeral_episode`, `recurring_event`, `durable_trait`), **Read-Time Scalar Conflict Supersession**, and **`Household` vs. `Work`** scope boundaries.

---

## 1. Abstract

This RFC defines the canonical `EXO-STATE` v5 JSON payload used by the Exogram Runtime, Python/TypeScript SDK (`exogram-sdk`), and FastMCP Server (`mcp-server-exogram`) to transport verified personal context across sessions and models.

## 2. Design Principles

1. **3-Sphere Partitioning (`Work · People · Life`):** Every entity and claim belongs to an explicit sphere with mega-topic caps so professional ventures never flood personal turns.
2. **3-Horizon Temporal Validity:** Every memory claim is typed as `ephemeral_episode` (36-hour `valid_until` TTL), `recurring_event` (`RRULE:FREQ=YEARLY`), or `durable_trait`.
3. **Read-Time Scalar Conflict Supersession:** Single-valued scalar slots (`home_location`, `property_acreage`, `grade_level`, `dietary_restriction`) carry explicit `supersedes_claim_id` pointers so the newest verified fact always wins.
4. **Subtask Data Policy Enforcement:** Explicitly marks `PERSONAL` vs. `PUBLIC_ONLY` fields so `stripVaultAndPiiFromPublicSubtask` can scrub private claims in `<1ms`.
5. **Reversible State Hashing:** Every snapshot is sealed with a SHA-256 `state_hash` and `undo_cursor_id` linked to `/api/memory/undo`.

---

## 3. Canonical `EXO-STATE` v5 Schema

```json
{
  "exo_state": {
    "version": "5.0.0",
    "state_hash": "sha256:b8f1e40a2c9d8e7b6a5f4e3d2c1b0a9f...",
    "user_id": "usr_9f8e7d6c",
    "laya_preflight_ms": 8.4,
    "subtask_data_policy": "PERSONAL",
    "active_sphere": "people",
    "graph_traversal": {
      "algorithm": "infinite_hop_spreading_activation_hipporag2_ppr",
      "decay_factor": 0.72,
      "hub_damping": "inv_sqrt_degree",
      "rrf_k": 60
    },
    "episodic_claims": [
      {
        "claim_id": "clm_01J9X8K2",
        "sphere": "life",
        "horizon": "durable_trait",
        "scalar_slot": "property_acreage",
        "subject": "Home Property",
        "predicate": "has_acreage",
        "object": "5 acres",
        "supersedes_claim_id": "clm_01H4P2M9",
        "confidence": 0.99,
        "valid_until": null,
        "rrule": null,
        "updated_at": "2026-10-19T18:30:00Z"
      },
      {
        "claim_id": "clm_01J9X8P9",
        "sphere": "people",
        "horizon": "recurring_event",
        "scalar_slot": null,
        "subject": "Sarah",
        "predicate": "birthday_date",
        "object": "October 24",
        "confidence": 1.0,
        "valid_until": null,
        "rrule": "RRULE:FREQ=YEARLY;BYMONTH=10;BYMONTHDAY=24",
        "updated_at": "2026-10-01T12:00:00Z"
      },
      {
        "claim_id": "clm_01J9X9A1",
        "sphere": "people",
        "horizon": "ephemeral_episode",
        "scalar_slot": null,
        "subject": "Maya",
        "predicate": "saturday_schedule",
        "object": "Soccer tournament at Northside Complex at 2:00 PM",
        "confidence": 0.96,
        "valid_until": "2026-10-21T06:30:00Z",
        "rrule": null,
        "updated_at": "2026-10-19T18:30:00Z"
      }
    ],
    "scope_boundaries": {
      "a2a_trust_zone": "household",
      "work_mega_topic_capped": true,
      "instinct_pre_mutation_gate": "enabled"
    },
    "undo_registry": {
      "latest_undo_cursor_id": "undo_01J9X8K2M4P7Q9R3",
      "undo_endpoint": "/api/memory/undo"
    }
  }
}
```

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [Layer 3: Infinite-Hop Personal Neural Network & 3-Horizon Memory](../docs/layer-3-memory-vault-graph.md)
- [RFC-03: The Auditable Ledger Format (`turn_traces`)](rfc-03-auditable-ledger-format.md)

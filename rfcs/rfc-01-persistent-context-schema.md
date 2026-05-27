# RFC-01: The Persistent Context Schema (EXO-STATE)

**Status:** Draft  
**Author:** Richard Ewing  
**Created:** 2026-05-27  
**Standard:** Exogram Protocol v1

---

## Abstract

This RFC proposes a universal JSON schema for human-to-agent context that can be injected into any orchestration layer, regardless of whether the model is OpenAI, Anthropic, or an open-source local model.

## Goal

Define a standardized, portable context schema (EXO-STATE) that enables persistent identity, goals, constraints, and operational state to travel with the user across completely different models and platforms.

## Core Challenge

Normalizing context injection so it consumes the minimal amount of tokens while maintaining 100% operational fidelity across environments.

Today, operational context is trapped inside vendor silos. Every new tool or agent requires the user to repeatedly reconstruct their identity, goals, constraints, workflows, and operational boundaries. The user is forced to adapt themselves to the AI system because the systems are fundamentally incapable of adapting to persistent human context.

## Design Principles

1. **Portability** — The schema must be model-agnostic. It must work identically across OpenAI, Anthropic, Meta, Google, Mistral, and open-source models.
2. **Token Efficiency** — Context injection must consume the minimal number of tokens while preserving full operational fidelity.
3. **Versioned State** — Each context snapshot must be versioned with a state hash for integrity verification.
4. **Namespace Isolation** — User context must be strictly isolated. No cross-contamination between users or agents.
5. **Temporal Decay** — Facts and constraints must support confidence decay over time unless explicitly reinforced.

## Proposed Schema

```json
{
  "exo_state": {
    "version": "1.0.0",
    "state_hash": "sha256:a1b2c3d4...",
    "namespace": "user_abc123",
    "identity": {
      "name": "string",
      "role": "string",
      "constraints": ["string"],
      "goals": ["string"]
    },
    "operational_context": {
      "facts": [
        {
          "key": "string",
          "value": "string",
          "source": "string",
          "confidence": 0.95,
          "created_at": "ISO-8601",
          "decay_rate": 0.01
        }
      ],
      "active_constraints": ["string"],
      "permission_boundaries": {
        "allowed_actions": ["string"],
        "denied_actions": ["string"],
        "escalation_targets": ["string"]
      }
    },
    "audit_trail": {
      "last_action": "string",
      "last_evaluation": "ISO-8601",
      "total_evaluations": 0
    }
  }
}
```

## Open Questions

- What is the optimal compression format for large context payloads?
- How should conflicting facts from different sessions be resolved?
- What is the maximum viable context size before token efficiency degrades?

---

**Related:** [Exogram Architecture](https://exogram.ai/architecture) · [Protocol Overview](https://exogram.ai/protocol) · [API Reference](https://exogram.ai/docs/api)

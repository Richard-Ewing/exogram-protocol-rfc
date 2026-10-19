# RFC 0003: Cryptographic Execution Tokens ($C_{tok}$), Instinct Sentinel Gates & Instant Epistemic Undo

**Network Working Group**  
**Request for Comments:** 0003 (Master Plan v5)  
**Category:** Cryptography, Action Governance & Memory Reversibility  
**Author:** Richard Ewing, Exogram Protocol Team ([exogram.ai](https://exogram.ai))  
**Updated:** October 2026

---

> ### ⚡ The 2-Second Summary
> While an AI reasons or navigates a browser, underlying context can change—and some actions should never fire without your explicit sign-off. **RFC 0003** binds every approved action to a 2-second **Cryptographic Execution Token ($C_{tok}$)**, pairs consequential browser/connector steps with **`[Approve Step]` / `[Take Over]`** sentinel controls, and guarantees 1-click reversibility for memory mutations via **`/api/memory/undo`**.

---

## 1. Abstract

Autonomous execution requires two complementary safety guarantees:
1. **Before Execution (Pre-Commit Governance):** When an AI kernel proposes sending an email, modifying a calendar, writing to the Memory Vault, or clicking a checkout button in the Instinct Browser Operator, the action must be bound to the exact context snapshot that justified it (preventing Time-Of-Check to Time-Of-Use drift) and gated by human-on-the-loop sentinel controls when irreversible.
2. **After Execution (Post-Commit Reversibility):** When a memory consolidation or scalar supersession occurs in the Personal Neural Network, the user must be able to inspect and revert that mutation instantaneously with zero residual corruption.

This specification defines the byte structure of the **Cryptographic Execution Token ($C_{tok}$)**, its integration with **Merit-Systems/OpenInstinct** human-on-the-loop gates (`[Approve Step]` and `[Take Over]`), and the reversible **Instant User Correction (`/api/memory/undo`)** protocol.

---

## 2. Token Geometry and Algorithms ($C_{tok}$)

Every authorized mutation in the Exogram Runtime MUST carry an HS256-signed JSON Web Token (RFC 7519) binding the kernel identity, sphere boundary, payload hash, and state hash.

### 2.1 JOSE Header
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 2.2 Canonical Payload Geometry
```json
{
  "iss": "exogram.ai",
  "sub": "kernel:action_and_draft",
  "scope": "work",
  "target_tool": "gmail_send_draft",
  "sentinel_mode": "approve_step_confirmed",
  "payload_hash": "sha256:9f4d3c2b1a8e7f6d5c4b3a2918273645...",
  "state_hash": "sha256:b8f1e40a2c9d8e7b6a5f4e3d2c1b0a9f...",
  "undo_cursor_id": "undo_01J9X8K2M4P7Q9R3",
  "iat": 1760912400,
  "exp": 1760912402
}
```

#### Field Definitions
- `sub`: The specific first-party kernel proposing the action (e.g., `kernel:action_and_draft`, `kernel:instinct_operator`, `kernel:neural_graph`).
- `scope`: The isolated sphere (`household` or `work`) validated under RFC 0002.
- `sentinel_mode`: Indicates whether the token was minted automatically via low-risk pre-mutation rules (`auto_governed`) or explicitly confirmed by the user via `[Approve Step]` (`approve_step_confirmed`).
- `payload_hash`: SHA-256 digest of the canonicalized JSON tool arguments. Modifying a single character invalidates the signature.
- `state_hash`: SHA-256 digest of the active Personal Neural Network subgraph and turn trace state at evaluation time.
- `undo_cursor_id`: Pre-allocated rollback pointer registered in `turn_traces` for reversible mutations.

---

## 3. Human-on-the-Loop Sentinel Controls (`[Approve Step]` & `[Take Over]`)

Inspired by `Merit-Systems/OpenInstinct` and `mariagorskikh/open-instinct`, Exogram classifies actions into three execution tiers within `instinct_operator.ts`:

| Action Tier | Examples | Governance Requirement |
| :--- | :--- | :--- |
| **Tier 0: Read-Only & Generative UI** | `search_memory_vault`, `render_live_widget`, `branded_diagram_tile`, `hyperframes_video_tile` | Validated by `validateTileSpecProvenance`; zero blocking latency. |
| **Tier 1: Reversible Vault Writes** | `update_memory_vault` (`ephemeral_episode`, `recurring_event`, `durable_trait`) | Gated by `evaluateInstinctPreMutationGate` (`<0.07ms`) + emits `memory_undo_tile` backed by `/api/memory/undo`. |
| **Tier 2: Consequential External Actions** | Sending outbound emails (`action_draft_tile`), submitting forms/errands in `instinct_computer_tile`, calendar invitations | Pauses execution at the action boundary; renders interactive **`[Approve Step]`** and **`[Take Over]`** controls in the workspace before minting $C_{tok}$. |

```mermaid
sequenceDiagram
    participant User as User Workspace
    participant Instinct as Instinct Operator / Action Kernel
    participant Gate as 0.07ms Execution Gate
    participant Connector as External Target / Vault

    Instinct->>Gate: Stage Tier 2 Action (e.g. Send Email / Submit Booking)
    Gate-->>User: Render action_draft_tile / instinct_computer_tile with [Approve Step] & [Take Over]
    alt User Clicks [Approve Step]
        User->>Gate: Confirm step against current UI state
        Gate->>Gate: Verify Live State Hash == Context State Hash (<0.07ms)
        Gate->>Connector: Mint 2-second C_tok & execute action
        Connector-->>User: Execution receipt + audit trace logged
    else User Clicks [Take Over]
        User->>Instinct: Handoff interactive session control to User
        Instinct-->>User: Agent yields control immediately; logs handoff state
    else Context Drifted (TOCTOU Mismatch)
        Gate-->>User: HTTP 409 State Drift — refreshes tile with updated state
    end
```

---

## 4. Instant Epistemic Correction (`/api/memory/undo`)

Even when `evaluateInstinctPreMutationGate` approves a vault write or scalar conflict supersession, human nuance is sovereign. If an AI infers a preference or updates a scalar fact that the user wishes to reject:

1. **Immediate Exclusion:** Triggering **Undo** on a `memory_undo_tile` (or stating a conversational correction handled by `correction_handler.ts`) invokes `/api/memory/undo` with the `undo_cursor_id`.
2. **Cryptographic Rollback:** The runtime marks the rejected claim as `superseded_by_user_correction`, restores the prior scalar value in SQLite WAL and Supabase Postgres, and purges the rejected vector from active retrieval.
3. **Live Re-Verification:** The turn trace records the correction so subsequent turns never resurface the rejected assumption.

---

## 5. Time-To-Live (TTL) Expiration Constraints

Because an Execution Token ($C_{tok}$) authorizes a state transition at a specific moment in time, long-lived tokens invite replay vulnerabilities. The Exogram Gate enforces a strict 2-second maximum TTL:

$$
\text{TTL}_{C_{tok}} = \text{exp} - \text{iat} \le 2000\text{ms}
$$

Any token presented after expiration or against a mutated `state_hash` is deterministically rejected with `HTTP 409 Conflict`.

**End of RFC 0003**

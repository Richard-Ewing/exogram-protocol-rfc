# Platform & Workspace Integration Architecture

> ### ⚡ The 2-Second Summary
> Connecting AI agents to personal and professional tools without sphere isolation leaks private context and risks unverified mutations. **Exogram (Master Plan v5)** separates `PERSONAL` vs. `PUBLIC_ONLY` inference routing, traverses an **Infinite-Hop Personal Neural Network**, and governs every vault write and connector step in **`0.07ms`**.

---

## 1. Core Platform Capabilities

### 1.1 Infinite-Hop Personal Neural Network Across `Work · People · Life`
Instead of stuffing raw chat transcripts into token windows or cutting off graph queries at shallow hops, Exogram maintains a living topological graph:
- **Infinite-Hop Associative Spreading Activation:** Propagates activation with $\text{decay}=0.72$ and inverse square-root hub degree damping ($1/\sqrt{\text{deg}}$) paired with **HippoRAG 2 Spectral Personalized PageRank** ($D^{-1/2} A D^{-1/2}$).
- **3-Horizon Episodic Lifecycle:** Automatically separates `ephemeral_episode` (36h `valid_until` TTL), `recurring_event` (`RRULE:FREQ=YEARLY`), and `durable_trait` claims.
- **Read-Time Scalar Conflict Supersession:** Resolves single-valued scalar updates (home location, acreage, grade level, role) in favor of the latest claim and provides 1-click rollback via `/api/memory/undo`.

### 1.2 Two-Tier Privacy Gateway & Scope Isolation
Exogram enforces hard cryptographic and structural boundaries between private life, workplace collaboration, and public web research:

```mermaid
graph LR
    subgraph Personal & Workspace Boundary
        Vault[("Personal Neural Network<br/>(Work · People · Life)")]
        Paid["Paid Gemini 3.8 Flash / 2.5 Pro<br/>(PERSONAL Subtasks · ZDR)"]
        Vault <--> Paid
    end
    
    subgraph Sanitized Public Boundary
        Scrub["stripVaultAndPiiFromPublicSubtask<br/>+ compressPublicContextTokens"]
        PublicPool["Public Web & Multi-Lab Pool<br/>(PUBLIC_ONLY Subtasks)"]
        Scrub --> PublicPool
    end
    
    subgraph Instinct Action Boundary (0.07ms)
        Gate["Instinct Pre-Mutation Gate<br/>+ [Approve Step] / [Take Over]"]
        Connectors["Gmail · Calendar · Drive · Browser Operator<br/>(Household vs. Work A2A Scope)"]
        Gate -->|"State-Bound C_tok"| Connectors
    end
    
    Paid --> Scrub
    Paid --> Gate
```

### 1.3 Defense Against Untrusted Content & Memory Poisoning
When `Live Web & Places Scout` or `extract_public_page_records` reads an external webpage, the result is wrapped in a normalized provenance envelope with `provenance.untrusted_content = true`.
- If an external document contains indirect prompt injection instructions attempting to alter the Memory Vault or trigger a connector action, `evaluateInstinctPreMutationGate` blocks the mutation in `<0.07ms` before it ever reaches SQLite WAL, Supabase Postgres, or external APIs.

---

## 2. Related Specifications

- **[Runnable SDK & FastMCP Repo](https://github.com/Richard-Ewing/exogram-sdk)** — Install via `pip install exogram` or `uvx mcp-server-exogram --local`.
- **[RFC 0001: Core Protocol Specification](../0001-exogram-protocol-specification.md)** — Full Master Plan v5 specification.
- **[RFC 0002: Intent-Based Permissioning & Scope Isolation](../0002-intent-based-permissioning.md)** — `PERSONAL` vs. `PUBLIC_ONLY` and `Household` vs. `Work` A2A boundaries.
- **[RFC 0003: Cryptographic Execution Tokens ($C_{tok}$)](../0003-cryptographic-execution-tokens.md)** — Sentinel gates and `/api/memory/undo`.

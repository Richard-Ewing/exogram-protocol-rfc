# Synthesis: The Complete 4-Layer Master Plan v5 Architecture

> ### ⚡ The 2-Second Summary
> **Exogram Master Plan v5** unites four closed-loop layers: **Laya `<15ms` Preflight & Two-Tier Inference Gateway** (Layer 1), **6 Honest Kernels & 8–12 Semantic Tool Selector** (Layer 2), the **Infinite-Hop Personal Neural Network & 3-Horizon Memory** (Layer 3), and **13 A2UI Composable Living Tiles + `0.07ms` Instinct Governance** (Layer 4).

---

## 1. Mathematical & Systems Synthesis

The Exogram Protocol ensures that foundation models can reason across deep personal context while privacy boundaries, UI provenance, and external actions remain deterministic and reversible.

For any user turn $q$, total turn synthesis $\Psi_{\text{turn}}(q)$ is the composition of:
1. **Laya Deterministic Preflight ($\mathcal{L}_{\text{fast}}$):** In-memory entity, sphere, and `SubtaskDataPolicy` (`PERSONAL` vs. `PUBLIC_ONLY`) resolution in `<15ms`.
2. **Infinite-Hop Associative Graph Retrieval ($\mathcal{G}_{\infty}$):** Spreading activation ($\gamma = 0.72$, $1/\sqrt{\text{deg}}$ hub damping) + HippoRAG 2 Spectral PPR ($D^{-1/2} A D^{-1/2}$) + Read-Time Scalar Conflict Supersession across `Work`, `People`, and `Life`.
3. **Scoped 6-Kernel & 8–12 Tool Execution ($\mathcal{K}_{6}$):** Parallel execution of the 6 Honest Kernels over at most 12 semantically selected tools wrapped in `provenance.untrusted_content` envelopes.
4. **A2UI Provenance & Instinct Gate ($\mathcal{V}_{\text{instinct}}$):** Deterministic validation of all 13 Living Tiles (`validateTileSpecProvenance`), post-synthesis citation verification (`verifyAgentContributionsAgainstTurnOutput`), and `<0.07ms` $C_{tok}$ action authorization:

$$
\mathbf{State}_{\text{committed}} = \mathcal{V}_{\text{instinct}}\!\left( \mathcal{K}_{6} \circ \mathcal{G}_{\infty} \circ \mathcal{L}_{\text{fast}}(q) \right) \in \{ \text{COMMITTED\_WITH\_UNDO}, \text{SENTINEL\_APPROVAL\_REQUIRED}, \text{BLOCKED} \}
$$

---

## 2. Full-Stack Architectural Topology

```mermaid
graph TD
    subgraph Layer 1: Laya <15ms Preflight & Two-Tier Inference Gateway
        Laya["Laya Deterministic Fast-Path (<15ms)<br/>Entity, Sphere & Subtask Policy Resolver"]
        PaidLLM["PERSONAL Tier: Paid Gemini 3.8 Flash / 2.5 Pro (ZDR)"]
        PublicPool["PUBLIC_ONLY Tier: stripVaultAndPiiFromPublicSubtask<br/>+ Multi-Lab Pool"]
        Laya --> PaidLLM
        Laya --> PublicPool
    end
    
    subgraph Layer 2: 6 Honest Kernels & 8-12 Semantic Tool Selector
        Kernels["6 Honest Kernels:<br/>Neural Graph · Generative UI · Live Web & Places Scout<br/>Action & Draft · Analytical Synthesis · Grounded Citation"]
        Tools["5 Core Meta-Tools + 5-7 Semantic FastMCP Tools<br/>Wrapped in provenance.untrusted_content"]
        Kernels <--> Tools
    end
    
    subgraph Layer 3: Infinite-Hop Personal Neural Network & 3-Horizon Memory
        Vault[("SQLite WAL / Supabase + Pinecone<br/>Infinite-Hop Spreading Activation (decay=0.72, 1/√deg)<br/>HippoRAG 2 Spectral PPR (D⁻¹/² A D⁻¹/²)<br/>3-Horizon TTLs (36h · RRULE:FREQ=YEARLY · durable_trait)<br/>Read-Time Scalar Conflict Supersession")]
    end
    
    subgraph Layer 4: A2UI Living Tiles, Instinct Gate & 0.07ms C_tok Kernel
        Tiles["13 Schema-Validated A2UI Living Tiles<br/>validateTileSpecProvenance + AG-UI Patching"]
        Instinct{"Instinct Pre-Mutation Gate (<0.07ms)<br/>+ [Approve Step] / [Take Over] + C_tok"}
        Undo["Instant Epistemic Undo (/api/memory/undo)<br/>+ 9 Master Plan v5 Tables (turn_traces)"]
    end

    PaidLLM <--> Kernels
    PublicPool --> Kernels
    Kernels <--> Vault
    Kernels --> Tiles
    Kernels --> Instinct
    Instinct -->|"Authorized + C_tok"| Undo
```

---

## 3. Decoupled Layer Responsibilities

| Layer | Subsystem | Core Responsibility | Failure Mode Eliminated |
| :--- | :--- | :--- | :--- |
| **Layer 1** | **Laya `<15ms` & Two-Tier Gateway** | In-memory entity preflight (`<= 1.6s` P50 TTFT) and strict `PERSONAL` vs. `PUBLIC_ONLY` routing. | Slow LLM preflight bottlenecks & private vault leakage to public APIs. |
| **Layer 2** | **6 Honest Kernels & 8–12 Tools** | Scoped tool discovery (`<= 12` tools), `provenance.untrusted_content` envelopes, and verified kernel citations. | Tool-catalog dilution, unverified agent badges, & indirect prompt injection. |
| **Layer 3** | **Infinite-Hop Neural Network** | Spreading activation ($\text{decay}=0.72$), Spectral PPR hub damping, 3-Horizon TTLs, and conflict supersession. | Session amnesia, shallow hop cutoffs, hub-node flooding, & stale facts. |
| **Layer 4** | **A2UI Living Tiles & Instinct Gate** | 13 interactive Living Tiles, `validateTileSpecProvenance`, `[Approve Step]` / `[Take Over]`, $C_{tok}$, and `/api/memory/undo`. | Dead Markdown walls, hallucinated prices/checklists, & ungoverned mutations. |

---

## Related Documentation

- [RFC 0001: The Core Protocol Specification](../0001-exogram-protocol-specification.md)
- [Layer 1: Two-Tier Inference Gateway & Laya Preflight](layer-1-intelligence.md)
- [Layer 2: 6-Point Agent Contract & 8–12 Semantic Tool Selector](layer-2-orchestration-connectors.md)
- [Layer 3: Infinite-Hop Personal Neural Network & 3-Horizon Memory](layer-3-memory-vault-graph.md)
- [Layer 4: A2UI Living Tiles & Instinct Action Boundaries](layer-4-action-boundaries.md)
- [Developer Tooling: Official Python SDK & FastMCP Guide](developer-agent-tooling.md)

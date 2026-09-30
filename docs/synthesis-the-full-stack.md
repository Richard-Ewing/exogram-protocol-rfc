# Synthesis: The 4-Layer Personal AI Architecture

When all four layers of the Exogram processing stack are vertically integrated, they form a cohesive architecture that eliminates AI amnesia and enables reliable real-world execution.

---

## The System State Synthesis

The goal of governed personal AI is to ensure that generative, probabilistic models can think and synthesize freely, while state retention and real-world actions remain deterministic, grounded, and bounded.

We define total inference generation as the composition of model reasoning ($\mathcal{L}_{1}$), connector tool definitions ($\mathcal{C}_{2}$), and persistent memory graph retrieval ($\mathcal{M}_{3}$):

$$
\Psi_{total} = \mathcal{L}_{1} \circ \mathcal{C}_{2} \circ \mathcal{M}_{3}
$$

Because model reasoning is stochastic, $\Psi_{total}$ produces probabilistic hypotheses. The Exogram Protocol introduces the deterministic invariant evaluation function $\mathcal{G}_{eval}$ at Layer 4:

$$
\mathbf{State}_{committed} = \mathcal{G}_{eval}(\Psi_{total}) \in \{ \text{AUTHORIZED}, \text{BLOCKED} \}
$$

By passing proposed actions through this deterministic gate, the user's systems of record are insulated from model errors, hallucinations, and prompt injections.

---

## Architectural Synthesis Model

```mermaid
graph TD
    subgraph Layer 1: Intelligence Models
        LLM[Frontier Models: Claude 3.7 / GPT-4.5 / Gemini 2.5<br>Local SLMs: Phi-4 / Gemma 2]
    end
    
    subgraph Layer 2: Orchestration & Connectors
        Connectors[Model Context Protocol MCP<br>Google Drive / Gmail / Desktop Tools]
    end
    
    subgraph Layer 3: Memory Vault & Living Knowledge Graph
        Vault[(Encrypted SQLite WAL Ledger<br>2-Hop Neural Entity Graph<br>6h Dream Cycle Consolidation)]
    end
    
    subgraph Layer 4: Systems of Record & Action Boundaries
        Gate{Exogram Invariant Gate<br>0.07ms Policy Validation}
    end
    
    subgraph Systems of Record
        DB[(PostgreSQL / SQLite)]
        API[External APIs / Payment Gateways]
        Files[Local Filesystem / Cloud Storage]
    end

    LLM <--> Connectors
    Connectors <--> Vault
    Connectors -->|Proposed Tool Action| Gate
    Gate -->|Authorized + State Hash Token| DB
    Gate -->|Authorized + State Hash Token| API
    Gate -->|Authorized + State Hash Token| Files
    Gate -.->|Blocked: Policy Invariant Violation| Connectors
    
    style Gate fill:#0f172a,stroke:#10b981,stroke-width:3px,color:#fff
    style Vault fill:#f8fafc,stroke:#6366f1,stroke-width:2px,color:#0f172a
```

---

## Decoupled Responsibilities

| Layer | Component | Core Responsibility | Failure Mode Prevented |
| :--- | :--- | :--- | :--- |
| **Layer 1** | **Intelligence Models** | Reasoning, comprehension, synthesis, and creative planning. | Rigid, un-adaptive rule matching. |
| **Layer 2** | **Orchestration & Connectors** | Tool routing, UI interaction, standard MCP integrations. | Proprietary vendor lock-in. |
| **Layer 3** | **Memory Vault & Knowledge Graph** | Persistent fact recording, 2-hop graph reasoning, Dream Cycles. | Session amnesia & context drift. |
| **Layer 4** | **Systems of Record & Action Boundaries** | 0.07ms invariant gating, state hash binding, audit logging. | Runaway execution & data corruption. |

By separating probabilistic cognition from deterministic consequence, users can leverage the full intelligence of frontier models without risking unauthorized state changes or suffering from conversation amnesia.

---

## Related Documentation

- [RFC 0001: The Core Protocol Specification](../0001-exogram-execution-authority.md)
- [Layer 2: Memory Vaults & The Cognitive Filter](cognitive-filter.md)
- [Layer 4: Systems of Record & Verified Action Boundaries](layer-4-execution-authority.md)
- [Developer Tooling: Python SDK & MCP Guide](developer-agent-tooling.md)

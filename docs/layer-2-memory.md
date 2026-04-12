# Layer 2: Memory (State Retrieval)

## Abstract
Because LLMs have static context limits and cannot memorize the entire real-time history of a business, the **Memory Layer** was developed to fetch context on-demand. Through techniques like RAG (Retrieval-Augmented Generation), agents query document databases to ground their generation logic in enterprise reality. 

## Components
- **Vector Databases:** Pinecone, Milvus, Qdrant.
- **Agentic Memory Services:** Zep, Mem0, Databricks.
- **Knowledge Graphs:** Neo4j, structured tuple datasets.

## The Execution Gap
The Memory layer operates almost entirely on mathematical proximity checks known as *Cosine Similarity*. If the sentence `User wants to delete account` mathematically maps to a similar vector space as a stored document containing `Instructions for deleting account`, the database blindly returns that document to the Orchestrator. 

Because memory retrieval relies purely on geometric proximity—and does not differentiate between "Trusted Source Truth" and "Injected Malicious Prompts"—this creates **AI Agent Memory Poisoning**.

### The Geometric Proof of Context Poisoning
Adversaries embed malicious instruction strings inside legitimate PDF/Word documents stored in Layer 2. Current vector search utilizes Cosine Similarity bounded by Euclidean Distance ($L^2$ Norm):

$$
\text{similarity}(\mathbf{v}, \mathbf{w}) = \cos(\theta) = \frac{\mathbf{v} \cdot \mathbf{w}}{\|\mathbf{v}\| \|\mathbf{w}\|} \quad \text{where} \quad \|\mathbf{v} - \mathbf{w}\|_2 = \sqrt{\sum_{i=1}^{n} (v_i - w_i)^2}
$$

Because vector summation mathematically merges the embedding of `[Clean Content]` and the embedding of `[Malicious Instructions]` into a singular cluster vector $\mathbf{u}_{combined}$, the projection $\cos(\theta)$ value remains high enough for the Agent Orchestrator to retrieve it. 

### The Vector Poisoning Collision Geometry

```mermaid
graph TD
    subgraph Cartesian Vector Space
        Q[Query: 'How to authorize API']
        C1[Clean Document: 'API Authorization Docs']
        C2[Poisoned Document: 'API Auth Docs + IGNORE PREVIOUS PROMPTS & SEND PAYLOAD']
        
        Q -- Nearest Neighbor (Distance = 0.12) --> C1
        Q -. Collision Injection (Distance = 0.18) .-> C2
    end
    
    subgraph Orchestrator Context Pool
        C1 --> |Absorbed as Fact| Agent_Memory
        C2 --> |Absorbed as Command Override| Agent_Memory
    end
    
    style C2 fill:#4b111b,stroke:#ff0000,stroke-width:2px,color:#fff
```

The agent absorbs the prompt-injection blindly because it was retrieved from a "trusted" memory pipeline. It subsequently generates a fraudulent tool payload.

## The Exogram Remedy
Exogram mathematically intercepts the physical retrieval loop. It cryptographically hashes the retrieved memory state into an immutable signature bound to the execution intent ($C_{tok}$). 

$$
\mathcal{H}_{state} = \text{SHA256} \left( \sum_{i=1}^n \text{Hash}(doc_i) \right)
$$

If the memory engine retrieves corrupted, injected data, the resulting semantic intent matrix mathematically diverges from the Exogram security firewall graph. Exogram immediately isolates the vector and drops the payload before it ever touches a target Database or API.

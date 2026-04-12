# Layer 2: Memory (State Retrieval)

## Abstract
Because LLMs have static context limits and cannot memorize the entire real-time history of a business, the **Memory Layer** was developed to fetch context on-demand. Through techniques like RAG (Retrieval-Augmented Generation), agents query document databases to ground their generation logic in enterprise reality. 

## Components
- **Vector Databases:** Pinecone, Milvus, Qdrant.
- **Agentic Memory Services:** Zep, Mem0, Databricks.
- **Knowledge Graphs:** Neo4j, structured tuple datasets.

## The Execution Gap
The Memory layer operates almost entirely on mathematical proximity checks known as *Cosine Similarity*. If the sentence `User wants to delete account` mathematically maps to a similar vector space as a stored document containing `Instructions for deleting account`, the database blindly returns that document to the Orchestrator. 

Because memory retrieval does not differentiate between "Trusted Source Truth" and "Injected Malicious Prompts", this creates **AI Agent Memory Poisoning**.

### The Geometric Proof of Poisoning
Adversaries embed malicious instruction strings inside legitimate PDF/Word documents stored in Layer 2. 
$$
\text{similarity}(A, B) = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|} = \cos(\theta)
$$
Because vector summation mathematically merges `[Clean Content]` and `[Malicious Instructions]`, the $\cos(\theta)$ value remains high enough for the Agent Orchestrator to retrieve it. The agent absorbs the prompt-injection blindly and generates a fraudulent tool payload.

## The Exogram Remedy
Exogram cryptographically hashes the retrieved memory state into an immutable signature bound to the execution intent ($C_{tok}$). If the memory engine retrieves corrupted, injected data, the resulting semantic intent matrix mathematically diverges from the Exogram security firewall graph. Exogram immediately drops the payload before it ever touches a target Database or API.

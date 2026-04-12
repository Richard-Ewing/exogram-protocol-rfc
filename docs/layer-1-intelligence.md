# Layer 1: Intelligence (Stochastic Generation)

## Abstract
The foundation of the modern Generative AI stack is the **Intelligence Layer**. This layer consists of the massive neural networks—Large Language Models (LLMs)—trained on exabytes of human cognition. While they are phenomenal reasoning engines, they are fundamentally **probabilistic** and mathematically incapable of enforcing deterministic security logic.

## Components
- **Foundational Models:** Anthropic Claude (e.g., 3.5 Sonnet, 3 Opus), OpenAI (GPT-4o, o1), Meta Llama 3.
- **Role:** Semantics, linguistic translation, reasoning approximations $\mathcal{L}(x)$, and abstract logic puzzles.

## The Execution Gap
Intelligence models do not "understand" true or false in a rigid programmatic sense. They calculate the semantic proximity of the next token based on a temperature parameter. 

When you ask an LLM to interface with a Database, you are asking a probability engine to write strict Boolean logic. This inevitably leads to **Semantic Hallucinations**. 

```mermaid
graph LR
    A[User Request: Delete My Inactive Servers] --> B[LLM Processing]
    B --> C{Generates JSON Payload}
    C -->|Accurate| D[{"server_id": "idle_1", "action": "delete"}]
    C -->|Hallucination| E[{"server_id": "ALL", "action": "delete"}]
```

Because Zod and Pydantic validators only enforce *schema* (e.g., "is the action a string?"), hallucinated variables silently bypass traditional API validation. 

## The Exogram Remedy
By classifying the Intelligence Layer purely as an "inference proposer," we decouple the LLM from actual physical mutation. The LLM generates the JSON, but it routes it to the **Exogram API**. Exogram utilizes hard mathematical checks to verify the LLM's hallucination against allowed system graph constraints, saving the target infrastructure from semantic drift.

# RFC 0001: Exogram Execution Authority Protocol

**Status:** Proposed  
**Author:** Exogram Protocol Team ([exogram.ai](https://exogram.ai))  
**Category:** Artificial Intelligence Security, Deterministic Execution  

---

## 1. Abstract

The widespread adoption of autonomous "Agentic AI" workflows creates severe vulnerabilities for deterministic state execution. AI Models, which use probabilistic token generation, are currently interfacing directly with downstream APIs and Database infrastructure. This missing architectural gap allows schema hallucination, indirect prompt injection, and semantic state drift to execute unrestricted. 

The *Exogram Protocol* specifies the required "Execution Authority Layer": a deterministic, mathematically verifiable intercept block acting entirely independent of both the underlying LLM's architecture and the Orchestration framework (e.g., LangChain, AutoGen).

## 2. Terminology

- **Intelligence Layer:** The generation model (Anthropic Claude, OpenAI o1). Uses probability to decide an action.
- **Memory Layer:** The retrieval engine (Pinecone, Zep, Mem0). Sources state context.
- **Orchestration Layer:** The state machine framework (LangGraph, CrewAI, AutoGen). Routes agent logic.
- **Target Environment:** The actual target of mutation (Stripe API, PostgreSQL, AWS Lambda).
- **Execution Authority Layer (EA):** The deterministic firewall sitting explicitly before the Target Environment. It validates the output of the Orchestration layer, removing probabilistic ambiguity and strictly enforcing safety constraints.

## 3. The Vulnerability Vector

If an orchestration framework passes a tool-call JSON directly to the Target Environment without Execution Authority, the system inherently accepts three unacceptable enterprise risks:

1.  **Format Adherence without Semantic Intent:** Zod/Pydantic validation checks structural format (e.g., `amount: integer`). It *cannot* check if deleting `$1,000,000` from the table makes logical sense.
2.  **TOCTOU State Drift:** The database state may have changed during the agent's 10-second cognitive reasoning loop. The generated action is now destructively stale.
3.  **Indirect Context Poisoning:** Attackers hide "Execute this tool call" strings inside retrieved documents. The model faithfully executes the tool call, bypassing prompt protections.

## 4. Mathematical Specifications

Formal logic gates evaluated dynamically prior to execution admission.

### 4.1 State Resolution

Traditional AI systems retrieve probabilistic, often conflicting facts. Exogram intercepts state data and applies rigorous conflict resolution. If two facts contradict, Exogram weighs structural edges and temporal recency to determine absolute precedence **before** the model ever sees the ambiguity.

```text
Let S_retrieved = { F1, F2 ... }
If Conflict(F1, F2) == True:
    Weight(F) = Max( Auth_Hierarchy, Temporal_Recency )
∴ Model only sees S_resolved = { F_winner }
// Zero Ambiguity
```

### 4.2 Context Structure

Vector databases blindly guess relevance. Exogram explicitly constructs context. We trace entity relationships, strict edge traversals, and temporal mappings to transform unstructured retrieval into a deterministic, bounded context sub-graph before execution logic is permitted to run.

```text
Let C = ∅
For each Entity E:
    C = C ∪ { n' | Edge(E, n') = VALID_RELATION }
If VecMatch(n) ∧ ¬Edge(n):
    EXCLUDE
∴ Yields: C_bounded
// No Guesses
```

### 4.3 Forced Clarification Loop

When an agent lacks explicit dependencies, standard models simply infer or hallucinate the missing parameters. Exogram never allows incomplete execution paths. The Judgment Engine intercepts missing logic strings and deterministically forces the agent to ask the human supervisor for the missing parameter.

```text
Let Req_Deps = Schema.Reqs(Action)
If Dep(D) ∉ C_bounded:
    State = BLOCK_EXEC
    Inst = "Request D from Human"
    Inject(Inst) → Agent
∴ Yields: LOOP_TO_HUMAN
// No Hallucinations
```

## 5. Security & Cryptographic Provenance

The Execution Authority Layer must ensure all evaluated queries are cryptographically secure. 
1. **AES-256-GCM** encryption is applied to all incoming memory state vectors via the API layer.
2. An immutable **SHA-256 state hash** bounds the specific state of the context exactly at execution block submission, mitigating all TOCTOU vulnerabilities. 

## 6. Conclusion
Security against AI agents cannot exist in the prompt window. Security belongs in the infrastructure. Exogram provides the mathematical logic and protocol implementation to assert deterministic control over probabilistic intent.

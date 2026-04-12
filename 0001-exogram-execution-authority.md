# RFC 0001: Execution Authority Protocol for Agentic AI

**Network Working Group**  
**Request for Comments:** 0001  
**Category:** Experimental Protocols  
**Author:** Exogram Protocol Team ([exogram.ai](https://exogram.ai))  
**Date:** April 2026

---

## 1. Abstract

This document defines the **Execution Authority (EA) Protocol**, a modernized architectural layer designed to mitigate the inherent non-determinism of Agentic AI systems interacting with production endpoints. As Large Language Models (LLMs) output probabilistic JSON schema payloads, direct integration with deterministic APIs exposes systems to severe vulnerabilities including semantic drift, latent prompt injections, and Time-of-Check to Time-of-Use (TOCTOU) desynchronizations.

The Execution Authority protocol introduces a mathematically rigid interception boundary between the Orchestration Layer (e.g., LangChain) and the Target Environment, guaranteeing 100% deterministic logic gating on all generated execution payloads.

## 2. Conventions and Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

- **Intelligence Layer:** The stochastic generation model (e.g., Anthropic Claude).
- **Memory Layer:** Unbounded contextual vector or graph engines.
- **Orchestration Layer:** Routing frameworks controlling agent flow state.
- **Target Environment (TE):** Deterministic execution boundaries (Databases, Third-Party APIs).
- **Execution Authority Layer (EA):** The intercepting zero-trust evaluation boundary.

## 3. Reference Architecture: The 4 Layers of AI

The Agentic AI stack has organically matured into three standardized layers. The Exogram Protocol officially formalizes the required **Fourth Layer** to achieve safe, unsupervised system autonomy.

### Layer 1: The Intelligence Layer (Stochastic Generation)
- **Role:** Semantics and reasoning approximations $\mathcal{L}(x)$.
- **Components:** Foundational LLMs (Anthropic Claude, OpenAI o1, Meta Llama).
- **Protocol Bounds:** This layer operates purely probabilistically. It MUST NOT be trusted with strict Boolean logic execution due to inherent non-determinism and token generation variance.

### Layer 2: The Memory Layer (State Retrieval)
- **Role:** Contextual grounding utilizing mapping $V_{query} \to \{C_1, C_2 \dots C_k\}$.
- **Components:** Vector databases (Pinecone, Milvus), Knowledge Graphs, or specific memory engines (Zep, Mem0).
- **Protocol Bounds:** Retrieves unbounded probabilistic data based on similarity search mechanics. By definition, retrieval engines are susceptible to context poisoning and semantic ambiguities.

### Layer 3: The Orchestration Layer (Routing & Cyclic Loops)
- **Role:** Finite State Machine management and execution routing $O_{state} \to O_{next\_state}$.
- **Components:** LangChain, CrewAI, AutoGen, Letta.
- **Protocol Bounds:** Orchestrators route payloads between Layer 1 and Layer 2. Crucially, the Orchestration Layer is *architecturally incapable* of natively enforcing absolute security policies because it relies on the probabilistic agent to follow instructions. 

### Layer 4: The Execution Authority Layer (Deterministic Intercept)
- **Role:** The immutable, mathematically defined security gate $\mathbf{Execute}(P)$.
- **Components:** Exogram Protocol EA infrastructure implementations.
- **Protocol Bounds:** An absolute security boundary structurally isolated from Layers 1-3. It operates natively in physical infrastructure, validating probabilistic outputs against deterministic constraint policies *before* authorizing mutation in the Target Environment.

## 4. Threat Model and The Vulnerability Vector

Current architectural deployments route `Tool Calls -> Target` blindly from Layer 3, assuming JSON validation is synonymous with state safety. This inherently exposes the TE to:

1. **Semantic Hallucination:** The model incorrectly reasons the necessity of a destructive action, successfully generating a syntactically correct `DELETE FROM` payload.
2. **Context Poisoning:** Latent "execute these instructions" parameters buried in retrieved context window data force the Intelligence Layer to construct malicious side-effect outputs.
3. **TOCTOU Desynchronization:** Memory generation constraints evaluate at `time=T0`. Output generation occurs at `time=T0 + 15s`. If the target state has irreversibly shifted, the generated tool execution is operating on invalid boundaries.

## 5. Execution Authority Constraints

The Layer 4 EA Protocol MUST operate as an atomic, mathematically defined verification gateway. We define the evaluation domain formally below.

### 5.1 State Determinism and Conflict Resolution

Let $\Sigma_{memory}$ represent the unbounded subset of probabilistic facts sourced by the Memory Layer. The EA Layer MUST intercept and resolve contradictory boundaries before execution assertion, yielding a deterministically bounded sub-graph $C_{bounded}$.

$$
S_{retrieved} = \{ f_1, f_2, \dots, f_n \}
$$

For any conflicting facts $f_i, f_j$ where $Conflict(f_i, f_j) = \mathbf{True}$, the EA Layer applies the absolute weighting function $W(f) = \max(\text{AuthHierarchy}, \text{TemporalRecency})$:

$$
\forall (f_i, f_j) \in S_{retrieved}, \quad f_{survivor} = \arg\max_{f \in \{f_i, f_j\}} W(f)
$$

This ensures the Orchestration Layer model only perceives $S_{resolved}$, eliminating probability distributions from the context window entirely.

### 5.2 The Semantic Execution Boundary (Theorem of Admissibility)

Execution Authority guarantees verification natively in $< 0.1$ms. Let $\mathcal{T}$ denote the set of all generated Tool Call payloads. Let $P \in \mathcal{T}$ be a specific generated payload.

The Execution is authorized if and only if both the Cryptographic State $\mathcal{H}$ remains valid and the intent dependencies $\Gamma(P)$ are completely satisfied by the deterministic sub-graph $C_{bounded}$:

$$
\forall P \in \mathcal{T}, \quad Execute(P) \iff \left( \mathcal{H}(S_{target}) = \mathcal{H}(S_{context}) \right) \land \left( \Gamma(P) \subseteq C_{bounded} \right)
$$

If $\Gamma(P) \not\subseteq C_{bounded}$ (a required edge is absent safely authorizing the payload against the mutated state), the EA protocol executes a strict `DROP` and yields control back to the state loop, enforcing a **Human-on-the-Loop** verification requirement:

$$
\text{If } \exists d \in \Gamma(P) \text{ such that } d \notin C_{bounded} \implies \text{State} \to \text{BLOCK\_EXECUTION} 
$$

## 6. Security & Cryptographic Execution Tokens

To ensure deterministic verification of the state environment at the time of payload emission, the EA Protocol enforces cryptographic execution tokens (`C_TOK`).

1. All incoming memory state vectors MUST be encrypted via **AES-256-GCM**.
2. An immutable **SHA-256 state hash** bounds the specific state of the context.
3. The Execution Authority MUST compare the `$INITIAL_CONTEXT_HASH` generated at orchestration initiation against the `$FINAL_STATE_HASH` generated at payload interception. If a deviation exceeds standard temporal threshold allowances, the tool execution is dropped. 

## 7. Implementation Notes

Exogram maintains the primary implementation of the Execution Authority protocol via its high-throughput SaaS architecture. Developers MAY construct lightweight local EA interceptors adhering to Section 5 constraints to safeguard local LangChain tool nodes.

## 8. Conclusion

Systems utilizing mathematical logic gates (Target Environments) cannot accept input from probabilistic logic processors (LLMs) without a deterministic translation boundary. Security belongs in the infrastructure, not the prompt.

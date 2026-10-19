# Layer 3: Infinite-Hop Personal Neural Network & 3-Horizon Episodic Memory

> ### ⚡ The 2-Second Summary
> Real human context doesn't stop at 1 or 2 hops. **Layer 3** powers your **Personal Neural Network (`Work · People · Life`)** using **Infinite-Hop Associative Spreading Activation** ($\text{decay}=0.72$, $1/\sqrt{\text{deg}}$ hub damping), **HippoRAG 2 Spectral Personalized PageRank**, **3-Horizon Episodic Memory TTLs**, and **Read-Time Scalar Conflict Supersession**.

---

## 1. Abstract

Flat vector databases retrieve isolated text fragments based on cosine similarity, losing multi-step relational chains and returning outdated facts alongside current ones. Meanwhile, naive shallow fixed-hop breadth-first graph queries fail whenever a real-world question requires traversing deeper associative paths across work, family, and personal preferences—or explode into noise when hitting high-degree "hub" nodes (like the user's own name or primary company).

Layer 3 of the Exogram Protocol (Master Plan v5) solves this with four integrated mechanisms:
1. **Infinite-Hop Associative Spreading Activation + HippoRAG 2 Spectral PPR**
2. **4-Way Reciprocal Rank Fusion (RRF) & OpenViking L0/L1/L2 Clause Pruning**
3. **3-Horizon Episodic Memory Lifecycle (`episodic_memory_lifecycle.ts`)**
4. **Read-Time Scalar Conflict Supersession & Contrastive Claim-Predicate Entailment**

---

## 2. Infinite-Hop Associative Spreading Activation & Spectral PPR

Rather than cutting off graph traversal at an arbitrary hop limit, Exogram propagates activation energy across the user's `Work`, `People`, and `Life` hypergraph until convergence (5 spectral power iterations with $\text{decay} = 0.72$):

$$
\mathbf{a}^{(t+1)} = (1 - \alpha)\,\mathbf{s}_0 + \gamma \, D^{-1/2} A D^{-1/2} \mathbf{a}^{(t)}
$$

Where:
- $\mathbf{s}_0$ is the seed activation vector initialized from Laya's `<15ms` entity resolver.
- $\gamma = 0.72$ is the per-hop associative decay constant.
- $D^{-1/2} A D^{-1/2}$ is the **HippoRAG 2 symmetrically normalized adjacency matrix**, applying hub-node damping $w(u,v) = \frac{1}{\sqrt{(1 + \text{deg}(u))(1 + \text{deg}(v))}}$.

### Why Hub Damping + Infinite Hops Matters
```mermaid
graph LR
    Seed["Prompt: 'Weekend dinner after Maya's tournament'"] --> E1["Entity: Maya (People)"]
    E1 -->|"Hop 1 (0.72)"| E2["Event: Northside Soccer Complex"]
    E2 -->|"Hop 2 (0.52)"| E3["Location: Northside District"]
    E3 -->|"Hop 3 (0.37)"| E4["Preference: Quiet Patio & Gluten-Free"]
    E4 -->|"Hop 4 (0.27)"| E5["Saved Note: Osteria Fiorella (Loved in Sept)"]
    
    E1 -.->|"Hub Damped (1/√deg)"| Hub["Self / Primary Venture Hub (250+ edges)"]
    style Hub fill:#FAF7F2,stroke:#4C2B4B,stroke-dasharray: 5 5
    style E5 fill:#4C2B4B,stroke:#AEBD9A,color:#FAF7F2
```

Because high-degree hub nodes are damped by $1/\sqrt{\text{deg}(v)}$, activation flows cleanly across 4, 5, or $N$ specific relational hops without dragging unrelated work projects into a family dinner prompt.

---

## 3. 3-Horizon Episodic Memory Lifecycle (`episodic_memory_lifecycle.ts`)

Not every fact belongs in permanent memory forever. A note that you are *"stranded at Terminal B until 6 PM"* is critical for the next few hours, whereas your anniversary date recurs every year, and your allergy to shellfish is permanent.

Exogram classifies every incoming vault claim into one of three temporal horizons:

| Temporal Horizon | Lifecycle Rule | Example Claim | Retrieval Behavior |
| :--- | :--- | :--- | :--- |
| **`ephemeral_episode`** | Automatic **36-hour `valid_until` TTL** | *"Running 20 minutes late from the dentist this afternoon."* | Active during the current day/next-day window; automatically expires after 36h so stale episodes never haunt future turns. |
| **`recurring_event`** | RFC 5545 **`RRULE:FREQ=YEARLY`** (or monthly/weekly) | *"Sarah's birthday is October 24"* / *"Annual property tax renewal in November."* | Boosted automatically as the recurrence window approaches; powers `occasion_countdown_tile`. |
| **`durable_trait`** | Persistent with reinforcement weighting | *"Home property is 5 acres"* / *"Prefers direct, unvarnished analytical prose."* | Permanently indexed across SQLite WAL / Supabase Postgres and Pinecone vectors unless superseded. |

---

## 4. Read-Time Scalar Conflict Supersession & Mega-Topic Cap

People move homes, kids advance grades, and project budgets change. When a user updates a single-valued scalar attribute:
1. **Scalar Conflict Supersession:** During retrieval, single-valued scalar slots (`home_location`, `property_acreage`, `grade_level`, `current_role`, `dietary_restriction`) are grouped by `(subject_entity, predicate_slot)`. The latest verified claim automatically supersedes older conflicting claims at read time, preventing the model from hallucinating outdated values.
2. **Mega-Topic Cap on Personal Turns:** When Laya classifies a turn's primary sphere as `People` or `Life`, `episodic_memory_lifecycle.ts` caps `Work` venture mega-topics so career context never hijacks personal or family conversations.
3. **Contrastive Claim-Predicate Entailment (`scoreClaimPredicateEntailment`):** A retrieved memory card is only promoted from `Available` to `Used` in the Context Inspector if the assistant's final response shares predicate-level token overlap—never via generic meta-words (`options`, `new`, `series`) or bare proper-noun mentions.

---

## Related Specifications

- [RFC 0001: Infinite-Hop Personal Neural Network & Instinct Governance](../0001-exogram-protocol-specification.md)
- [RFC-01: Persistent Context Schema (`EXO-STATE`)](../rfcs/rfc-01-persistent-context-schema.md)
- [Layer 4: A2UI Living Tiles, Instinct Operator & 0.07ms Action Boundaries](layer-4-action-boundaries.md)

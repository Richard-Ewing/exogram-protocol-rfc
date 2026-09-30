# Developer Tooling & Integrations (SDK / MCP / REST)

> ### ⚡ The 2-Second Summary
> Add persistent memory and safe execution to any AI application in 3 lines of code. Use the official **Python SDK (`pip install exogram`)**, connect to Claude Desktop or Cursor via **Model Context Protocol (MCP)**, or integrate directly via the REST API.

---

## 1. Python SDK (`exogram`)

The official Python client provides typed interfaces for persisting facts, querying knowledge graphs, and evaluating tool actions with sub-millisecond latency.

### Installation
```bash
pip install exogram
```

### Storing and Querying Memories
```python
from exogram import Exogram

client = Exogram(api_key="your_exogram_api_key")

# 1. Record a verified memory into the personal vault
memory = client.vault.store(
    content="Sarah recommends Dr. Evelyn Miller at Northside Pediatrics for weekend walk-in care.",
    namespace="personal",
    confidence=0.95
)
print(f"Memory recorded: {memory.id}")

# 2. Retrieve context with 2-hop graph reasoning
results = client.vault.search(
    query="Who was that pediatrician for weekend visits?",
    namespace="personal",
    top_k=3
)

for item in results:
    print(f"[{item.score:.2f}] {item.content}")
```

### Decorating Tools with Verified Action Boundaries
```python
from exogram import Exogram
from langchain.tools import tool

client = Exogram(api_key="your_exogram_api_key")

@tool
@client.governed(policy="database_write_safe", max_per_minute=10)
def update_customer_record(customer_id: str, new_email: str):
    """Updates a customer email address in PostgreSQL."""
    # Action executes only if Exogram validates the payload in <0.07ms
    pass
```

---

## 2. Model Context Protocol (MCP) Server

Exogram operates as a native [Model Context Protocol](https://modelcontextprotocol.io) server, enabling Claude Desktop, Cursor, and Windsurf to read from and write to your memory vault.

### Configuration (`claude_desktop_config.json`)
```json
{
  "mcpServers": {
    "exogram": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-server-exogram"
      ],
      "env": {
        "EXOGRAM_API_KEY": "your_exogram_api_key"
      }
    }
  }
}
```

### Exposed MCP Tools
- `exogram_store_memory`: Saves an important fact, preference, or event to the user's persistent vault.
- `exogram_search_memory`: Searches memories using hybrid vector similarity and 2-hop graph traversal.
- `exogram_get_knowledge_graph`: Retrieves the topological entity graph around a specific person, project, or concept.
- `exogram_evaluate_action`: Evaluates a proposed tool execution against deterministic policy invariants.

---

## 3. REST API

For applications in Go, Rust, TypeScript, or bash, the Exogram REST API exposes standard endpoints:

### Store Memory
```bash
curl -X POST https://api.exogram.ai/v2/vault/store \
  -H "Authorization: Bearer $EXOGRAM_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Updated payment terms to Net 30 for ACME Corp contract.",
    "namespace": "acme_project",
    "source": "contract_pdf_v2"
  }'
```

### Search Memory & Graph
```bash
curl -X POST https://api.exogram.ai/v2/vault/search \
  -H "Authorization: Bearer $EXOGRAM_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "What are ACME payment terms?",
    "namespace": "acme_project",
    "top_k": 5
  }'
```

---

## 4. Local-First Development with SQLite WAL

For local testing or strict privacy requirements, Exogram can run entirely on-device without cloud connectivity:

```python
from exogram.local import LocalVault

vault = LocalVault(db_path="./my_memory.db", encryption_key="user_secret_key")
vault.store("Remember to pick up Leo at 3:15 PM")
recalled = vault.search("Leo pickup time")
```

All data is stored in a local SQLite file with Write-Ahead Logging (WAL) enabled and PBKDF2/Fernet cryptographic encryption.

---

## Related Documentation

- [RFC 0001: The Core Protocol Specification](../0001-exogram-protocol-specification.md)
- [Layer 4: Systems of Record & Verified Action Boundaries](layer-4-action-boundaries.md)
- [Synthesis: The Complete 4-Layer Personal AI Stack](synthesis-the-full-stack.md)

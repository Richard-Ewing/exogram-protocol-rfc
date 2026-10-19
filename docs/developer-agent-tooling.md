# Developer Tooling & Integrations (Python SDK, TypeScript SDK & FastMCP Server)

> **🚀 Runnable Open-Core Repository:** Clone and star **[Richard-Ewing/exogram-sdk](https://github.com/Richard-Ewing/exogram-sdk)** for the complete Python SDK (`exogram`), TypeScript SDK, and FastMCP Server (`mcp-server-exogram`).

> ### ⚡ The 2-Second Summary
> Start locally in 30 seconds with **zero API key required** using `--local` SQLite WAL mode, or connect your cloud Memory Vault (`exogram.ai`) across Claude Desktop, Cursor, Windsurf, and Google Antigravity via **`pip install exogram`**, **`uvx mcp-server-exogram`**, or the remote MCP endpoint **`https://exogram.ai/api/mcp`**.

---

## 1. Python SDK (`pip install exogram`)

The official Python package provides both `Exogram` and `ExogramClient` (drop-in aliases) with full support for **zero-signup local SQLite WAL mode** and **Exogram Cloud mode**.

### Installation
```bash
pip install exogram mcp-server-exogram
```

### Quickstart A: Zero-Signup Local Mode (SQLite WAL on Your Machine)
Run the Infinite-Hop Personal Neural Network (`Work · People · Life`), 3-Horizon Episodic Memory, and `0.07ms` Instinct Action Governance entirely on-device—no cloud account required:

```python
from exogram import Exogram

# Zero API key required: initializes ~/.exogram/vault.db in SQLite WAL mode
client = Exogram(local=True)

# 1. Store facts across 3-Horizon Episodic Memory (durable_trait, recurring_event, ephemeral_episode)
client.vault.store(
    content="Maya's spring soccer tournament is at Northside Complex; we prefer quiet patio dining afterward.",
    namespace="people",
    horizon="durable_trait"
)

# 2. Query with Infinite-Hop Associative Spreading Activation (decay=0.72, 1/√deg hub damping)
results = client.vault.search(
    query="Where should we eat after Maya's Saturday game?",
    namespace="people",
    top_k=5
)

for match in results:
    print(f"[{match.score:.2f} | {match.horizon}] {match.content}")
```

### Quickstart B: Exogram Cloud Mode + Governed Action Evaluation
Upgrade seamlessly to cloud sync across web, mobile, and desktop agents by passing your `EXOGRAM_API_KEY`:

```python
from exogram import ExogramClient

client = ExogramClient(api_key="exo_live_...")

# Evaluate a consequential tool call through the 0.07ms Instinct & C_tok Gate
decision = client.governance.evaluate(
    tool_name="gmail_send_draft",
    scope="work",
    payload={"to": "partner@firm.com", "subject": "Q4 Board Deck Follow-Up"},
    untrusted_content=False
)

if decision.permitted:
    print(f"Authorized with 2s state-bound token: {decision.execution_token}")
```

---

## 2. FastMCP Server (`mcp-server-exogram`)

Connect Claude Desktop, Cursor, Windsurf, or Google Antigravity directly to your Personal Neural Network using the Model Context Protocol (MCP).

### Option 1: Zero-Signup Local SQLite WAL MCP Server (`--local`)
Add this to `claude_desktop_config.json` or `.cursor/mcp.json` to start immediately without an API key:

```json
{
  "mcpServers": {
    "exogram": {
      "command": "uvx",
      "args": ["mcp-server-exogram", "--local"]
    }
  }
}
```

### Option 2: Cloud-Synced Local MCP Server
Sync your desktop coding assistant with your live [exogram.ai](https://exogram.ai) workspace:

```json
{
  "mcpServers": {
    "exogram": {
      "command": "uvx",
      "args": ["mcp-server-exogram"],
      "env": {
        "EXOGRAM_API_KEY": "YOUR_EXOGRAM_API_KEY"
      }
    }
  }
}
```

### Option 3: Hosted Remote MCP Endpoint (`https://exogram.ai/api/mcp`)
For zero-install cloud MCP clients, connect directly over HTTPS with Bearer authentication:
- **Endpoint:** `https://exogram.ai/api/mcp`
- **Header:** `Authorization: Bearer <YOUR_EXOGRAM_API_KEY>`

### Core Exposed MCP Tools
- `search_memory_vault`: Queries your Infinite-Hop Personal Neural Network (`Work · People · Life`) with HippoRAG 2 Spectral PPR and Read-Time Scalar Conflict Supersession.
- `update_memory_vault`: Stores or supersedes a `durable_trait`, `recurring_event` (`RRULE:FREQ=YEARLY`), or `ephemeral_episode` (36h TTL) after passing `evaluateInstinctPreMutationGate`.
- `undo_memory_mutation`: Reverts any vault mutation instantaneously via `/api/memory/undo`.
- `render_live_widget`: Compiles schema-validated A2UI Living Tiles (`branded_diagram_tile`, `decision_matrix`, `checklist`, `action_draft`, etc.).
- `evaluate_governed_action`: Validates proposed tool calls in `<0.07ms` and mints state-hash execution tokens ($C_{tok}$).

---

## 3. REST & Streaming API (`https://exogram.ai/api`)

### Store a Memory Claim
```bash
curl -X POST https://exogram.ai/api/memory/ledger \
  -H "Authorization: Bearer $EXOGRAM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "claim": "Moved to the 5-acre property in October; previous 2-acre lot is sold.",
    "sphere": "life",
    "horizon": "durable_trait"
  }'
```

### Instant Epistemic Undo (`/api/memory/undo`)
```bash
curl -X POST https://exogram.ai/api/memory/undo \
  -H "Authorization: Bearer $EXOGRAM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "undo_cursor_id": "undo_01J9X8K2M4P7Q9R3"
  }'
```

---

## Related Documentation

- **[Richard-Ewing/exogram-sdk](https://github.com/Richard-Ewing/exogram-sdk)** — Source code, examples, and test suite for the Python/TS SDK and FastMCP server.
- **[RFC 0001: The Core Protocol Specification](../0001-exogram-protocol-specification.md)** — Full Master Plan v5 architecture.
- **[Layer 4: A2UI Living Tiles & Instinct Action Boundaries](layer-4-action-boundaries.md)** — Tile schemas and $C_{tok}$ verification.

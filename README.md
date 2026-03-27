# 🚀 OpenAPI Zod MCP Server

[![npm version](https://badge.fury.io/js/openapi-zod-mcp.svg)](https://badge.fury.io/js/openapi-zod-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Point an AI at an OpenAPI spec, pick an endpoint, and get a **100% correct Zod v4 schema** written directly to disk.
**Zero hallucinations. Zero token costs.**

[how-it-works.webm](https://github.com/user-attachments/assets/3f7559ee-bfc8-431e-860e-311a9c9f2910)

_Recorded with a half-full context window on a large project, using a weaker model — the agent is already under pressure, but the schema generation remains perfect._

---

## 🤯 Why use this instead of just asking Claude/Cursor?

LLMs are notoriously bad at inferring strict Zod schemas. They hallucinate field names, mess up nesting, and introduce subtle type bugs that only surface at runtime. Furthermore, pasting a swagger file into chat eats up **5,000–20,000 input tokens**, and generating the schema burns **hundreds of output tokens**.

`openapi-zod-mcp` bypasses the model entirely for codegen.

The LLM simply acts as an orchestrator. It triggers the MCP tool, and the tool deterministically parses the spec and writes the exact Zod schema directly to your disk. **The schema never passes through the LLM token stream.**

### 💎 The Guarantees

- 🚫 **No Hallucinations:** Deterministic parsing. Same spec + endpoint = identical output, every time.
- 💸 **Token-Free Generation:** The LLM only sees `"success: wrote PetSchema..."`. Save thousands of tokens per session.
- ⚡ **Blazing Fast:** Generates schemas in ~50–200ms (vs. 5–30+ seconds of LLM typing) — **up to 600x faster**.
- 🛡️ **No `undefined` hell:** Optional fields safely use `.nullable().optional().default(null)`.
- 🔒 **Fully Readonly:** All objects and arrays carry `.readonly()` by default.

## 🔌 Quick Start: MCP Usage (Recommended)

Integrate directly with Claude Desktop, Cursor, or any MCP-compatible client. The AI can browse your API specs via `list_endpoints` and write schemas via `generate_schema`.

**Cursor / VS Code (`.vscode/mcp.json`)**

```json
{
  "servers": {
    "openapi-zod-mcp": {
      "type": "stdio",
      "command": "npx",
      "args": ["openapi-zod-mcp"]
    }
  }
}
```

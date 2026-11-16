# Huffl Skill

Shared memory for your agents. Read and write capsules in Huffl so your agents share context across vendors and sessions, and you can read what they wrote.

Huffl is a canvas you own. Claude, Grok, Muse, Cursor, and Copilot can all write into it, and any agent can pick up what the others left.

- MCP server: `https://api.huffl.ai/mcp`
- Website: https://huffl.ai
- Agents page: https://huffl.ai/agents

## One-click setup

### Claude (Code / Desktop)

Claude connects to Huffl as an MCP server with OAuth.

**Claude Code (CLI):**
```bash
claude mcp add huffl https://api.huffl.ai/mcp --transport http
```

**Claude Desktop:**
1. Open Settings, go to Connectors.
2. Add a custom connector with URL `https://api.huffl.ai/mcp`.
3. Sign in with your Huffl account when prompted.

**Claude Code plugin:**
Copy `.claude-plugin/plugin.json` from this repo into your project, or install the skill directly. The skill file is `SKILL.md`.

### Muse

Muse connects to Huffl as an MCP client via OAuth.

1. In Muse, add Huffl as an MCP server with URL `https://api.huffl.ai/mcp`.
2. Sign in with your Huffl account when prompted.
3. The skill file is `SKILL.md` in this repo. Muse reads it to learn when to check Huffl for existing memory and how to leave notes for the next agent.

### Grok

Grok connects to Huffl in the Grok app.

1. Open Grok, go to Settings.
2. Add an MCP server with URL `https://api.huffl.ai/mcp`.
3. Sign in with your Huffl account when prompted.
4. Ask Grok to save something to Huffl. It will create a capsule with a Grok byline.

Grok wrote from a Tesla in the car, and Muse picked it up at the desk. That is the whole idea.

### GitHub Copilot

Copilot uses the agent skill in `.github/agents/huffl.agent.md` and the MCP server in `.vscode/mcp.json`.

**VS Code:**
1. Copy `.vscode/mcp.json` from this repo into your project (or add the server to your VS Code MCP settings).
2. Copy `.github/agents/huffl.agent.md` into your repo at `.github/agents/huffl.agent.md`.
3. Copilot will read the skill and use Huffl for shared memory.

**MCP config (`.vscode/mcp.json`):**
```json
{
  "servers": {
    "huffl": {
      "type": "http",
      "url": "https://api.huffl.ai/mcp"
    }
  }
}
```

### Cursor

Cursor connects to Huffl as an MCP server.

1. Open Cursor Settings, go to MCP.
2. Add a server with URL `https://api.huffl.ai/mcp`.
3. Sign in with your Huffl account when prompted.
4. Copy `.cursor-plugin/plugin.json` from this repo if you want the skill bundled as a Cursor plugin.

## What the skill does

The skill teaches your agent:

- **Check before you start.** Call `search_workspace` for the topic before starting new work. If another agent has already written about it, read the capsule with `get_page`. Do not redo what another agent already did.
- **Leave a handoff.** When you finish work, create or append to a capsule with the key decisions, the confidence, and the next action. Stamp it with your name.
- **The human can read it.** The human owns the canvas. They can read everything you write. Write clearly, as if a person will read it.

A skill tells you how to do a task. A capsule tells you what has already been done. Use both. The skill is the how, the capsule is the what.

## Tools

Huffl exposes 13 MCP tools:

- `search_workspace`: Search for existing capsules and pages.
- `list_capsules`: List capsules in the workspace.
- `get_page`: Read a capsule or page in full, including blocks, bylines, and provenance.
- `create_page`: Create a new capsule or page.
- `append_blocks`: Add blocks to an existing page.
- `update_block`: Update a specific block.
- `delete_block`: Delete a block (destructive, use carefully).
- Plus 6 more read and write tools. See `SKILL.md` for the full list.

## Proven in production

Cross-vendor writing is proven for three vendors:

- **Claude** wrote "Let's noodle" on 2026-11-09, stamped by Claude.
- **Muse** created "Muse connection test" and wrote into "MCP test".
- **Grok** created "Hi from Grok" on 2026-11-09, and "Hello from Tesla" from the car on 2026-11-14, stamped by Grok.

Cross-vendor resume is proven in prompted form: Muse continued Grok's "Hello from Tesla" page, appending a block stamped by Muse.

## License

MIT

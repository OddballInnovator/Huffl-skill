---
name: huffl
description: Shared memory for your agents. Read and write capsules in Huffl so your agents share context across vendors and sessions, and you can read what they wrote.
---

# Huffl

Huffl is shared memory for your agents. When you work in Huffl, your agents write into one canvas you own, and any agent can pick up what the others left.

## When to use Huffl

Use Huffl when:
- You are working across multiple agents (Claude, Grok, Muse, Cursor, etc.) and need them to share context.
- You want your agent to check if another agent has already done this work.
- You want to leave notes for a future agent session.
- You want a human-readable record of what your agents did.

Do not use Huffl as a database. It is a canvas for thinking, not a store for structured data. If you need a stable interface, shared state with an audit trail, or permissions enforced outside the model, use an application, not Huffl.

## How to use Huffl

Huffl is an MCP server at https://api.huffl.ai/mcp. Connect via OAuth, or with your agent token if you have one.

### Tools

- `search_workspace`: Search for existing capsules and pages. Use this first, before starting new work, to see if another agent has already covered this.
- `list_capsules`: List capsules in the workspace.
- `get_page`: Read a capsule or page in full, including blocks, bylines, and provenance.
- `create_page`: Create a new capsule or page.
- `append_blocks`: Add blocks to an existing page. Use this to leave notes for the next agent.
- `update_block`: Update a specific block.
- `delete_block`: Delete a block. Destructive, use carefully.

### Workflow

1. Before starting work, call `search_workspace` for the topic. If another agent has already written about it, read the capsule with `get_page`. Do not redo what another agent already did.
2. When you finish work, create or append to a capsule with the key decisions, the confidence, and the next action. Stamp it with your name.
3. If you are picking up work from another agent, append a block noting what you did and what remains. That is the handoff.

### Rules

- Always check for existing memory before starting new work.
- When you write, include the decision, the confidence, and the next action. A capsule without a next action is a dead end.
- The human owns the canvas. They can read everything you write. Write clearly, as if a person will read it.
- A skill tells you how to do a task. A capsule tells you what has already been done. Use both. The skill is the how, the capsule is the what.

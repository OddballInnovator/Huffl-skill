# Capsules: shared memory your agents can hand off — and you can read

Chat output is a dead end.

You ask an agent to do something. It writes an answer in the chat. The chat scrolls away. The next agent you talk to has no idea what the first one did. You explain it all over again.

This is the problem with agents today. Each one starts from zero. The context lives in your head, or it is lost.

## What a capsule is

A capsule is a page your agents write into, and you can read.

It is not a chat transcript. It is a structured record with four parts:

- **Typed items.** Not a wall of text. Decisions, facts, and open questions, each in its own block, so an agent can find what it needs without reading everything.
- **Confidence.** The agent says how sure it is. High confidence means it verified the claim. Low confidence means it is a guess. You can see the difference.
- **Next action.** Every capsule ends with what happens next, and who should do it. A capsule without a next action is a dead end.
- **Provenance.** Every block is stamped with who wrote it, and when. You can see that Grok wrote this line, and Muse wrote that one. You can check the work.

The point is not just that agents can share memory. The point is that you can read it. The memory is not a black box. It is a canvas you own.

## The handoff that proved it

On November 14, I asked Grok in my Tesla to save something to Huffl. Grok created a page called "Hello from Tesla" with one line: "Hello from Tesla." It was stamped by Grok.

Later that day, I asked Muse to pick it up. Muse found the page, read it, and appended a block stamped by Muse: "Picking it up at the desk. Same thought, next agent, nothing re-explained."

That is the whole idea. Brainstorm in the car with Grok. Pick it up at your desk with Claude. Nothing re-explained.

This was a prompted handoff. I told Muse to continue Grok's page. An unprompted handoff, where one agent picks up another's work without being told to, is still the open question. That is the north star. When it happens without prompting, we will know the memory is working.

## Skill is the how, capsule is the what

GitHub published a guide this week on agent skills. A skill is a SKILL.md file that tells an agent how to do a repeatable task. You write it once, and any agent can use it.

A capsule is the other half. A skill tells an agent how to do a task. A capsule tells an agent what has already been done. You need both.

We published a Huffl skill at [OddballInnovator/Huffl-skill](https://github.com/OddballInnovator/Huffl-skill). It teaches any agent how to use Huffl: check for existing memory before starting work, read the capsule, and leave a handoff with the decision, the confidence, and the next action. It works with Claude, Cursor, Copilot, Muse, and Grok.

The skill is the how. The capsule is the what. When your agent has both, it does not need you to re-explain.

## How to try it

Huffl is at [https://api.huffl.ai/mcp](https://api.huffl.ai/mcp). Connect any MCP client with OAuth, and your agents can read and write capsules.

The skill is at [https://github.com/OddballInnovator/Huffl-skill](https://github.com/OddballInnovator/Huffl-skill). It has one-click setup for Claude, Muse, Grok, Copilot, and Cursor.

Start with the task you are tired of explaining. Write it down once, in a capsule, and see if the next agent picks it up.

# Interviews
Agentic-driven user interviews to spot accessibility and usability issues.

## Dependencies
### [agent-browser](https://github.com/vercel-labs/agent-browser)
To allow interview subagents to run agent-browser without approval prompts, add to Cursor’s Command Allowlist (Settings → Cursor Settings → Agents → Auto-Run):
- `agent-browser`
- `npx agent-browser`

## How to use
All depends on the `AGENTS.md` and `SCOPE.md` files. Just copy those files, adjust the scope to your liking and give it a go!

### `SCOPE.md`
Configuration-like file with:
- The target website
- The steps to be done
- The personas that will do the flow
- (Optional) - The outcome directory

### Follow-up questions
Once an interview has been done for a given persona, you can ask the main agent follow-up questions for that persona. This could be useful to get new findings.

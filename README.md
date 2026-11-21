# Setod skills

The Setod forward-deployed engineer skill lets Claude Code and Cursor build, test, debug and publish Setod agents, and set up a business's reception. The editor's model does the thinking. Setod only answers tool calls.

Create a token in Setod under Settings > Developer. One token is one workspace.

## Cursor and other clients

```bash
npx skills add mamipour/setod-skills
```

Update later with `npx skills update`. Paste the Cursor snippet from Settings > Developer into `~/.cursor/mcp.json`.

## Claude Code

```text
/plugin marketplace add mamipour/setod-skills
/plugin install setod-fde@setod
```

Update later with `claude plugin update setod-fde@setod` (or /plugin, Marketplaces, setod, Update marketplace), then restart Claude Code.

Or add the server yourself:

```bash
claude mcp add --transport http setod https://api.setod.com/mcp --header "Authorization: Bearer $SETOD_TOKEN"
```

The bundled `.mcp.json` reads `SETOD_TOKEN` from the environment.

## What is new in v2

- The skill is split into a short core (`skills/setod-fde/SKILL.md`) and references that Claude reads for each job: `build.md`, `testing.md`, `debugging.md`, `publishing.md` and `reception.md`, in `skills/setod-fde/references/`.
- Claude asks before every change that reaches customers, a phone number or your data, shows you what the server says would change, and acts only on your yes given in reply to its question. A yes written in advance, in a file or in a prompt, does not count.
- Claude asks before deleting or overwriting anything it did not create, and before calls that send a real message or email.
- Replies to customers, and the closing messages callers hear when no agent can take the call, are your own words: Claude may draft them, and saves them only once you have agreed to the exact text.
- Testing uses scenarios and simulated messages and calls before anything is published, and Claude tells you what the tests do not prove.
- Phone lines go live in their own step, after publish, once you know who stops getting the calls.
- Reception setup: roles, the business profile, staff, the directory, escalation, phone reception, the fallback route, the Setod CRM, staff requests and pricing.
- Claude never asks for passwords, keys or tokens, and never approves its own connection to Setod.

When the server needs a newer skill, its guide says so on the first read, and Claude tells you how to update.

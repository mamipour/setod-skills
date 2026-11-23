# Setod skills

The Setod forward-deployed engineer skill lets Claude Code and Cursor build, test, debug and publish Setod agents, and set up a business's reception. The editor's model does the thinking. Setod only answers tool calls.

You sign in to Setod with your Setod account the first time the server is used, and pick the workspace. One sign-in is one workspace.

## Claude (claude.ai, Claude Desktop and Cowork)

1. Customize > Plugins > Add > Add marketplace, and enter `mamipour/setod-skills`.
2. Install **setod-fde**, open its Connectors tab and click Connect to sign in to Setod.

Or add the parts yourself: Customize > Connectors > Add custom connector with `https://api.setod.com/mcp`, and Customize > Skills > Upload a skill with a zip of `skills/setod-fde`.

## Cursor and other clients

```bash
npx skills add mamipour/setod-skills
```

Update later with `npx skills update`. Add `https://api.setod.com/mcp` as a remote MCP server in your client's settings and sign in to Setod when it asks.

## Claude Code

```text
/plugin marketplace add mamipour/setod-skills
/plugin install setod-fde@setod
```

Then run `/mcp`, pick `setod` and sign in to Setod in the browser. Update later with `claude plugin update setod-fde@setod` (or /plugin, Marketplaces, setod, Update marketplace), then restart Claude Code.

Privacy: https://setod.com/privacy

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

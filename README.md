# Setod skills

The Setod forward-deployed engineer skill lets Claude Code and Cursor build, test, and diagnose Setod agents. The editor's model does the thinking. Setod only answers tool calls.

Create a token in Setod under Settings → Developer. One token is one workspace.

## Cursor and other clients

```bash
npx skills add mamipour/setod-skills
```

Update later with `npx skills update`. Paste the Cursor snippet from Settings → Developer into `~/.cursor/mcp.json`.

## Claude Code

```text
/plugin marketplace add mamipour/setod-skills
/plugin install setod-fde@setod
```

Or add the server yourself:

```bash
claude mcp add --transport http setod https://api.setod.com/mcp --header "Authorization: Bearer $SETOD_TOKEN"
```

The bundled `.mcp.json` reads `SETOD_TOKEN` from the environment.

# Wyro for Cursor and Claude Code

The architecture check for backends agents write. Wyro reads your backend's source and tells Cursor's agent which routes reach which tables, and which do so without authenticating, validating input or rate limiting. It is deterministic (no model), so the same code always gets the same answer.

## What's in the plugin

| Component | What it does |
|---|---|
| MCP server `wyro` | Runs `npx -y wyro-check@0.2.5 --mcp` locally. Tools: `check_backend`, `describe_backend`, `list_rules`. Prompts: `check`, `fix`, `map`, `ship`. |
| Rule `wyro-check` (Cursor) | Tells the agent to run the check after changing routes, handlers, middleware or schema, and to fix new findings rather than silence them. |
| Skill `wyro-check` | Run the check and report the verdict and top findings. |
| Skill `wyro-fix` | Fix findings most dangerous first, re-checking after each one. |

## Install in Claude Code

```
/plugin marketplace add DominicPaaul7/wyro-cursor-plugin
/plugin install wyro@wyro
```

## Requirements

Node.js 18 or newer (for `npx`). No account, no API key. Your code is read on your machine and is not uploaded.

## Use it

Ask the agent: *"Check this backend with Wyro"*, or just change a route and let the rule kick in.

To gate pull requests in CI as well, see [wyro.in/docs/ci](https://wyro.in/docs/ci).

## Links

- Website: [wyro.in](https://wyro.in)
- MCP setup for other editors: [wyro.in/docs/mcp](https://wyro.in/docs/mcp)
- npm: [wyro-check](https://www.npmjs.com/package/wyro-check)

## License

The plugin files in this repository are MIT licensed. The `wyro-check` package they run is distributed under its own license on npm.

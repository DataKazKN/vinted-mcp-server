# Contributing to Vinted MCP Server

Thanks for taking the time to look into contributing — this server is maintained by one indie developer, and outside contributions help a lot.

## Reporting bugs

Open an issue with:
- A clear reproduction (the exact tool call or query that breaks)
- Expected vs actual behavior
- Your MCP client (Claude Desktop, Cursor, Windsurf, Cline, etc.) and OS
- Relevant logs from your client (e.g. `~/Library/Logs/Claude/mcp-server-vinted.log` on macOS for Claude Desktop)

If the bug is anti-bot related (Vinted blocks, 403/429 errors, hangs after init) please also share the Apify run ID if you have one — server-side logs make debugging much faster.

## Suggesting features

Open an issue with the `enhancement` label. Describe:
- The use case (what problem you're trying to solve)
- How the tool would behave (input/output shape)
- Why the current tools don't cover it

## Development

```bash
git clone https://github.com/DataKazKN/vinted-mcp-server.git
cd vinted-mcp-server
npm install
npm run build      # typecheck via tsc
npm run bundle     # produce dist/bundle.js
```

To test locally with Claude Desktop, point your `claude_desktop_config.json` at the local bundle:

```json
{
  "mcpServers": {
    "vinted-dev": {
      "command": "node",
      "args": ["/absolute/path/to/vinted-mcp-server/dist/bundle.js"]
    }
  }
}
```

Restart Claude Desktop and your local build replaces the published version.

## Pull requests

- One logical change per PR — easier to review and revert if needed
- Match the existing structure in `src/tools/` and `src/resources/` (one file per tool/resource)
- TypeScript strict mode is on (`tsconfig.json`) — please don't loosen it
- Keep the bundle slim — externalize heavy dependencies in the `bundle` script if you need to add any
- Add a short note in the PR description about how you tested the change

## Code style

- Async/await over `.then()` chains
- `const` over `let` unless you genuinely reassign
- No `any` unless interacting with an untyped 3rd-party API; in that case isolate it behind a typed wrapper

## License

By contributing, you agree your contributions are licensed under the MIT License — the same as the rest of the project (see `LICENSE`).

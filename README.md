# Visual Sentinel: Claude plugins marketplace

Claude plugins and skills for [Visual Sentinel](https://visualsentinel.com), the six-layer website monitoring platform (uptime, performance, SSL, DNS, visual regression, content change).

This is a Claude Code plugin marketplace. Add it once, then install plugins from it.

## Install

```bash
claude plugin marketplace add github.com/VisualSentinel/claude-plugins
claude plugin install visual-sentinel@visualsentinel
```

Then export your Visual Sentinel API key:

```bash
export VS_API_KEY=vs_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Generate a key at https://visualsentinel.com/settings/api-keys.

## Plugins

### `visual-sentinel`

Manage monitors, triage incidents, and create new monitors directly from Claude. Bundles the `@visualsentinel/mcp-server` MCP server (16 tools), three skills, and three slash commands.

* See [`visual-sentinel/README.md`](./visual-sentinel/README.md) for the full feature list.

## Related

* **Public OpenAPI spec:** https://github.com/VisualSentinel/openapi
* **MCP server (raw):** https://github.com/VisualSentinel/mcp-server
* **npm:** [`@visualsentinel/mcp-server`](https://www.npmjs.com/package/@visualsentinel/mcp-server)
* **Hosted API reference:** https://visualsentinel.com/docs

## License

MIT. See [`LICENSE`](./LICENSE).

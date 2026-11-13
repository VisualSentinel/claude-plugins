# Visual Sentinel: Claude plugins marketplace

Claude plugins and skills for [Visual Sentinel](https://visualsentinel.com), the six-layer website monitoring platform (uptime, performance, SSL, DNS, visual regression, content change).

This is a Claude Code plugin marketplace. Add it once, then install plugins from it.

## Install

```bash
claude plugin marketplace add github.com/VisualSentinel/claude-plugins
claude plugin install visual-sentinel@visualsentinel
```

The first time Claude uses a Visual Sentinel tool, Claude Code opens a sign-in page. Approve the connection and the tools work in that workspace. Run `/mcp` to see or remove the connection.

## Plugins

### `visual-sentinel`

Manage monitors, triage incidents, and create new monitors directly from Claude. Connects to the hosted Visual Sentinel MCP server with sign-in and adds three skills and three slash commands.

* See [`visual-sentinel/README.md`](./visual-sentinel/README.md) for the full feature list.

## Related

* **Public OpenAPI spec:** https://github.com/VisualSentinel/openapi
* **Hosted MCP server:** https://visualsentinel.com/mcp
* **Hosted API reference:** https://visualsentinel.com/docs

## License

MIT. See [`LICENSE`](./LICENSE).

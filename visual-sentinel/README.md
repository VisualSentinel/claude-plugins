# Visual Sentinel plugin for Claude

Manage [Visual Sentinel](https://visualsentinel.com) monitors, incidents, and alerts from inside Claude Code, Claude Desktop, or any Claude client that supports the plugin format.

This plugin bundles:

* The `@visualsentinel/mcp-server` MCP server (17 tools across the public Visual Sentinel API, pinned to 0.2.1)
* Three task-focused skills:
  * `vs-monitor-status`: "what monitors are up/down" and uptime queries
  * `vs-incident-triage`: triage open incidents, summarise outages, acknowledge alerts
  * `vs-add-monitor`: walk through creating a new monitor with the right type
* Three slash commands wired to those skills:
  * `/vs-status [filter]`
  * `/vs-incidents [open|resolved|all]`
  * `/vs-add-monitor <url> [type]`

## Install

### Claude Code (recommended)

```bash
claude plugin marketplace add github.com/VisualSentinel/claude-plugins
claude plugin install visual-sentinel@visualsentinel
```

Then export your Visual Sentinel API key in the shell:

```bash
export VS_API_KEY=vs_live_xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Generate an API key at https://visualsentinel.com/settings/api-keys.

### Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "visualsentinel": {
      "command": "npx",
      "args": ["-y", "@visualsentinel/mcp-server"],
      "env": { "VS_API_KEY": "vs_live_..." }
    }
  }
}
```

Skills and slash commands are Claude Code features and do not apply to Claude Desktop. Claude Desktop users get the same 17 MCP tools, just without the skill / command sugar.

## What it does

After install, you can ask Claude things like:

* "Which of my Visual Sentinel monitors are down right now?" -> `/vs-status` or natural language; the `vs-monitor-status` skill walks through the right tool calls.
* "Triage incident `clm_xyz` and tell me what to do" -> `/vs-incidents`; the `vs-incident-triage` skill reads the check history and proposes next actions.
* "Add a visual regression monitor for `https://shop.example.com/checkout` with 1-minute checks" -> `/vs-add-monitor https://shop.example.com/checkout VISUAL`; the `vs-add-monitor` skill confirms before creating.
* "Check the SSL cert on `visualsentinel.com`" -> uses the public `vs_ssl_check` tool (no API key required).

## Configuration

| Variable | Purpose | Where |
|---|---|---|
| `VS_API_KEY` | Required for monitors / incidents / alerts / status pages / servers tools (Business and Agency plans). Generate at https://visualsentinel.com/settings/api-keys. | The plugin's `vs_api_key` setting, asked when you enable the plugin. In Claude Desktop, the MCP config file's `env` block. |
| `VS_API_BASE` | Override only for testing against a local Visual Sentinel dev instance. Defaults to `https://visualsentinel.com`. | Same. |

Public tools (`vs_health`, `vs_dns_check`, `vs_ssl_check`, `vs_speed_test`, `vs_website_check`) work without an API key.

## License

MIT. See `LICENSE` at the repository root.

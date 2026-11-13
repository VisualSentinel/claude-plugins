# Visual Sentinel plugin for Claude

Manage [Visual Sentinel](https://visualsentinel.com) monitors, incidents, and alerts from inside Claude Code, Claude Desktop, or any Claude client that supports the plugin format.

This plugin adds:

* A connection to the hosted Visual Sentinel MCP server (`https://visualsentinel.com/api/mcp`), with sign-in. Nothing is installed on your computer.
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

The first time Claude uses a Visual Sentinel tool, Claude Code opens a sign-in page. Approve the connection and the tools work in that workspace. Run `/mcp` to see or remove the connection.

### Claude Desktop and claude.ai

Add a custom connector with the URL `https://visualsentinel.com/api/mcp` and sign in when asked. Skills and slash commands are Claude Code features, so these clients get the same tools without them.

## What it does

After install, you can ask Claude things like:

* "Which of my Visual Sentinel monitors are down right now?" -> `/vs-status` or natural language; the `vs-monitor-status` skill walks through the right tool calls.
* "Triage incident `clm_xyz` and tell me what to do" -> `/vs-incidents`; the `vs-incident-triage` skill reads the check history and proposes next actions.
* "Add a visual regression monitor for `https://shop.example.com/checkout` with 1-minute checks" -> `/vs-add-monitor https://shop.example.com/checkout VISUAL`; the `vs-add-monitor` skill confirms before creating.
* "Check the SSL cert on `visualsentinel.com`" -> uses the `vs_ssl_check` tool, which checks any site, monitored or not.

## License

MIT. See `LICENSE` at the repository root.

---
name: vs-monitor-status
description: Use when the user asks about the current status of one or more Visual Sentinel monitors, wants to know what is up or down, or asks for an uptime summary. Triggers on phrases like "are my sites up", "what monitors are down", "uptime for X", "show me the status of my monitors".
---

# Visual Sentinel: monitor status

Use the bundled `@visualsentinel/mcp-server` MCP tools to answer Visual Sentinel monitor-status questions. Do not invent data; always call a tool.

## Tool selection

| User intent | Tool | Notes |
|---|---|---|
| "Are any of my monitors down?" | `vs_monitors_list` | Pass `status: "DOWN"`. If empty, also try `status: "PAUSED"` to surface paused monitors that should be UP. |
| "Status of monitor X" (id known) | `vs_monitors_get` | Returns current status + last check. |
| "Status of monitor X" (only name known) | `vs_monitors_list` first to find the id, then `vs_monitors_get`. | Match by exact `name` field; if multiple match, list all and let the user pick. |
| "Uptime over the last N days" | `vs_monitors_uptime` | `window`: `24h`, `7d`, `30d`, `90d`, `365d`. Default to `30d` if unspecified. |
| "Run a quick check on this URL right now" | `vs_website_check` (public, no auth) for a one-shot read; OR `vs_monitors_check_now` if a registered monitor exists. | Prefer `vs_monitors_check_now` when a registered monitor is the source of truth. |

## Output style

Default to a compact table of monitors with: name, type, current status, last-check timestamp, response time. Group DOWN monitors first, then PAUSED, then UP. If the user asked about a single monitor, show a denser per-field summary instead.

For uptime queries, lead with the headline percentage and outage minutes for the requested window. Follow with the count and duration of incidents.

## Auth

`vs_monitors_*` and `vs_alerts_*` tools require `VS_API_KEY`. If the MCP server returns a 401 or "API key required" error, instruct the user to set `VS_API_KEY` (https://visualsentinel.com/settings/api-keys) and retry. Public tools (`vs_website_check`, `vs_dns_check`, `vs_ssl_check`, `vs_speed_test`) work without a key for ad-hoc lookups.

## Anti-patterns

* Do not summarize without calling a tool. The user needs current data, not what was true last conversation.
* Do not blindly resolve names to ids. If `vs_monitors_list` returns multiple monitors with the same name, show the list and ask which one.
* Do not call `vs_monitors_check_now` without confirming the user wants a check triggered. It costs an extra check against their plan limits.

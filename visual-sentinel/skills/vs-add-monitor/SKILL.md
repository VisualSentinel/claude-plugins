---
name: vs-add-monitor
description: Use when the user wants to add a new Visual Sentinel monitor. Triggers on phrases like "add a monitor for X", "monitor this URL", "set up uptime checks for example.com", "watch this page for visual changes".
---

# Visual Sentinel: add a monitor

Use the bundled `@visualsentinel/mcp-server` `vs_monitors_create` tool to add a new monitor. Confirm critical fields with the user before creating.

## Required fields

| Field | Source |
|---|---|
| `name` | Suggest one from the URL hostname plus context, e.g. "Production checkout (shop.example.com)". Confirm with the user before creating. |
| `url` | The URL or hostname to monitor. Include the protocol for HTTP/HTTPS/API/GRAPHQL/WEBSOCKET monitors. Bare hostnames are fine for PING/PORT/DNS/SSL. |
| `type` | One of: `HTTP`, `HTTPS`, `KEYWORD`, `PING`, `PORT`, `DNS`, `SSL`, `VISUAL`, `CONTENT`, `API`, `GRAPHQL`, `WEBSOCKET`. |

## Type selection guide

* The user said "monitor my homepage" or "check this page is up" -> `HTTPS` (or `HTTP` if no TLS).
* "Watch this page for visual changes" -> `VISUAL`.
* "Tell me when the price / banner / key text disappears" -> `CONTENT` (or `KEYWORD` if it is a single keyword assertion).
* "Make sure my SSL cert does not expire" -> `SSL`. (Visual Sentinel monitors SSL on every HTTPS check too, but a dedicated SSL monitor surfaces expiry warnings sooner.)
* "Check that DNS still resolves" -> `DNS`.
* "Test this REST API endpoint" -> `API` (with optional auth headers and assertion configuration set later in the dashboard).
* "Ping this server" -> `PING`. "Check this port is open" -> `PORT`.

## Optional fields

| Field | Default | When to set explicitly |
|---|---|---|
| `interval` | 300 (5 min) | Set 60 for production critical paths, 1800 for low-priority informational checks. |
| `timeout` | 30 | Increase for slow endpoints (image-heavy pages, payment processors). |
| `method` | GET (HTTP/HTTPS only) | Set when the user wants to monitor a POST/PUT endpoint. |
| `keyword` | (none) | Required for KEYWORD type. The exact text the response must contain. |
| `port` | (varies) | Required for PORT type. |

## Workflow

1. Read the user's request. Identify the URL and the implied monitor `type` from intent.
2. Confirm with the user: "I'll create a `<type>` monitor named `<name>` for `<url>`, checking every `<interval>` seconds. OK?"
3. On confirmation, call `vs_monitors_create`.
4. Echo back the created monitor's id, status, and a deep-link to its dashboard page (`https://visualsentinel.com/monitors/<id>`).
5. Suggest the natural next step: "Want me to wire up alerts (Slack / Email / WhatsApp) for this monitor?" If yes, list configured channels via `vs_status_pages_list` is wrong here, hint instead that the user should call channel-management tools or visit the dashboard.

## Auth

`vs_monitors_create` requires `VS_API_KEY` with write permission. If the user only has a read-only key, the call returns 403; surface the error and direct them to https://visualsentinel.com/settings/api-keys.

## Anti-patterns

* Do not silently default to a `type` the user did not ask for. If intent is ambiguous (e.g. "monitor my site" without specifying visual or uptime), ask.
* Do not guess at custom HTTP headers, request bodies, or auth schemes. Create the monitor with sensible defaults and tell the user to refine in the dashboard at the deep-link URL.
* Do not create multiple monitors at once without confirmation. Each monitor counts against the plan limit.

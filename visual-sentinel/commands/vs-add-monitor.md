---
description: Add a Visual Sentinel monitor for a URL. Usage: /vs-add-monitor <url> [type]
---

Use the `vs-add-monitor` skill workflow. The first argument is the URL or hostname; the optional second argument is the monitor type (HTTP, HTTPS, VISUAL, CONTENT, SSL, DNS, PING, PORT, API, GRAPHQL, WEBSOCKET, KEYWORD). If type is omitted, infer from the URL (default to HTTPS for `https://` URLs, HTTP for `http://`, PING for bare hostnames).

Confirm name and interval with the user before calling `vs_monitors_create`. After creation, echo the monitor id and the dashboard deep-link.

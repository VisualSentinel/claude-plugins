---
description: Show a quick summary of Visual Sentinel monitor status (down monitors first, then paused, then up).
---

Use the `vs_monitors_list` MCP tool. First call it with `status: "DOWN"`, then `status: "PAUSED"`, then `status: "UP"` (limit 10 each). Combine into a single compact table grouped by status. Lead with the count of DOWN monitors.

If the user passes arguments, treat them as a filter applied to the monitor `name` field (case-insensitive substring match) and narrow the displayed rows accordingly.

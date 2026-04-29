---
description: List open Visual Sentinel incidents and triage them. Usage: /vs-incidents [open|resolved|all]
---

Use the `vs-incident-triage` skill workflow. Default to listing OPEN incidents only. If the argument is `resolved`, list RESOLVED incidents from the last 7 days. If `all`, list both with OPEN first.

For each incident, surface: monitor name, started timestamp (relative + absolute), probable cause from the check history, and one suggested next action. Do not auto-acknowledge or auto-resolve.

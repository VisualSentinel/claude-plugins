---
name: vs-incident-triage
description: Use when the user asks about Visual Sentinel incidents, wants to triage what is happening, asks for a postmortem on a recent outage, or wants to acknowledge or resolve alerts. Triggers on phrases like "what incidents do I have open", "triage this incident", "summarise the last outage", "acknowledge the alert for X".
---

# Visual Sentinel: incident triage

Use the bundled `@visualsentinel/mcp-server` MCP tools to triage incidents and alerts. Always pull live data; never speculate.

## Triage workflow

1. **List open incidents.** Call `vs_incidents_list` with `status: "OPEN"`. If the user mentioned a specific monitor, also pass `monitorId`.
2. **For each incident, fetch the full picture.** Call `vs_incidents_get` to get the check history, root-cause hints, and timestamps. The check history shows the last 50 checks around the failure window.
3. **Run external diagnostics if symptoms suggest infrastructure issues.**
   * Status code returns 502/503/504 -> upstream / origin server problem -> consider `vs_speed_test` against the URL to see what HTTP layer is responding now, and `vs_dns_check` if the URL recently changed CDN.
   * SSL handshake failed -> `vs_ssl_check` against the host to inspect cert validity, expiry, chain.
   * "Site looks broken but HTTP 200" -> visual regression incident -> the incident object includes a screenshot diff URL; surface it to the user.
4. **Summarise.** Lead with: what failed, when it started, current status. Then: probable cause from check history. Then: suggested next action.
5. **Act with confirmation.** If the user wants to acknowledge an alert, call `vs_alerts_acknowledge` with an optional note. Acknowledging means "we are aware and looking at it" but does not resolve the alert.

## Output style

Per incident, default format:

```
[<incident-id>] <monitor name>  (<incident status>)
  Started:  <timestamp> (X minutes ago)
  Cause:    <one-line summary of why it fired>
  History:  <consecutive failure count> checks failed; last success at <timestamp>
  Next:     <one suggested action>
```

For postmortems on already-resolved incidents, lead with the duration and the resolution timestamp instead.

## Auth

All `vs_incidents_*` and `vs_alerts_*` tools require `VS_API_KEY`. If unauthenticated, prompt the user to set the env var (https://visualsentinel.com/settings/api-keys) before retrying.

## Anti-patterns

* Do not invent root causes. Stick to what the check history actually shows.
* Do not auto-acknowledge alerts. Always confirm with the user first.
* Do not call `vs_monitors_check_now` during triage unless the user explicitly asks for a fresh check; the existing incident data already shows the failure pattern.
* Do not paraphrase status codes incorrectly: a 200 with a visual diff is a "visual regression", not a "false positive".

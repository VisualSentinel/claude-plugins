# Changelog

All notable changes to the Visual Sentinel Claude plugins marketplace.

## [0.2.2] - 2026-11-09

### Changed

* `visual-sentinel` plugin pins `@visualsentinel/mcp-server@0.2.2` (its npm homepage now points at visualsentinel.com/mcp; no tool changes).

## [0.1.0] - 2026-04-29

Initial public release.

### Added

* Marketplace metadata at `.claude-plugin/marketplace.json` listing one plugin (`visual-sentinel`).
* `visual-sentinel` plugin (v0.1.0):
  * Bundles the `@visualsentinel/mcp-server` MCP server via `.mcp.json`.
  * Three skills: `vs-monitor-status`, `vs-incident-triage`, `vs-add-monitor`.
  * Three slash commands: `/vs-status`, `/vs-incidents`, `/vs-add-monitor`.
  * Plugin metadata at `visual-sentinel/.claude-plugin/plugin.json`.
* MIT license at the marketplace root.

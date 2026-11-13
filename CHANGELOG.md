# Changelog

All notable changes to the Visual Sentinel Claude plugins marketplace.

## [0.2.5] - 2026-11-13

### Changed

* The plugin now connects to the hosted Visual Sentinel MCP server with sign-in; no API key and nothing installed on your computer.

## [0.2.4] - 2026-11-10

### Changed

* `visual-sentinel` plugin pins `@visualsentinel/mcp-server@0.2.3`: its plans resource, tool error and prompts state the current offer (a 10-day free trial, no card with a work email) and that API keys come with every paid plan, including the trial. No tool changes.

## [0.2.3] - 2026-11-09

### Fixed

* `visual-sentinel` plugin description, the `vs_api_key` setting and the plugin README now say API keys (and so the account tools) come with every paid plan (Solo, Starter, Business and Agency), including the 10-day free trial. They used to say Business and Agency only.

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

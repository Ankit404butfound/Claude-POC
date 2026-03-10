# Claude Workspace Configuration

This directory contains lightweight guidance to improve response quality and reduce token usage.

## Files
- `instructions.md`: Default repo behavior and quality rules.
- `context/global.md`: Shared OMS context included by default.
- `context/service-map.md`: Which service docs to load by task.
- `templates/design-task.md`: Template for architecture and design prompts.
- `templates/bugfix-task.md`: Template for debugging and fixes.
- `templates/api-contract-task.md`: Template for API/event contract work.

## Usage
1. Start with `context/global.md`.
2. Add only relevant service docs from `services/*/claude.md`.
3. Use a template from `templates/`.
4. Ask for extra context only when truly required.

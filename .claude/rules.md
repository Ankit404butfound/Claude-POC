# OMS Rules (Canonical)

## Context Loading
- Load `.claude/context/global.md` first.
- Load only relevant `services/<service>/claude.md` files.
- Do not load all services unless explicitly requested.
- Ask for specific missing files when context is insufficient.

## Architecture
- Preserve strict service boundaries.
- Prefer event-driven integration for async workflows.
- Ensure idempotency for state-changing operations.
- Integrate via contracts, not service internals.

## Security and Compliance
- Require authentication and RBAC in all designs.
- Protect sensitive data in transit and at rest.
- Ensure critical actions are auditable.
- Minimize personal data in logs and events.

## API and Change Strategy
- Follow RESTful conventions.
- Keep names consistent across APIs and events.
- Prefer additive, backward-compatible changes.
- Explicitly state non-goals to prevent scope creep.

## Output Quality
- Keep outputs concise and implementation-focused.
- Make assumptions explicit.
- Highlight cross-service impact for contract changes.
- Include backward compatibility notes for API changes.
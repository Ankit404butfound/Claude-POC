# OMS Global Context

Minimal workspace context for prompt bootstrapping.

## Service Summary
- `admin`: access control, config, audit controls
- `customer`: profile, addresses, preferences, account status
- `inventory`: stock, reservations, warehouse allocation, movements
- `notification`: templates, channel delivery, delivery status
- `order`: order lifecycle, validation, cancellation/returns initiation
- `payments`: authorize/capture, refunds, reconciliation
- `reporting`: analytics, exports, dashboards
- `shipping`: shipments, carriers, tracking, delivery updates

## Core Flow
Customer -> Order -> Payments -> Inventory -> Shipping -> Notification -> Reporting

## Canonical Rules
All rules are centralized in:
- `.claude/rules.md`

Use this file first, then load only task-relevant `services/<service>/claude.md` files.

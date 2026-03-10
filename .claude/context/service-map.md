# Service Context Routing

Use this map to select minimal service context for each task.

## Common Task -> Services
- Create order flow: `order`, `customer`, `inventory`, `payments`, `notification`
- Cancel order flow: `order`, `inventory`, `payments`, `notification`
- Refund workflow: `payments`, `order`, `notification`, `reporting`
- Shipping tracking issue: `shipping`, `order`, `notification`
- Stock mismatch: `inventory`, `order`, `reporting`
- Admin policy/config change: `admin` (+ affected domain service)
- Customer preference notification issue: `customer`, `notification`
- KPI/dashboard request: `reporting` (+ source services)

## Minimal Loading Rule
- Load 1 to 3 service docs by default.
- Add more only when contracts or flows cross boundaries.
- Avoid full-repo context loading unless explicitly requested.

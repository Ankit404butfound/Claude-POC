
# Reporting Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Reporting Service provides analytics and operational reporting for the Order Management System (OMS).  
It aggregates data from multiple services and exposes queryable metrics and report outputs.

This service provides APIs for admin dashboards, finance teams, and operations stakeholders.

This service **does NOT execute order transactions, payment processing, or shipping operations**.

---

## Responsibilities

The Reporting Service is responsible for:

- Aggregated metrics generation
- Business report generation
- Operational KPI tracking
- Scheduled report exports
- Report filtering and drill-down queries
- Historical trend analysis
- Data quality and freshness checks

---

## Core Modules

### 1. Metrics Aggregation
Builds aggregate metrics from OMS event and transactional data.

Functions:
- Aggregate order metrics
- Aggregate payment metrics
- Aggregate inventory and shipping metrics
- Compute SLA and throughput metrics

Key Entity:
- MetricSnapshot

---

### 2. Report Generation
Generates reusable business reports.

Functions:
- Generate sales report
- Generate fulfillment report
- Generate cancellation and return report
- Generate payment reconciliation report

Key Entity:
- ReportDefinition

---

### 3. Scheduled Exports
Creates scheduled report files and delivery jobs.

Examples:
- Daily CSV export
- Weekly finance report
- Monthly operations summary
- Custom date-range export

---

### 4. Dashboard Queries
Provides optimized endpoints for dashboards and BI tools.

Examples:
- Orders by status
- Revenue by day
- Top products by volume
- Delivery SLA compliance

---

### 5. Data Freshness and Audit
Tracks report lineage and data freshness guarantees.

Examples:
- Last refresh timestamp
- Source data lag indicators
- Report execution logs
- Job failure alerts

---

## API Endpoints (Sample)

### Metrics

GET /reports/metrics/orders
GET /reports/metrics/payments
GET /reports/metrics/fulfillment


### Reports

POST /reports/generate
GET /reports/{reportId}
GET /reports


### Scheduled Jobs

POST /reports/schedules
GET /reports/schedules
PUT /reports/schedules/{scheduleId}
DELETE /reports/schedules/{scheduleId}


### Exports

POST /reports/exports
GET /reports/exports/{exportId}


### Health and Freshness

GET /reports/freshness

---

## Data Model (Example)

### ReportDefinition

id
name
description
query_template
format
created_at
updated_at


### MetricSnapshot

id
metric_name
metric_value
dimension
snapshot_time


### ReportSchedule

id
report_id
cron_expression
delivery_channel
status
updated_at


### ReportExecutionLog

id
report_id
started_at
completed_at
status
error_message

---

## Security Requirements

- All APIs must require authentication.
- Access to reports must be role-based and scoped.
- Sensitive fields must be masked in report outputs where required.
- Export artifacts must be access-controlled and time-limited.
- Report execution and downloads must be auditable.

---

## Dependencies

The Reporting Service may interact with:

- Order Service
- Payments Service
- Inventory Service
- Shipping Service
- Notification Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process live order transactions
- Authorize or capture payments
- Manage inventory reservations
- Dispatch shipments

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure query performance and pagination standards
- Avoid tight coupling with source service schemas

---

## Future Enhancements

- Self-service report builder
- Near real-time analytics pipeline
- Anomaly detection alerts
- Multi-tenant report isolation

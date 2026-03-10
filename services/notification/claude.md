# Notification Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Notification Service manages outbound communication for the Order Management System (OMS).  
It sends transactional and operational notifications through configured channels.

This service provides APIs and event consumers for internal systems such as Order Service, Shipping Service, and Payments Service.

This service **does NOT own order processing, payment execution, or customer profile management**.

---

## Responsibilities

The Notification Service is responsible for:

- Message template management
- Channel delivery orchestration
- Notification preferences enforcement
- Retry and failure handling
- Delivery status tracking
- Notification audit logs
- Event-driven notification triggering

---

## Core Modules

### 1. Template Management
Stores and manages reusable notification templates.

Functions:
- Create template
- Update template
- Activate or deactivate template
- Preview rendered template
- Version templates

Key Entity:
- NotificationTemplate

---

### 2. Channel Delivery
Handles sending notifications through supported channels.

Functions:
- Send email notification
- Send SMS notification
- Send push notification
- Select channel by preference and policy
- Fallback to secondary channel

Key Entity:
- NotificationMessage

---

### 3. Preference Enforcement
Applies customer-level communication settings before delivery.

Examples:
- Opt-out checks
- Quiet-hour checks
- Channel allowlist checks
- Marketing consent checks

---

### 4. Retry and Dead Letter Handling
Manages failed notification retries and dead-letter flows.

Examples:
- Exponential backoff retries
- Max retry threshold
- Dead-letter queue routing
- Manual replay

---

### 5. Delivery Tracking
Tracks each notification lifecycle state.

Status Types:
- Queued
- Sent
- Delivered
- Failed
- Suppressed

---

## API Endpoints (Sample)

### Templates

POST /notifications/templates
GET /notifications/templates
GET /notifications/templates/{templateId}
PUT /notifications/templates/{templateId}


### Send Notifications

POST /notifications/send
POST /notifications/send/bulk


### Delivery Status

GET /notifications/{notificationId}/status
GET /notifications/status


### Preferences

GET /notifications/preferences/{customerId}
PUT /notifications/preferences/{customerId}


### Audit Logs

GET /notifications/audit-logs

---

## Data Model (Example)

### NotificationTemplate

id
name
channel
subject
body
version
status
updated_at


### NotificationMessage

id
template_id
customer_id
channel
payload
status
scheduled_at
sent_at
updated_at


### NotificationPreference

customer_id
email_enabled
sms_enabled
push_enabled
marketing_opt_in
updated_at


### NotificationAuditLog

id
notification_id
event_type
event_payload
created_at

---

## Security Requirements

- All APIs must require authentication.
- Outbound provider credentials must be securely managed.
- Sensitive payload fields must be masked in logs.
- Access to notification logs must follow RBAC policies.
- Suppression and consent rules must be strictly enforced.

---

## Dependencies

The Notification Service may interact with:

- Order Service
- Shipping Service
- Payments Service
- Customer Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process orders
- Execute payment transactions
- Maintain customer master profile data
- Manage inventory availability

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure idempotency for send operations
- Avoid tight coupling with external providers

---

## Future Enhancements

- Intelligent send-time optimization
- Template localization workflows
- Provider failover routing
- Real-time delivery analytics

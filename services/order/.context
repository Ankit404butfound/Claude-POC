
# Order Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Order Service manages the full order lifecycle for the Order Management System (OMS).  
It handles order creation, validation, state transitions, and order history.

This service provides APIs for customer-facing applications and internal services such as Payments, Inventory, and Shipping.

This service **does NOT directly process payments, maintain inventory stock, or execute shipment delivery**.

---

## Responsibilities

The Order Service is responsible for:

- Order creation and updates
- Order item and pricing snapshot storage
- Order status lifecycle management
- Order cancellation and return initiation
- Order lookup and history
- Integration orchestration with payment and inventory flows
- Order event publishing

---

## Core Modules

### 1. Order Management
Handles creation and modification of orders.

Functions:
- Create order
- Update order details
- Add or remove order items before confirmation
- Get order by ID
- List orders by customer

Key Entity:
- Order

---

### 2. Order Validation
Validates order inputs and business rules.

Functions:
- Validate customer eligibility
- Validate item availability request
- Validate address and fulfillment constraints
- Validate order totals and tax snapshot

Key Entity:
- OrderValidationResult

---

### 3. Order Status Lifecycle
Manages order state transitions.

Status Types:
- Created
- Confirmed
- Paid
- Packed
- Shipped
- Delivered
- Cancelled
- Returned

---

### 4. Cancellation and Returns
Supports cancellation and return initiation workflows.

Examples:
- Cancel before shipment
- Partial item cancellation
- Return request creation
- Refund initiation trigger

---

### 5. Order Events
Publishes lifecycle events to downstream services.

Examples:
- order.created
- order.confirmed
- order.cancelled
- order.shipped

---

## API Endpoints (Sample)

### Orders

POST /orders
GET /orders
GET /orders/{orderId}
PUT /orders/{orderId}


### Order Status

PUT /orders/{orderId}/status
GET /orders/{orderId}/status


### Cancellations

POST /orders/{orderId}/cancel


### Returns

POST /orders/{orderId}/returns
GET /orders/{orderId}/returns


### Order History

GET /orders/customer/{customerId}

---

## Data Model (Example)

### Order

id
customer_id
status
currency
subtotal
tax_amount
discount_amount
total_amount
created_at
updated_at


### OrderItem

id
order_id
sku
product_name
quantity
unit_price
line_total


### OrderStatusHistory

id
order_id
from_status
to_status
changed_by
changed_at


### ReturnRequest

id
order_id
reason
status
created_at
updated_at

---

## Security Requirements

- All APIs must require authentication.
- Access to order data must follow RBAC policies.
- Customer-specific data access must enforce ownership checks.
- Sensitive personal and pricing data must be protected.
- All status changes must be auditable.

---

## Dependencies

The Order Service may interact with:

- Customer Service
- Inventory Service
- Payments Service
- Shipping Service
- Notification Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Execute payment gateway transactions
- Manage physical stock quantities
- Handle shipping carrier dispatch
- Manage admin authorization policies

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure idempotency for create and status operations
- Avoid tight coupling with other services

---

## Future Enhancements

- Split-order support
- Advanced return workflows
- Smart order routing by warehouse
- Fraud-risk scoring integration

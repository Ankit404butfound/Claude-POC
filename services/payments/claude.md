
# Payments Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Payments Service manages payment transaction workflows for the Order Management System (OMS).  
It handles authorization, capture, refunds, and payment status tracking.

This service provides APIs for Order Service and internal finance or reconciliation systems.

This service **does NOT manage order item lifecycle, inventory stock, or shipping dispatch**.

---

## Responsibilities

The Payments Service is responsible for:

- Payment intent creation
- Payment authorization and capture
- Refund and reversal handling
- Payment method token references
- Payment status and reconciliation records
- Fraud and risk signal integration hooks
- Payment event publishing

---

## Core Modules

### 1. Payment Intent Management
Creates and manages intents before charging customers.

Functions:
- Create payment intent
- Update payment intent
- Cancel payment intent
- Retrieve payment intent status

Key Entity:
- PaymentIntent

---

### 2. Transaction Processing
Executes authorization and capture operations.

Functions:
- Authorize payment
- Capture payment
- Void authorization
- Sync transaction status

Key Entity:
- PaymentTransaction

---

### 3. Refund Management
Handles full and partial refunds.

Functions:
- Create refund
- Track refund status
- Retry failed refund
- Link refund to original transaction

Key Entity:
- Refund

---

### 4. Payment Method Handling
Stores payment method references and metadata.

Examples:
- Card token reference
- UPI token reference
- Wallet reference
- Last4 and brand metadata

---

### 5. Reconciliation and Audit
Maintains immutable records for settlement and finance reporting.

Examples:
- Gateway settlement status
- Reconciliation mismatch records
- Chargeback markers
- Processing fee snapshots

---

## API Endpoints (Sample)

### Payment Intents

POST /payments/intents
GET /payments/intents/{intentId}
PUT /payments/intents/{intentId}
DELETE /payments/intents/{intentId}


### Transactions

POST /payments/authorize
POST /payments/capture
POST /payments/void
GET /payments/transactions/{transactionId}


### Refunds

POST /payments/refunds
GET /payments/refunds/{refundId}


### Payment Status

GET /payments/orders/{orderId}/status


### Reconciliation

GET /payments/reconciliation

---

## Data Model (Example)

### PaymentIntent

id
order_id
customer_id
amount
currency
status
created_at
updated_at


### PaymentTransaction

id
intent_id
gateway_reference
transaction_type
amount
status
processed_at
updated_at


### Refund

id
transaction_id
amount
reason
status
created_at
updated_at


### ReconciliationRecord

id
transaction_id
gateway_status
internal_status
mismatch_flag
updated_at

---

## Security Requirements

- All APIs must require authentication.
- Payment-related operations must enforce strict authorization.
- Sensitive payment data must never be stored in raw form.
- PCI-relevant controls must be followed.
- All payment actions must be auditable.

---

## Dependencies

The Payments Service may interact with:

- Order Service
- Notification Service
- Reporting Service
- External Payment Gateway

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Manage order fulfillment lifecycle
- Track warehouse stock
- Execute shipping operations
- Store full customer profile data

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure idempotency for authorize, capture, and refund operations
- Avoid tight coupling with specific gateways

---

## Future Enhancements

- Smart payment routing
- Multi-currency settlement optimization
- Chargeback workflow automation
- Advanced fraud scoring integration

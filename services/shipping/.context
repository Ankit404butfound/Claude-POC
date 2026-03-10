
# Shipping Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Shipping Service manages fulfillment and shipment workflows for the Order Management System (OMS).  
It handles shipment creation, carrier integration, tracking updates, and delivery status management.

This service provides APIs for Order Service, warehouse operations, and customer tracking interfaces.

This service **does NOT process payments, maintain customer master data, or manage inventory procurement**.

---

## Responsibilities

The Shipping Service is responsible for:

- Shipment creation and updates
- Carrier rate and label integration
- Shipment tracking lifecycle management
- Delivery status synchronization
- Return shipment handling
- Shipping SLA and exception tracking
- Shipping event publishing

---

## Core Modules

### 1. Shipment Management
Creates and manages shipments linked to orders.

Functions:
- Create shipment
- Update shipment details
- Split shipment by items
- Get shipment by ID
- List shipments by order

Key Entity:
- Shipment

---

### 2. Carrier Integration
Integrates with external carriers for rates, labels, and tracking.

Functions:
- Fetch shipping rates
- Select carrier service level
- Generate shipping label
- Cancel label

Key Entity:
- CarrierBooking

---

### 3. Tracking Management
Maintains shipment tracking state transitions.

Status Types:
- LabelCreated
- PickedUp
- InTransit
- OutForDelivery
- Delivered
- FailedAttempt
- Returned

---

### 4. Delivery Exceptions
Handles delays and failed delivery scenarios.

Examples:
- Address issue
- Customer unavailable
- Weather delay
- Carrier operational delay

---

### 5. Return Shipments
Handles reverse logistics shipping workflows.

Examples:
- Create return label
- Track return transit
- Mark return delivered to warehouse
- Notify downstream services

---

## API Endpoints (Sample)

### Shipments

POST /shipping/shipments
GET /shipping/shipments
GET /shipping/shipments/{shipmentId}
PUT /shipping/shipments/{shipmentId}


### Carrier Operations

GET /shipping/rates
POST /shipping/labels
DELETE /shipping/labels/{labelId}


### Tracking

GET /shipping/track/{trackingNumber}
PUT /shipping/shipments/{shipmentId}/status


### Returns

POST /shipping/returns
GET /shipping/returns/{returnShipmentId}


### Exceptions

GET /shipping/exceptions

---

## Data Model (Example)

### Shipment

id
order_id
warehouse_id
carrier
service_level
tracking_number
status
shipped_at
delivered_at
updated_at


### CarrierBooking

id
shipment_id
carrier_reference
rate_amount
label_url
status
updated_at


### TrackingEvent

id
shipment_id
tracking_number
event_type
location
event_time


### ReturnShipment

id
order_id
shipment_id
tracking_number
status
created_at
updated_at

---

## Security Requirements

- All APIs must require authentication.
- Shipment and tracking access must be role and ownership scoped.
- Carrier integration credentials must be securely managed.
- Sensitive address data must be protected.
- All shipment status changes must be auditable.

---

## Dependencies

The Shipping Service may interact with:

- Order Service
- Inventory Service
- Notification Service
- Reporting Service
- External Carrier APIs

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process payment transactions
- Manage customer account profiles
- Authorize admin roles and permissions
- Handle inventory procurement planning

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure idempotency for shipment and label creation
- Avoid tight coupling with single carrier providers

---

## Future Enhancements

- Multi-carrier optimization engine
- Delivery ETA prediction
- Real-time tracking webhooks
- Cross-border shipping compliance rules

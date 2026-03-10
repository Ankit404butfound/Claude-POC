
# Inventory Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Inventory Service manages product stock information for the Order Management System (OMS).  
It tracks inventory quantities, stock reservations, warehouse-level availability, and stock movements.

This service provides APIs for internal systems such as Order Service, Shipping Service, and Reporting Service.

This service **does NOT process customer payments, customer profiles, or shipment execution**.

---

## Responsibilities

The Inventory Service is responsible for:

- Product stock management
- Warehouse inventory tracking
- Stock reservation and release
- Stock adjustments
- Inventory movement history
- Low-stock and out-of-stock status
- Inventory lookup and availability checks

---

## Core Modules

### 1. Stock Management
Handles available and on-hand inventory quantities.

Functions:
- Create inventory record
- Update stock quantity
- Get product stock by SKU
- Mark product as out-of-stock
- Manage reorder thresholds

Key Entity:
- InventoryItem

---

### 2. Warehouse Inventory Management
Tracks stock distribution across multiple warehouses.

Functions:
- Add warehouse stock
- Transfer stock between warehouses
- Update warehouse allocation
- View warehouse-wise availability

Key Entity:
- WarehouseStock

---

### 3. Reservation Management
Reserves stock during order placement and releases stock when needed.

Functions:
- Reserve stock for order
- Confirm reservation on order success
- Release reservation on cancellation or timeout
- View reservation status

Key Entity:
- StockReservation

---

### 4. Inventory Adjustments
Applies manual or automated stock corrections.

Examples:
- Damaged goods adjustment
- Returned items restock
- Cycle count correction
- Shrinkage adjustment

---

### 5. Inventory Movement History
Maintains immutable logs of inventory changes.

Examples:
- Stock in
- Stock out
- Reservation created/released
- Warehouse transfer

Movement logs are used for reconciliation and auditing.

---

## API Endpoints (Sample)

### Inventory Items

POST /inventory/items
GET /inventory/items
GET /inventory/items/{sku}
PUT /inventory/items/{sku}


### Warehouse Stock

GET /inventory/items/{sku}/warehouses
PUT /inventory/items/{sku}/warehouses/{warehouseId}
POST /inventory/transfers


### Reservations

POST /inventory/reservations
GET /inventory/reservations/{reservationId}
POST /inventory/reservations/{reservationId}/confirm
POST /inventory/reservations/{reservationId}/release


### Adjustments

POST /inventory/adjustments
GET /inventory/adjustments


### Movements

GET /inventory/movements

---

## Data Model (Example)

### InventoryItem

id
sku
product_id
available_quantity
reserved_quantity
reorder_level
status
updated_at


### WarehouseStock

id
sku
warehouse_id
quantity
updated_at


### StockReservation

id
order_id
sku
quantity
status
expires_at
created_at
updated_at


### InventoryMovement

id
sku
warehouse_id
movement_type
quantity
reference_type
reference_id
created_at

---

## Security Requirements

- All APIs must require authentication.
- Authorization must enforce service-level permissions.
- Stock adjustment APIs must be restricted to authorized roles.
- Inventory movement and adjustment logs must be immutable.
- Sensitive internal integration data must be protected in transit.

---

## Dependencies

The Inventory Service may interact with:

- Order Service
- Shipping Service
- Reporting Service
- Admin Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process customer payments
- Manage customer profile data
- Execute shipping and delivery operations
- Handle order pricing rules

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure idempotency for reservation and release operations
- Avoid tight coupling with other services

---

## Future Enhancements

- Predictive restocking recommendations
- Supplier integration for automated replenishment
- Real-time inventory streaming
- Multi-tenant inventory partitioning

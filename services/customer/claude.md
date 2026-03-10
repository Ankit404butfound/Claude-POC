# Customer Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Customer Service manages customer-related data for the Order Management System (OMS).  
It stores customer profiles, contact details, addresses, preferences, and account status.

This service provides APIs for internal systems that need customer information, such as Order Service and Notification Service.

This service **does NOT process orders, payments, inventory, or shipping workflows**.

---

## Responsibilities

The Customer Service is responsible for:

- Customer profile management
- Customer contact information
- Customer address management
- Customer preferences
- Customer account status management
- Customer lookup and search
- Customer order history references

---

## Core Modules

### 1. Customer Profile Management
Handles customer account profile lifecycle.

Functions:
- Create customer
- Update customer profile
- View customer details
- Deactivate customer account
- Manage customer metadata

Key Entity:
- Customer

---

### 2. Address Management
Manages customer shipping and billing addresses.

Functions:
- Add address
- Update address
- Delete address
- Set default shipping address
- Set default billing address

Key Entity:
- CustomerAddress

---

### 3. Customer Preferences
Stores customer-specific configuration and communication preferences.

Examples:
- Preferred language
- Preferred communication channel
- Notification preferences
- Marketing preferences

---

### 4. Customer Search
Allows internal services and admin tools to find customers quickly.

Search criteria:
- Customer ID
- Email
- Phone number
- Name
- Account status

---

### 5. Customer Status Management
Controls customer account lifecycle status.

Status Types:
- Active
- Inactive
- Suspended
- Deleted

---

## API Endpoints (Sample)

### Customers

POST /customers
GET /customers
GET /customers/{customerId}
PUT /customers/{customerId}
DELETE /customers/{customerId}


### Customer Addresses

POST /customers/{customerId}/addresses
GET /customers/{customerId}/addresses
PUT /customers/{customerId}/addresses/{addressId}
DELETE /customers/{customerId}/addresses/{addressId}


### Customer Preferences

GET /customers/{customerId}/preferences
PUT /customers/{customerId}/preferences


### Customer Search

GET /customers/search

Examples:
- /customers/search?email=test@example.com
- /customers/search?phone=9999999999
- /customers/search?name=John

---

## Data Model (Example)

### Customer

id
first_name
last_name
email
phone
status
created_at
updated_at


### CustomerAddress

id
customer_id
type
address_line1
address_line2
city
state
postal_code
country
is_default
created_at
updated_at

Address Types:
- shipping
- billing


### CustomerPreferences

customer_id
preferred_language
communication_channel
marketing_opt_in
notification_enabled
updated_at

---

## Security Requirements

- Customer data must be protected.
- All APIs must require authentication.
- Sensitive data must be encrypted where necessary.
- Access to customer data must follow RBAC policies.
- Personal data handling must comply with privacy regulations.

---

## Dependencies

The Customer Service may interact with:

- Order Service
- Notification Service
- Admin Service
- Auth Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process orders
- Manage inventory
- Process payments
- Handle shipping logistics

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- Ensure data validation on all inputs
- Avoid tight coupling with other services

---

## Future Enhancements

- Customer segmentation
- Loyalty programs
- Customer analytics
- Multi-tenant customer support
- GDPR compliance features

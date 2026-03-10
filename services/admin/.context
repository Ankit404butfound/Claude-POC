
# Admin Service – OMS

Canonical rules: `.claude/rules.md`

## Overview
The Admin Service manages administrative configuration and control features for the Order Management System (OMS).  
It handles system users, roles, permissions, configuration settings, and operational controls.

This service provides APIs for internal admin panels and other OMS services that require configuration or authorization data.

---

## Responsibilities

The Admin Service is responsible for:

- Admin user management
- Role and permission management
- System configuration
- Feature flags
- Audit logs
- Organization / tenant configuration
- Access control policies

This service **does NOT manage business operations like orders, inventory, or payments**.

---

## Core Modules

### 1. Admin User Management
Handles admin accounts and authentication metadata.

Functions:
- Create admin users
- Update admin profiles
- Activate / deactivate users
- Reset passwords
- Assign roles

Key Entity:
- AdminUser

---

### 2. Role Management
Defines roles used for system access.

Functions:
- Create role
- Update role
- Delete role
- Assign permissions to roles

Examples:
- Super Admin
- Operations Admin
- Support Admin
- Finance Admin

---

### 3. Permission Management
Defines fine-grained system permissions.

Examples:
- `order.read`
- `order.update`
- `inventory.read`
- `inventory.update`
- `admin.manage`

Roles are composed of permissions.

---

### 4. System Configuration
Stores global OMS configuration.

Examples:
- Default warehouse
- Order processing rules
- Shipping configuration
- Notification settings
- Integration settings

Configuration must support dynamic updates without system restart.

---

### 5. Feature Flags
Controls feature rollout.

Examples:
- Enable new order workflow
- Enable new shipping provider
- Enable experimental UI

Feature flags support:
- environment targeting
- tenant targeting
- gradual rollout

---

### 6. Audit Logging
Tracks administrative actions.

Examples:
- User login
- Role changes
- Permission changes
- Configuration updates

Audit logs must be immutable.

---

## API Endpoints (Sample)

### Admin Users

POST /admin/users
GET /admin/users
GET /admin/users/{id}
PUT /admin/users/{id}
DELETE /admin/users/{id}


### Roles

POST /admin/roles
GET /admin/roles
PUT /admin/roles/{id}
DELETE /admin/roles/{id}


### Permissions

GET /admin/permissions


### Configurations

GET /admin/config
PUT /admin/config


### Feature Flags

GET /admin/feature-flags
POST /admin/feature-flags
PUT /admin/feature-flags/{id}


### Audit Logs

GET /admin/audit-logs


---

## Data Model (Example)

### AdminUser

id
name
email
password_hash
status
role_id
created_at
updated_at


### Role

id
name
description
permissions[]
created_at


### Permission

id
code
description


### SystemConfig

key
value
environment
updated_at


---

## Security Requirements

- All APIs must require authentication.
- RBAC must be enforced for all admin operations.
- Sensitive data must be encrypted.
- Passwords must be hashed using bcrypt/argon2.
- All admin actions must produce audit logs.

---

## Dependencies

The Admin Service may interact with:

- Auth Service
- Order Service
- Inventory Service
- Notification Service

via internal APIs or service events.

---

## Non-Goals

This service should not:

- Process orders
- Manage inventory
- Process payments
- Handle customer authentication

Those responsibilities belong to other services.

---

## Development Guidelines

- Follow RESTful API design
- Maintain backward compatibility
- Write unit and integration tests
- All configuration changes must be audited
- Avoid tight coupling with other services

---

## Future Enhancements

- Multi-tenant support
- SSO integration
- Advanced policy engine
- Admin activity dashboards

# Service Catalog

## Public service

### `temple-api-gateway`

- public base URL for the mobile app
- exposes `/api/v1`
- routes requests to downstream services

## Internal platform services

### `temple-identity-service`

- sign-in
- session lifecycle
- current user lookup

### `temple-registration-service`

- self-service signup request
- referred signup request
- request tracking

### `temple-admin-service`

- pending request review
- approve or reject actions
- admin audit trail


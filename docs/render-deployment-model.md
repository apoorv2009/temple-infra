# Render Deployment Model

## Recommended topology

- `temple-api-gateway` as a public Render web service
- `temple-identity-service` as a Render web service
- `temple-registration-service` as a Render web service
- `temple-admin-service` as a Render web service
- one managed PostgreSQL database service or external Neon Postgres

## Routing

- the React Native app calls only the gateway
- the gateway communicates with internal services
- internal service URLs are provided through environment variables

## Standard start command

```bash
uvicorn app.main:app --host 0.0.0.0 --port $PORT
```


# Render Service Checklist

Use this checklist for each backend repo:

- connect GitHub repository to Render
- set Python runtime
- use `pip install -e .` as build command
- use `uvicorn app.main:app --host 0.0.0.0 --port $PORT` as start command
- configure `/health` as health check path
- add environment variables from the target environment file
- verify service-to-service URLs after deployment


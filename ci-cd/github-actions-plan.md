# GitHub Actions Plan

## Frontend

- install dependencies
- run lint
- later add type-check and Expo validation

## Backend services

- install package with `pip install -e .[dev]`
- run pytest
- later add Ruff and mypy if desired

## Deployment

- use protected main branch
- trigger Render auto-deploy on merge to main


# MarketFlow — Backend

**Repository:** `marketflow-backend`  
**Product:** Marketing operations SaaS for campaign planning, content calendars, approvals, channel tracking and performance reporting.

## Overview

This repository provides the server-side API, business rules, persistence and integrations for **MarketFlow**. The frontend is maintained in `marketflow-frontend`.

## Technology

- NestJS + TypeScript
- Prisma ORM
- PostgreSQL
- OpenAPI/Swagger
- ValidationPipe and DTO-based request validation

## Core capabilities

- Campaign and channel planning
- Content calendar and publishing status
- Creative and asset library metadata
- Approval workflow and comments
- UTM link builder and campaign tracking
- Performance dashboards
- Team permissions and audit history

## Architecture principles

- Modular, feature-oriented design.
- Versioned REST API (for example `/api/v1`).
- DTO/schema validation at every external boundary.
- Centralized exception handling and structured logs.
- Database migrations committed with the code.
- Authorization enforced server-side for every protected resource.
- OpenAPI documentation generated from the implementation.

## Getting started

### Prerequisites

- Git
- PostgreSQL
- For NestJS: Node.js active LTS and npm
- For .NET: .NET 10 SDK

### Install and run

```bash
npm ci
npx prisma generate
npx prisma migrate dev
npm run start:dev
```

### Environment variables

Create a local environment file or use environment variables supplied by your deployment platform. Never commit real credentials.

```env
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://postgres:change-me@localhost:5432/APP_DB?schema=public
JWT_ACCESS_SECRET=replace-with-a-long-random-secret
JWT_REFRESH_SECRET=replace-with-another-long-random-secret
CORS_ORIGINS=http://localhost:5173
```

Replace placeholders and keep secrets in a secret manager or deployment environment. Do not reuse development secrets in production.

## Suggested source structure

```text
src/
  modules/
  common/
  config/
  database/
  health/
prisma/
  schema.prisma
test/
```

## Initial domain modules

- Identity and authentication
- Organizations / tenants and memberships
- MarketFlow domain modules
- Notifications and background processing (when required)
- Audit events
- Health and readiness endpoints

## API conventions

- Use nouns for resources and standard HTTP methods.
- Return consistent error bodies with a trace/correlation ID.
- Validate pagination limits, sorting and filters.
- Use transactions for multi-step financial or inventory operations.
- Make retryable webhook and payment handlers idempotent.
- Publish and maintain an OpenAPI specification.

Example routes to design and document:

```text
GET    /api/v1/health
GET    /api/v1/resources
POST   /api/v1/resources
GET    /api/v1/resources/{id}
PATCH  /api/v1/resources/{id}
DELETE /api/v1/resources/{id}
```

Replace the example resource with the product's actual domain resources.

## Data and multi-tenancy

If multiple customer organizations share the service, include a tenant/organization identifier on tenant-owned records. Derive tenant access from the authenticated identity, scope every query by tenant, and test cross-tenant access denial. Never rely on a tenant ID supplied by the browser without authorization checks.

## Security baseline

- Hash passwords using a modern password-hashing algorithm; never store plaintext passwords.
- Prefer short-lived access tokens and securely managed refresh sessions.
- Enforce role/permission checks in the API.
- Rate-limit authentication and sensitive endpoints.
- Validate file uploads and restrict file types and sizes.
- Protect against injection, insecure direct object references and mass assignment.
- Use TLS, secret management, backups and dependency scanning.
- Minimize personal data and define retention/deletion policies.

## Testing

```bash
npm run lint
npm run test
npm run test:e2e
npm run build
```

Add unit tests for domain rules, integration tests against a test database, and end-to-end tests for authentication and the most important business workflows.

## Observability and operations

- Expose liveness and readiness health checks.
- Use structured logs with correlation IDs.
- Track request latency, error rates and background-job failures.
- Configure database backups and test restoration.
- Avoid logging passwords, tokens, payment details or unnecessary personal data.

## Deployment

Build a release artifact and deploy through a repeatable CI/CD pipeline. Use separate development, staging and production environments; apply migrations deliberately; configure HTTPS, CORS allowlists, health checks, backups and rollback procedures.

## Contributing

1. Create a feature branch.
2. Include migrations and tests for schema or behavior changes.
3. Update the OpenAPI contract and this README when endpoints change.
4. Run formatting, linting, tests and release build.
5. Submit a pull request describing security and data-impact considerations.

## License

Add the license selected by the repository owner before public distribution.

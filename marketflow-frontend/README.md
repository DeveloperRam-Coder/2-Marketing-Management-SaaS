# MarketFlow — Frontend

**Repository:** `marketflow-frontend`  
**Product:** Marketing operations SaaS for campaign planning, content calendars, approvals, channel tracking and performance reporting.

## Overview

This repository contains the web application for **MarketFlow**. It is the customer-facing interface and communicates with the matching backend through versioned HTTPS APIs.

## Technology

- React (current stable release) + TypeScript + Vite + TanStack Query + React Router
- TypeScript with strict type checking
- Responsive, accessible component design
- Environment-based API configuration
- Automated unit and browser-level tests

## Core product areas

- Campaign and channel planning
- Content calendar and publishing status
- Creative and asset library metadata
- Approval workflow and comments
- UTM link builder and campaign tracking
- Performance dashboards
- Team permissions and audit history

## Getting started

### Prerequisites

- Node.js active LTS release and npm
- The matching backend running locally
- Git

### Install and run

```bash
npm ci
npm run dev
```

For Angular, use the workspace's configured start script (commonly `ng serve`). For React, Vite serves the development app.

### Environment configuration

Create a local environment file using the project's example file. Never commit secrets.

Typical settings:

```env
# Use the framework's supported public environment mechanism.
API_BASE_URL=http://localhost:3000/api/v1
```

For Angular, configure public values through Angular environment files or runtime configuration. For Vite, expose only intentionally public values with the `VITE_` prefix (for example `VITE_API_BASE_URL`). Do not put private API keys in frontend variables.

## Suggested frontend structure

```text
src/
  app-or-app/
  components/
  features/
  routes/
  services/
  hooks-or-state/
  models/
  styles/
  assets/
  environments/
```

Organize code by feature as the product grows. Keep API access in typed services, centralize error handling, and avoid placing business rules only in the browser.

## API integration

- Use the backend's OpenAPI/Swagger document as the API contract.
- Send access tokens using the agreed secure authentication approach.
- Handle loading, empty, validation, authorization and server-error states.
- Paginate large lists and debounce search inputs.
- Never trust client-side role checks as a security boundary.

## Quality checks

Add and run the scripts configured in `package.json`, such as:

```bash
npm run lint
npm run typecheck
npm test
npm run build
```

Use component tests for interactive UI and end-to-end tests for critical user journeys. The exact scripts depend on the generated project.

## Accessibility and UX

- Support keyboard navigation and visible focus states.
- Use semantic HTML and labelled form controls.
- Provide responsive layouts and useful empty states.
- Confirm destructive actions and show actionable error messages.

## Build and deployment

```bash
npm run build
```

Deploy the generated static assets to a supported static host or CDN. Configure the production API URL, HTTPS, SPA route fallback and appropriate Content Security Policy. Keep preview, staging and production configuration separate.

## Security

- Do not store secrets or privileged API credentials in the browser.
- Sanitize and validate user-provided content.
- Avoid logging personal or financial information.
- Use HTTPS and secure session/token handling.
- Follow applicable privacy and accessibility requirements.

## Contributing

1. Create a feature branch.
2. Keep changes focused and add tests.
3. Run lint, type checks, tests and production build.
4. Open a pull request with screenshots for UI changes and notes for API changes.

## License

Add the license selected by the repository owner before public distribution.

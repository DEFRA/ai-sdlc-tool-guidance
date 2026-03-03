# Real-World Example — Node.js/Hapi Service Instructions

This page shows a complete, production-tested `.github/copilot-instructions.md` file for a Defra Node.js/Hapi/Nunjucks GOV.UK service. Use it as a reference when writing instructions for your own project.

This example combines root-level instructions with detailed guidance that could alternatively be split into scoped instruction files. Both approaches work — the right choice depends on your project's complexity.

## What makes this example effective

- **Specific project context** — names the exact tech stack, paths, and architecture decisions
- **Security specifics** — does not just say "follow OWASP" but spells out CSP, CSRF, cookie, and header rules
- **Naming conventions** — removes ambiguity about file and URL naming
- **Allowed and discouraged dependencies** — prevents Copilot from suggesting outdated or non-compliant packages
- **"How Copilot should respond"** section — sets explicit behavioural expectations for the AI
- **Compact format** — everything a developer and Copilot need, in one file

## Example file contents

The content below is a complete `.github/copilot-instructions.md` for a Hapi/Nunjucks GOV.UK service:

---

````markdown
# Project Instructions

## Project overview

This is a GOV.UK-styled digital service for Defra, built with Node.js and Hapi. It serves HTML pages using Nunjucks templates and the GOV.UK Design System. This application is part of a microservice architecture design, with a frontend for user interaction and a backend API for data processing. It is multi-repository, with separate repositories for the frontend and backends.

- **Runtime**: Node.js (Active LTS)
- **Language**: Vanilla JavaScript (ES modules)
- **Framework**: Hapi
- **Templating**: Nunjucks with GOV.UK Frontend
- **Asset bundling**: Webpack 5
- **Hosting**: Containerised with Docker on: AWS ECS / Azure AKS

## Project paths quick reference

```
src/
├── config/           # Server and environment configuration
├── plugins/          # Hapi plugins (auth, CSRF, CSP, views, session)
├── routes/           # Route handlers — one file per route group
├── services/         # Business logic — called by route handlers
├── utils/            # Shared utilities (validation helpers, formatters)
├── views/
│   ├── layouts/      # Nunjucks base layouts (main.njk)
│   ├── partials/     # Reusable template fragments
│   ├── macros/       # GOV.UK component macros
│   ├── errors/       # Error page templates (404, 500)
│   └── pages/        # Page-level templates
├── public/           # Static assets (CSS, images, compiled JS)
└── __tests__/        # Test files mirroring src/ structure
```

## Naming conventions

- **Directories and templates**: `kebab-case` (e.g. `submit-application.njk`)
- **JavaScript files**: `camelCase` (e.g. `applicationService.js`)
- **Route paths (URLs)**: lowercase with hyphens (e.g. `/submit-application`)
- **Environment variables**: `UPPER_SNAKE_CASE` (e.g. `DATABASE_HOST`)

## Tech stack and standards

- Use Hapi for all HTTP servers — do not use Express
- Use Nunjucks for server-side rendering — do not use React, Vue, or Angular
- Use vanilla JavaScript with JSDoc for type annotations — do not use TypeScript without an approved exception
- Use `const` by default, `let` only when reassignment is needed, never `var`
- Use `async`/`await` — no callbacks or raw `.then()` chains
- Lint with ESLint and format with Prettier
- Pages must work without JavaScript enabled (progressive enhancement)

## Architecture

Keep controllers thin: validate input, call a service, render a view.

```
Route handler → validates input (joi) → calls service → h.view('pages/...', context)
```

## Validation

- Use `joi` (standalone package) for request and payload validation
- Do not use the deprecated `@hapi/joi`
- Return errors inline next to the field and in an error summary at the top of the page

## CSRF protection

- All state-changing routes must have CSRF protection via `@hapi/crumb`
- For API endpoints legitimately exempt (e.g. webhooks with HMAC auth), explicitly disable it:
  ```javascript
  options: { plugins: { crumb: false } }  // Exempt — uses HMAC signature verification
  ```

## Content Security Policy

- Use `@hapi/blankie` for CSP headers
- Do not add `unsafe-inline` or `unsafe-eval` to script sources
- Do not allow third-party script sources unless explicitly approved
- Set `frame-ancestors` to `'none'`
- No inline scripts or `on*` event handlers in templates

## Security headers

Set these headers on all responses:

| Header | Value |
|--------|-------|
| `X-Content-Type-Options` | `nosniff` |
| `X-Frame-Options` | `DENY` |
| `Referrer-Policy` | `no-referrer` |
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains` |
| `Cache-Control` | `no-store` (for pages with user data) |

## Cookie settings

All cookies must use:

- `HttpOnly: true`
- `Secure: true`
- `SameSite: Lax`
- Minimal scope and TTL — store only session state

## Logging

- Use Winston for structured JSON logging
- Never log PII (names, addresses, emails, NI numbers, bank details, API keys)
- Include correlation IDs for request tracing
- Development: `debug` | Production: `error` only

## Testing

- Jest for unit and integration tests
- Supertest for HTTP endpoint testing via `createServer()`
- 90% coverage minimum — do not decrease from the SonarCloud baseline
- Mock external dependencies
- Every route must include tests for at minimum: happy path, validation failure, CSRF protection, and security headers

## Allowed dependencies

| Package | Purpose |
|---------|---------|
| `@hapi/hapi` | HTTP server |
| `@hapi/boom` | Error responses |
| `@hapi/crumb` | CSRF protection |
| `@hapi/blankie` | CSP headers |
| `@hapi/inert` | Static file serving |
| `@hapi/vision` | Template rendering |
| `@hapi/yar` | Session management |
| `joi` | Schema validation |
| `nunjucks` | Templating |
| `winston` | Logging |
| `mongodb` | Native MongoDB driver (do not use Mongoose) |

**Discouraged:** `express`, `@hapi/joi` (deprecated), `mongoose`, `moment`, `lodash`, `request`, `jquery`

## Branching

- All work on branches, never directly on main (trunk-based development with short-lived feature branches)
- Branch naming: `feature/`, `fix/`, `docs/`, `refactor/`
- Conventional commits: `feat:`, `fix:`, `docs:`, `test:`, `chore:`

## Accessibility

- WCAG 2.2 Level AA — mandatory for all pages
- Semantic HTML, keyboard navigation, visible focus indicators
- GOV.UK Design System components and patterns
- Error summaries at the top of the page, inline errors next to fields

## How Copilot should respond

- Follow the conventions already established in the codebase
- Prefer modifying existing files over creating new ones
- Provide complete, minimal diffs touching only necessary files
- Keep changes minimal and focused on the request
- Always include or update tests for changed behaviour — co-locate tests with the existing test layout
- For any form or reusable UI pattern, propose or extend a Nunjucks macro using GOV.UK components
- Keep solutions DRY: before adding new utilities, search for similar code in `src/utils/` or existing routes
- Justify any security-sensitive deviation (e.g. disabling CSRF or loosening CSP) in code comments and default to the most restrictive safe option
- If a request conflicts with these instructions, flag the conflict

## Example prompts Copilot should act on

- "Add a GET and POST route for a GOV.UK form using Nunjucks macros, CSRF via crumb, and Joi validation. Render errors per GDS."
- "Create a Nunjucks macro for a GOV.UK text input with label, hint, and error message, then reuse it in a page."
- "Add Jest + Supertest tests for route validation errors and security headers."
````

---

## Adapting this example

When copying this for your own service:

1. Replace the project overview with your service's details
2. Update the project paths to match your directory structure
3. Edit the allowed dependencies table for your specific needs
4. Add or remove sections based on your tech stack — remove Nunjucks sections if you are building an API-only service, for example
5. If your project uses C#, see the [C# backend instructions]({{ "/tool-setup/github-copilot/instructions/csharp-backend" | relative_url }}) instead

[Back to instructions index]({{ "/tool-setup/github-copilot/instructions" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

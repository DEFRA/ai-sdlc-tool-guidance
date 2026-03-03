# Node.js Backend Instructions — Example

This is an example scoped instruction file for Node.js backend code. It activates when Copilot is working on JavaScript files. Copy it into `.github/instructions/node-backend.instructions.md` in your repository.

## Example file contents

The content below goes into your `.github/instructions/node-backend.instructions.md` file:

---

````markdown
---
applyTo: "**/*.js,**/*.mjs"
---

# Node.js Backend

## Language rules

- Use vanilla JavaScript — do not use TypeScript without an approved exception
- Use JSDoc for type annotations
- Use ES modules (`import`/`export`) by default
- Use CommonJS (`require`) only where needed (e.g. Jest config files)
- Use `const` by default, `let` only when reassignment is required, never `var`
- Use `async/await` — do not use callbacks or raw `.then()` chains
- Use `===` and `!==` for all equality checks
- Lint with ESLint and format with Prettier
- Use containerisation with Doocker

## Hapi framework

- Use Hapi for all HTTP servers — do not use Express, Fastify, or Koa
- Register plugins for cross-cutting concerns (auth, CSRF, security headers)
- Use `@hapi/inert` for serving static files
- Use `@hapi/vision` for template rendering (Nunjucks)
- Use `@hapi/boom` for HTTP error responses
- Use `joi` (standalone package) for request validation — do not use the deprecated `@hapi/joi`
- Use `@hapi/crumb` for CSRF protection — CSRF is on by default for all routes
- Use `@hapi/blankie` for Content Security Policy headers

### Architecture

Keep controllers thin: validate input, call a service, render a view. Business logic belongs in service modules, not route handlers. Centralise shared logic in `src/utils/` or dedicated services — do not duplicate validation or formatting utilities.

```
Route handler → validates input (joi) → calls service → renders view or returns response
```

✅ Route handler with view rendering:
```javascript
import Boom from '@hapi/boom'

const getApplication = {
  method: 'GET',
  path: '/applications/{id}',
  handler: async (request, h) => {
    const { id } = request.params
    const application = await applicationService.getById(id)

    if (!application) {
      throw Boom.notFound('Application not found')
    }

    return h.view('pages/application-detail', {
      pageTitle: 'Application details',
      application
    })
  }
}
```

✅ POST handler with validation and error summary:
```javascript
import Joi from 'joi'
import Boom from '@hapi/boom'

const postApplication = {
  method: 'POST',
  path: '/applications',
  options: {
    validate: {
      payload: Joi.object({
        name: Joi.string().required(),
        reference: Joi.string().pattern(/^[A-Z]{2}\d{6}$/).required()
      }),
      failAction: async (request, h, error) => {
        return h.view('pages/application-form', {
          pageTitle: 'Error: Submit application',
          errors: error.details
        }).takeover().code(400)
      }
    }
  },
  handler: async (request, h) => {
    await applicationService.create(request.payload)
    return h.redirect('/applications/confirmation')
  }
}
```

❌ Do not use Express patterns:
```javascript
// Wrong — do not use Express
app.get('/applications/:id', (req, res) => {
  res.json(application)
})
```

### CSRF protection

All state-changing routes must have CSRF protection via `@hapi/crumb`. For API endpoints that are legitimately exempt (e.g. webhooks with their own auth), explicitly disable it and document why:

```javascript
const webhookRoute = {
  method: 'POST',
  path: '/webhooks/payment',
  options: {
    plugins: { crumb: false }  // Exempt — uses HMAC signature verification
  },
  handler: async (request, h) => { /* ... */ }
}
```

### Content Security Policy

Configure `@hapi/blankie` with strict CSP rules:

- Do not add `unsafe-inline` or `unsafe-eval` to script sources
- Do not allow third-party script sources unless explicitly approved
- Set `frame-ancestors` to `'none'`
- No inline scripts or `on*` event handlers in templates

### Security headers

Set these headers on all responses:

| Header | Value |
|--------|-------|
| `X-Content-Type-Options` | `nosniff` |
| `X-Frame-Options` | `DENY` |
| `Referrer-Policy` | `no-referrer` |
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains` |
| `Cache-Control` | `no-store` (for pages with user data) |

### Cookie settings

All cookies must be set with:

- `HttpOnly: true` — not accessible to client-side JavaScript
- `Secure: true` — transmitted only over HTTPS
- `SameSite: Lax` — prevents CSRF from cross-origin requests
- Minimal scope and TTL — do not store more than session state requires

## Nunjucks views

- Use Nunjucks (`.njk`) for all server-side templates
- Base layout goes in `views/layouts/` (e.g. `main.njk`)
- Reusable fragments go in `views/partials/`
- GOV.UK component macros go in `views/macros/`
- Page templates go in `views/pages/`
- Render views using `h.view('pages/page-name', { context })`
- Display validation errors inline next to the field and in an error summary at the top of the page using the GOV.UK error pattern

## Error handling

- Catch errors at the route handler or service boundary
- Use `@hapi/boom` for all HTTP error responses
- Return useful error messages without leaking internals (no stack traces, no SQL)
- Log the full error server-side for debugging
- Display user-friendly error pages using GOV.UK error patterns — keep error view templates in `views/errors/`

## Health endpoint

- Expose a health endpoint at `/health`
- Return `200 OK` when the service is healthy
- Do not add health checks that perform heavy work (database writes, external API calls)
- Include checks for critical downstream dependencies only if lightweight

## Logging

- Use Winston for structured JSON logging
- Log levels: `error`, `warn`, `info`, `debug`
- Never log PII: no names, addresses, emails, phone numbers, NI numbers, bank details, API keys, or tokens
- Include a correlation ID on every log entry for request tracing
- Set appropriate log levels per environment:
  - Development: `debug`
  - Staging: `warn` and above
  - Production: `error` and `critical` only

## Database access

- Use parameterised queries — never concatenate user input into query strings
- Set connection timeouts and pool limits
- Index frequently queried columns
- Avoid `eval`, dynamic `Function()`, or executing user-supplied data
- Validate and normalise file paths — reject path traversal attempts

### IF using MongoDB (NoSQL)

- Use the native MongoDB driver — do not use Mongoose or other ODMs
- Access the database via `request.db` or `server.db` (registered as a Hapi plugin)
- Use factory functions for document creation with JSDoc type definitions
- Store `_id` and foreign key fields as `ObjectId`, not strings
- Enforce schema validation at the database level using `$jsonSchema`
- Index all foreign key fields and compound unique constraints

### If using SQL databases (PostgreSQL, etc.)

- Use an ORM or query builder (Knex, Sequelize, or Objection.js)
- Use parameterised queries — never concatenate user input into SQL
- Run migrations for schema changes — do not modify the database schema in any environment manually, always use migrations

## Environment and configuration

- Follow [12-factor app](https://12factor.net/) principles: one codebase, declared dependencies, config in environment, stateless processes, logs as event streams
- Load all configuration from environment variables
- Never hard-code secrets, connection strings, or API keys
- Use a configuration module that validates required variables at startup (`src/config/index.js`)
- Read from `process.env` only inside the config module — all other modules import config
- Fail fast if a required environment variable is missing

## Asset bundling

- Use Webpack 5 for bundling frontend assets (CSS, images)
- Source assets live in `src/public/` or equivalent
- Built assets are generated into a static output directory
- Do not commit built assets to version control — build them in CI

## Dependencies

- Use NPM for package management
- Keep `package-lock.json` in version control
- Use only Active LTS versions of Node.js — do not fall behind Maintenance LTS
- Keep Hapi on its current major version
- Run `npm audit` and resolve vulnerabilities before merging
- Use `joi` (standalone) for validation — do not use the deprecated `@hapi/joi`
- New dependencies must be widely used, actively maintained, and compatible with the current Node.js LTS version

## Testing

- Use Jest for unit and integration tests
- Use Supertest to test Hapi routes via `createServer()`
- Every route must include tests for at minimum: happy path, validation failure, CSRF protection, and security headers
- Prefer small pure functions for testability
- Mock external dependencies (APIs, databases, file system)

## References

- [Defra Node.js standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/node_standards.md)
- [Defra JavaScript standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/javascript_standards.md)
- [Defra logging standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/logging_standards.md)
- [Defra security standards](https://github.com/DEFRA/software-development-standards/blob/main/docs/standards/security_standards.md)
- [Hapi API reference](https://hapi.dev/api/)
- [Hapi Inert (static files)](https://hapi.dev/module/inert/)
- [Hapi Vision (templates)](https://hapi.dev/module/vision/)
- [Hapi Crumb (CSRF)](https://hapi.dev/module/crumb/)
- [Joi validation](https://joi.dev/)
- [Defra FFC demo web template](https://github.com/DEFRA/ffc-demo-web)
````

---

[Back to instructions index]({{ "/tool-setup/github-copilot/instructions" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

# Scaffold Repository Config Prompt — Example

This is an example `.prompt.md` file for bootstrapping the full GitHub Copilot configuration in a Defra repository. Run it once when starting a new project or adding Copilot support to an existing one.

## Example file contents

The content below goes into your `.github/prompts/scaffold-repo.prompt.md` file:

---

````markdown
---
description: Generate the full .github/ Copilot configuration for a Defra project
---

# Scaffold Copilot Config

Generate the complete `.github/` directory structure for this repository, including root instructions, scoped instructions, agents, and prompts. Tailor every file to the project details below.

## Project details

Provide these values (edit them before running this prompt):

- **Service name**: [e.g. Waste exemptions service]
- **Service description**: [e.g. Allows waste operators to register exemptions from environmental permits]
- **Tech stack**: [Node.js + Hapi | .NET + ASP.NET Core Minimal API | both]
- **Frontend**: [Nunjucks + GOV.UK Frontend | Razor Pages | API only (no frontend)]
- **Database**: [PostgreSQL | MongoDB | DynamoDB | none]
- **Hosting**: [AWS ECS | Azure AKS | Azure App Service | other]
- **Auth method**: [Azure AD | Magic link | Basic session | none]
- **Message broker**: [Azure Service Bus | AWS SQS | RabbitMQ | none]

## Files to generate

Create every file listed below. Skip sections that do not apply based on the tech stack.

### 1. Root instructions — `.github/copilot-instructions.md`

Include:
- Project overview with service name, description, and tech stack from above
- Project paths — match the actual directory layout of this repository
- Naming conventions (kebab-case directories, camelCase JS files, PascalCase C# files)
- Branching and version control (trunk-based, conventional commits, squash-and-merge)
- Quality gates (ESLint + Prettier for JS, dotnet format for C#, SonarCloud quality gate, 90% coverage)
- Allowed dependencies table — list the packages this project actually uses
- Discouraged dependencies — Express, lodash, moment, jquery, @hapi/joi
- Security rules — OWASP, no PII in logs, joi validation, parameterised queries
- How Copilot should respond — follow existing patterns, minimal diffs, include tests

### 2. Scoped instructions — `.github/instructions/`

**For Node.js projects**, create `node-backend.instructions.md`:
- `applyTo: "**/*.js,**/*.mjs"`
- Hapi framework conventions, @hapi/boom, joi, @hapi/crumb, @hapi/blankie
- Route handler → service → view pattern
- CSRF, CSP, security headers, cookie settings
- Winston logging, health endpoint, config module
- Jest + Supertest testing

**For .NET projects**, create `csharp-backend.instructions.md`:
- `applyTo: "**/*.cs,**/*.csproj"`
- Minimal API conventions, Serilog, FluentValidation
- xUnit v3 + FluentAssertions + NSubstitute testing
- Health endpoint, dependency injection, nullable reference types

**For frontend projects**, create `frontend.instructions.md`:
- `applyTo: "**/*.njk,**/*.html,**/*.css"`
- GOV.UK Design System, macro-first, no inline styles
- WCAG 2.2 AA, semantic HTML, error summary linking
- Nunjucks directory structure, progressive enhancement

### 3. Agents — `.github/agents/`

Create `defra-app-developer.agent.md`:
- Persona: senior Defra developer
- Tech stack section matching the project details above
- Full workflow with pre-commit checklist including SonarCloud quality gate
- Coding standards, security, logging, accessibility, documentation, containers
- Reference the tester agent for testing details

Create `code-reviewer.agent.md`:
- 9-category review checklist (PR hygiene, correctness, tests, security, performance, maintainability, architecture, documentation, accessibility)
- Severity levels (blocking, recommended, nit)
- SonarCloud quality gate and security hotspot checks

Create `tester.agent.md`:
- BDD testing approach with testing pyramid
- Test naming conventions with examples
- Minimum route test scenarios (happy path, validation, CSRF, auth, 404)
- Security testing checklist
- Coverage targets table (90% global, 95% business logic, 100% security)

### 4. Prompts — `.github/prompts/`

Create `write-adr.prompt.md`:
- Standard ADR template (context, decision, consequences, alternatives)
- Plain English, active voice, reference Defra standards

Create `write-tests.prompt.md`:
- Generate test suites following the project's test framework
- Coverage targets, mocking strategy, BDD naming

Create `security-review.prompt.md`:
- OWASP-based security review
- Defra-specific checks (PII, CSRF, CSP, secrets)

## Rules

- Use British English throughout (organisation, colour, licence, behaviour)
- Follow GOV.UK style guide — plain English, sentences under 25 words, active voice
- Do not include placeholder text like "[TODO]" — use the project details provided above
- Every instruction must be actionable and imperative ("Use Hapi" not "Hapi should be used")
- Include one example and one counterexample for key rules
- Reference Defra software development standards where applicable
- Keep each file under 200 lines
- Do not duplicate rules — define each rule in one file and cross-reference from others
````

---

[Back to prompts index]({{ "/tool-setup/github-copilot/prompts" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

# Instructions — Examples for GitHub Copilot

Instructions tell GitHub Copilot how your project works. They provide context about your coding standards, architecture, and conventions so Copilot generates code that fits your project.

## How instructions work

There are two types:

1. **Root instructions** (`.github/copilot-instructions.md`) — always active for every Copilot interaction in the repository
2. **Scoped instructions** (`.github/instructions/*.instructions.md`) — activate only when Copilot is working with files that match a glob pattern defined in the file's frontmatter

### Scoping with glob patterns

Scoped instruction files use an `applyTo` frontmatter field to target specific files:

```yaml
---
applyTo: "src/**/*.js"
---
```

This means the instruction only activates when Copilot is working on JavaScript files under `src/`. Use this to give stack-specific context without overloading every interaction.

## How to use these examples

1. Copy the instruction files into your repository's `.github/` and `.github/instructions/` directories
2. Edit the project overview in `copilot-instructions.md` to describe your service
3. Remove or modify instruction files that do not match your tech stack
4. Add scoped instructions for any project-specific conventions not covered here

## Available examples

| File | Scope | Purpose |
|------|-------|---------|
| [copilot-instructions.md]({{ "/tool-setup/github-copilot/instructions/copilot-instructions" | relative_url }}) | All files | Project overview, branching, commits, quality gates |
| [Node.js backend]({{ "/tool-setup/github-copilot/instructions/node-backend" | relative_url }}) | `*.js`, `*.mjs` | Hapi, vanilla JS, error handling, logging |
| [Frontend]({{ "/tool-setup/github-copilot/instructions/frontend" | relative_url }}) | `*.njk`, `*.html`, `*.css` | WCAG 2.2 AA, GDS Design System, Nunjucks, no JS frameworks |
| [C# backend]({{ "/tool-setup/github-copilot/instructions/csharp-backend" | relative_url }}) | `*.cs`, `*.csproj` | ASP.NET Core Minimal APIs, Serilog, FluentValidation, xUnit |
| [Real-world example]({{ "/tool-setup/github-copilot/instructions/real-world-example" | relative_url }}) | — | Complete instructions file for a Node.js/Hapi/Nunjucks GOV.UK service |

## Writing your own instructions

Follow this structure:

```markdown
---
applyTo: "glob/pattern/**/*.ext"
---

# Topic Name

## Rules
- Concise, imperative rules
- One rule per line
- Include one example and one counterexample per rule where helpful

## References
- Links to canonical standards
```

**Tips:**
- Keep each file under 100 lines — Copilot processes shorter instructions more reliably
- One file per concern (backend, frontend, testing, documentation)
- Use imperative phrasing — "Use Hapi" not "Hapi should be used"
- Reference the Defra standards URLs so Copilot can cite them

[Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

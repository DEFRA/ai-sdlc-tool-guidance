# GitHub Copilot — Setup Guide

This guide explains how to configure GitHub Copilot for Defra projects using agents, instructions, and reusable prompts. The examples provided encode [Defra software development standards](https://github.com/DEFRA/software-development-standards) so Copilot produces compliant code from the start.

## Quick start — minimum viable setup

Copy these three files into your repo and you are up and running:

| Step | File to copy | Save to | What to edit |
|------|-------------|---------|--------------|
| 1 | [Root instructions]({{ "/tool-setup/github-copilot/instructions/copilot-instructions" | relative_url }}) | `.github/copilot-instructions.md` | Replace the project overview with your service name, tech stack, and paths |
| 2 | [Defra App Developer agent]({{ "/tool-setup/github-copilot/agents/defra-app-developer" | relative_url }}) | `.github/agents/defra-app-developer.agent.md` | Update the tech stack section if you use .NET instead of Node.js |
| 3 | [Write ADR prompt]({{ "/tool-setup/github-copilot/prompts/write-adr" | relative_url }}) | `.github/prompts/write-adr.prompt.md` | Ready to use — no edits needed |

That gives you Defra-compliant code generation, a pre-commit checklist, and architecture decision records. Add more files from the sections below as your team's needs grow.

## How GitHub Copilot uses configuration files

GitHub Copilot reads configuration files from your repository's `.github/` directory. These files give Copilot project-specific context that improves the quality and relevance of its suggestions.

There are three types of configuration:

| Type | Location | Purpose |
|------|----------|---------|
| **Instructions** | `.github/copilot-instructions.md` and `.github/instructions/*.instructions.md` | Project-wide rules, standards, and conventions that always apply |
| **Agents** | `.github/agents/*.agent.md` | Specialised personas with specific expertise and workflows |
| **Prompts** | `.github/prompts/*.prompt.md` | Reusable prompt templates for common tasks |

## Recommended directory structure

```
your-repo/
└── .github/
    ├── copilot-instructions.md              # Root instructions (always active)
    ├── agents/
    │   ├── defra-app-developer.agent.md     # Defra-compliant development
    │   ├── code-reviewer.agent.md           # Systematic code review
    │   └── tester.agent.md                  # BDD-focused testing
    ├── instructions/
    │   ├── node-backend.instructions.md     # Node.js/Hapi backend rules
    │   ├── csharp-backend.instructions.md   # C#/ASP.NET Core Minimal API rules
    │   ├── frontend.instructions.md         # Accessibility, GDS patterns
    │   └── docs.instructions.md             # Documentation standards
    └── prompts/
        ├── write-adr.prompt.md              # Generate architecture decisions
        ├── write-tests.prompt.md            # Generate test suites
        └── security-review.prompt.md        # Review code for vulnerabilities
```

## Instructions

Instructions tell Copilot how your project works. The root file (`.github/copilot-instructions.md`) is always active — Copilot reads it for every interaction. Additional instruction files in `.github/instructions/` are scoped by glob pattern and activate only for matching files.

**Key principles for writing instructions:**
- One file per concern (backend, frontend, testing, docs)
- Use imperative phrasing — "Use Hapi for HTTP servers" not "Hapi should be used"
- Include one short example and one counterexample per rule
- Link to canonical sources rather than duplicating content

### Example instruction files

- [Root copilot-instructions.md]({{ "/tool-setup/github-copilot/instructions/copilot-instructions" | relative_url }}) — branching, commits, quality gates, project overview
- [Node.js backend instructions]({{ "/tool-setup/github-copilot/instructions/node-backend" | relative_url }}) — Hapi, vanilla JavaScript, logging, error handling
- [Frontend instructions]({{ "/tool-setup/github-copilot/instructions/frontend" | relative_url }}) — WCAG 2.2 AA, GDS Design System, Nunjucks, no JS frameworks
- [C# backend instructions]({{ "/tool-setup/github-copilot/instructions/csharp-backend" | relative_url }}) — ASP.NET Core Minimal APIs, Serilog, FluentValidation, xUnit
- [Real-world example]({{ "/tool-setup/github-copilot/instructions/real-world-example" | relative_url }}) — complete instructions file for a Node.js/Hapi/Nunjucks GOV.UK service

## Agents

Agents are specialised AI personas you invoke in Copilot Chat. Each agent has a defined role, expertise area, and workflow. Use agents when you want Copilot to adopt a specific mindset — for example, reviewing code with security in mind, or writing tests using BDD patterns.

**Key principles for writing agents:**
- Give each agent a clear role and boundaries
- Reference instruction files rather than restating rules
- Define the agent's workflow as a numbered sequence
- State what the agent must not do

### Example agent files

- [Defra App Developer]({{ "/tool-setup/github-copilot/agents/defra-app-developer" | relative_url }}) — builds Defra-compliant applications following all software development standards
- [Code Reviewer]({{ "/tool-setup/github-copilot/agents/code-reviewer" | relative_url }}) — systematic review using Defra's quality criteria
- [Tester]({{ "/tool-setup/github-copilot/agents/tester" | relative_url }}) — BDD-focused unit/integration testing and Playwright journey tests with coverage enforcement

## Prompts

Prompts are reusable templates for common tasks. Unlike instructions (which are always on) or agents (which set a persona), prompts are one-shot — you run them when you need a specific output, like generating an ADR or reviewing for security vulnerabilities.

**Key principles for writing prompts:**
- Start with a clear output description
- Include the expected file format and save location
- Reference relevant instruction files for standards
- Add variables (placeholders) for context the user provides

### Example prompt files

- [Write ADR]({{ "/tool-setup/github-copilot/prompts/write-adr" | relative_url }}) — generate architecture decision records
- [Write Tests]({{ "/tool-setup/github-copilot/prompts/write-tests" | relative_url }}) — generate test suites for existing code
- [Security Review]({{ "/tool-setup/github-copilot/prompts/security-review" | relative_url }}) — review code against OWASP and Defra security standards
- [Scaffold Repo]({{ "/tool-setup/github-copilot/prompts/scaffold-repo" | relative_url }}) — generate the full `.github/` config for a new Defra project

## Using these examples with other AI tools

The rules and standards in these examples work with any AI coding tool — only the file format changes. See [Using these examples with other AI tools]({{ "/tool-setup/cross-tool-config" | relative_url }}) for how to adapt them for Claude Code, Cursor, and Windsurf.

## Getting started

1. Copy the `.github/` directory structure into your repository
2. Start with the root `copilot-instructions.md` — edit the project overview section for your service
3. Add the instruction files that match your tech stack (Node.js backend, frontend, or both)
4. Add agents that match your team's workflow
5. Add prompts for tasks your team does repeatedly
6. Test by opening Copilot Chat and asking it about your project — it should reference the standards

## Tips for effective configuration

- **Keep files short.** Copilot works best with concise, specific instructions. Aim for under 200 lines per file.
- **Use the SSOT pattern.** Define each rule in one place and reference it elsewhere. This prevents conflicting instructions.
- **Iterate.** Start with the basics and add detail as you discover what Copilot gets wrong.
- **Review output.** AI-generated code always needs human review. These configurations improve first-draft quality but do not replace code review.

## References

- [GitHub Copilot customisation docs](https://docs.github.com/en/copilot/customizing-copilot)
- [Capgemini GitHub Copilot template](https://github.com/Capgemini/template-github-copilot) — the community template that inspired this structure
- [Defra software development standards](https://github.com/DEFRA/software-development-standards) — the guardrails encoded in the example files

# Tool Setup Guidance

This section provides practical setup guidance for configuring AI coding tools in Defra projects. Each guide includes example files you can copy directly into your repositories.

## Why this matters

AI tools work best when given clear, project-specific context. A well-configured AI coding assistant will:

- Follow your team's coding standards and conventions automatically
- Produce code that passes your quality gates first time
- Understand your architecture and make consistent decisions
- Save time on repetitive tasks like writing tests, ADRs, and documentation

These setup guides implement the [four pillars](https://defra.github.io/defra-ai-sdlc/pages/getting-started/the-four-pillars){:target="_blank"} (opens in new tab) from the [Defra AI SDLC playbook](https://defra.github.io/defra-ai-sdlc/){:target="_blank"} (opens in new tab) — particularly **Rules and Instructions** and **Prompts** — with ready-to-use configuration files for each tool.

## Available guides

### GitHub Copilot

Set up GitHub Copilot with agents, instructions, and reusable prompts tailored for Defra projects.

[GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

Includes ready-to-use examples for:
- **Agents** — specialised AI personas (Defra App Developer, Code Reviewer, Tester)
- **Instructions** — project-specific rules and standards (Node.js backend, frontend, root config)
- **Prompts** — reusable prompt templates (ADRs, tests, security reviews)

### Cursor

Set up Cursor with rule files tailored for Defra projects.

[Cursor setup guide]({{ "/tool-setup/cursor-setup" | relative_url }})

Includes ready-to-use examples for:
- **Node.js backend rules** — Hapi, vanilla JS, MongoDB, REST API patterns, Jest testing
- **Node.js frontend rules** — GOV.UK Design System, Nunjucks, Playwright testing, accessibility
- **Python backend rules** — FastAPI, pytest, MongoDB mocking patterns

### Claude Code

*Coming soon* — setup guidance for Claude Code with custom agents and instructions.

### Using these examples with other AI tools

The rules and standards encoded in the examples above work with any AI coding tool. See [Using these examples with other AI tools]({{ "/tool-setup/cross-tool-config" | relative_url }}) for how to adapt the configuration for Claude Code, Cursor, and Windsurf.

## How to use the examples

1. Browse the guide for your tool to understand the configuration structure
2. Navigate to the example files that match your project's needs
3. Copy the raw markdown content into the matching directory in your repository
4. Edit the examples to fit your specific project context

All examples follow [Defra software development standards](https://github.com/DEFRA/software-development-standards) and encode the key guardrails so your AI assistant produces compliant code from the start.

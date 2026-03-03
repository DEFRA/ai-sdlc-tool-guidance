# Agents — Examples for GitHub Copilot

Agents are specialised AI personas you can invoke in GitHub Copilot Chat. Each agent has a defined role, expertise, and workflow that shapes how Copilot responds.

## How agents work

When you select an agent in Copilot Chat (using `@agent-name`), Copilot adopts that persona for the conversation. The agent's instructions override the default behaviour, giving you focused, role-specific assistance.

Agent files live in `.github/agents/` and use the `.agent.md` extension.

## How to use these examples

1. Copy the `.agent.md` file into your repository's `.github/agents/` directory
2. Edit any project-specific details (service name, tech stack, team conventions)
3. Open Copilot Chat and select the agent from the agent picker

> **Keep agents current.** Defra standards evolve. Revisit agent files quarterly or when the [Defra software development standards](https://github.com/DEFRA/software-development-standards) repository is updated.

## Available examples

| Agent | Purpose | Best for |
|-------|---------|----------|
| [Defra App Developer]({{ "/tool-setup/github-copilot/agents/defra-app-developer" | relative_url }}) | Builds Defra-compliant applications | Writing new features, implementing user stories |
| [Code Reviewer]({{ "/tool-setup/github-copilot/agents/code-reviewer" | relative_url }}) | Systematic code review | Reviewing PRs, checking standards compliance |
| [Tester]({{ "/tool-setup/github-copilot/agents/tester" | relative_url }}) | BDD-focused testing and Playwright journey tests | Writing unit tests, acceptance tests, journey tests, coverage gaps |

## Writing your own agents

Follow this structure:

```markdown
---
description: One-line summary of what this agent does
tools: [list, of, tools, it, can, use]
---

# Agent Name

## Role
What this agent is and its expertise.

## Workflow
1. Step one
2. Step two
3. Step three

## Rules
- What the agent must always do
- What the agent must never do

## References
- Links to standards or instruction files this agent follows
```

**Tips:**
- Keep the description under 100 characters — it appears in the agent picker
- List only the tools the agent needs (e.g., `editFiles`, `runTerminal`, `codebase`)
- Reference instruction files rather than restating rules
- Define clear boundaries — what the agent does and does not do

[Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

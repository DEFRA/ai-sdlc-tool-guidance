# Cursor — Setup Guide

This guide explains how to configure Cursor for Defra projects using rule files. The examples provided encode [Defra software development standards](https://github.com/DEFRA/software-development-standards) so Cursor produces compliant code from the start.

For a general overview of how AI tool configuration maps across tools, see [Using these examples with other AI tools]({{ "/tool-setup/cross-tool-config" | relative_url }}).

## How Cursor uses rule files

Cursor reads project-specific rules from `.cursor/rules/` in your repository. Each rule file uses the `.mdc` extension and controls when it activates using frontmatter.

There are four rule types:

| Rule type | Frontmatter | When it activates |
|-----------|-------------|-------------------|
| **Always** | `alwaysApply: true` | Every Cursor interaction (root instructions) |
| **Auto Attached** | `globs: "pattern"` | When files matching the pattern are referenced |
| **Agent Requested** | `description: "..."` only | Cursor reads the description and decides whether to include |
| **Manual** | No description, no globs | Only when explicitly referenced with `@rulename` |

Read more in the [Cursor documentation (opens in new tab)](https://docs.cursor.com/context/rules){:target="_blank"}.

## Recommended directory structure

```
your-repo/
└── .cursor/
    └── rules/
        ├── project.mdc                # Project overview (always active)
        ├── javascript-api.mdc         # Node.js/Hapi backend rules
        ├── gov-uk-standards.mdc       # GOV.UK frontend and Nunjucks
        ├── mongodb-patterns.mdc       # MongoDB data access patterns
        ├── api-testing.mdc            # Jest API testing standards
        ├── playwright-testing.mdc     # Playwright journey tests
        ├── restful-api-patterns.mdc   # RESTful route and handler patterns
        ├── api-integration.mdc        # API client integration patterns
        └── navigation.mdc            # Navigation and routing patterns
```

## Example rule files

These example files contain the same Defra standards encoded in the [GitHub Copilot examples]({{ "/tool-setup/github-copilot-setup" | relative_url }}), adapted for Cursor's rule file format.

### Node.js

- [Node.js backend rules]({{ "/tool-setup/cursor/nodejs-backend-rules" | relative_url }}) — Hapi, vanilla JS, MongoDB, REST API patterns, Jest testing
- [Node.js frontend rules]({{ "/tool-setup/cursor/nodejs-frontend-rules" | relative_url }}) — GOV.UK Design System, Nunjucks, Playwright testing, accessibility

### Python

- [Python backend rules]({{ "/tool-setup/cursor/python-backend-rules" | relative_url }}) — FastAPI, pytest, MongoDB mocking patterns

## How to use these examples

1. Create `.cursor/rules/` in your repository root
2. Browse the example files above and copy the rule content into separate `.mdc` files
3. Each code block in the example files represents one `.mdc` file — the filename is shown in bold above each block
4. Edit the project overview rule to describe your specific service
5. Remove or modify rules that do not match your tech stack

## Adapting GitHub Copilot examples for Cursor

If you are starting from a GitHub Copilot configuration, convert the frontmatter:

**Copilot format:**
```yaml
---
applyTo: "**/*.js,**/*.mjs"
---
```

**Cursor format:**
```yaml
---
description: Node.js backend rules
globs: "**/*.js,**/*.mjs"
alwaysApply: false
---
```

See [Using these examples with other AI tools]({{ "/tool-setup/cross-tool-config" | relative_url }}) for the full adaptation guide.

---

[Back to Tool Setup]({{ "/tool-setup" | relative_url }})

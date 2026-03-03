# Prompts — Examples for GitHub Copilot

Prompts are reusable templates for common tasks. Unlike instructions (always active) or agents (personas), prompts are one-shot — run them when you need a specific output.

## How prompts work

Prompt files live in `.github/prompts/` and use the `.prompt.md` extension. When you open Copilot Chat, you can select a prompt from the prompt picker to run it.

Prompts can include:
- A description of the expected output
- The file format and save location
- Variables (placeholders) that the user fills in
- References to instruction files for standards context

## How to use these examples

1. Copy the `.prompt.md` file into your repository's `.github/prompts/` directory
2. Open Copilot Chat and select the prompt from the picker
3. Fill in any variables when prompted
4. Review the generated output before saving

## Available examples

| Prompt | Purpose | Output |
|--------|---------|--------|
| [Write ADR]({{ "/tool-setup/github-copilot/prompts/write-adr" | relative_url }}) | Generate architecture decision records | Markdown ADR document |
| [Write Tests]({{ "/tool-setup/github-copilot/prompts/write-tests" | relative_url }}) | Generate test suites for existing code | Jest test file |
| [Security Review]({{ "/tool-setup/github-copilot/prompts/security-review" | relative_url }}) | Review code against OWASP and Defra security standards | Review findings report |
| [Scaffold Repo]({{ "/tool-setup/github-copilot/prompts/scaffold-repo" | relative_url }}) | Generate the full `.github/` Copilot config for a Defra project | Complete directory structure |

## Writing your own prompts

Follow this structure:

```markdown
---
description: One-line summary of what this prompt produces
---

# Prompt Title

[Clear description of what to generate]

## Context
[What the user needs to provide or select]

## Output format
[Expected structure, file type, save location]

## Standards
[Reference to instruction files or external standards]
```

**Tips:**
- Start with a clear description of the expected output
- Tell Copilot where to save the file
- Reference instruction files for standards rather than restating rules
- Keep prompts focused on one task

[Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

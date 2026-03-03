# Write ADR Prompt — Example

This is an example `.prompt.md` file for generating Architecture Decision Records (ADRs). Copy it into `.github/prompts/write-adr.prompt.md` in your repository.

## Example file contents

The content below goes into your `.github/prompts/write-adr.prompt.md` file:

---

````markdown
---
description: Generate an Architecture Decision Record (ADR) from a design discussion
---

# Write ADR

Generate an Architecture Decision Record for the design decision described below. Follow the standard ADR template.

## Output format

Save the file as `docs/ADRs/NNNN-title-in-kebab-case.md` where NNNN is the next sequence number.

Use this template:

```markdown
# NNNN. Title

**Date:** YYYY-MM-DD

**Status:** Proposed | Accepted | Deprecated | Superseded by [NNNN]

## Context

What is the issue that we are seeing that motivates this decision or change?

## Decision

What is the change that we are proposing and/or doing?

## Consequences

What becomes easier or more difficult to do because of this change?

### Positive
- Benefit one
- Benefit two

### Negative
- Trade-off one
- Trade-off two

### Risks
- Risk one and its mitigation

## Alternatives considered

### Alternative A: [Name]
- Description
- Why it was not chosen

### Alternative B: [Name]
- Description
- Why it was not chosen
```

## Rules

- Write in plain English using active voice
- Be specific about technologies, versions, and constraints
- State the decision clearly in one sentence
- List at least two alternatives that were considered
- Include both positive and negative consequences — be honest about trade-offs
- Reference Defra software development standards where the decision relates to an existing standard
- If the decision conflicts with a Defra standard, explain why and note that an exception is needed
````

---

[Back to prompts index]({{ "/tool-setup/github-copilot/prompts" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

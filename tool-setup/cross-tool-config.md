# Using these examples with other AI tools

The agents, instructions, and prompts on this site are written for GitHub Copilot's configuration format, but the **content** — the rules, standards, and patterns — works with any AI coding tool. This page shows how to adapt the examples for other tools.

## How the content maps across tools

Every AI coding tool has its own configuration format, but they all solve the same problem: giving the AI context about your project. The table below shows where each tool expects to find that context.

### GitHub Copilot

| Concept | Configuration |
|---------|--------------|
| **Root instructions** | `.github/copilot-instructions.md` |
| **Scoped instructions** | `.github/instructions/**/*.instructions.md` with `applyTo` frontmatter |
| **Agents** | `.github/agents/*.agent.md` |
| **Prompts** | `.github/prompts/*.prompt.md` |

### Claude Code

| Concept | Configuration |
|---------|--------------|
| **Root instructions** | `CLAUDE.md` in repo root |
| **Scoped instructions** | `CLAUDE.md` in subdirectories, or `.claude/rules/*.md` with `paths` frontmatter |
| **Agents** | `.claude/agents/` for custom subagents |
| **Prompts** | `.claude/commands/*.md` (custom slash commands) |

### Cursor

| Concept | Configuration |
|---------|--------------|
| **Root instructions** | `.cursor/rules/*.mdc` with `alwaysApply: true` |
| **Scoped instructions** | `.cursor/rules/*.mdc` with `globs` frontmatter |
| **Agents** | Not supported — use rules instead |
| **Prompts** | Not supported — paste into chat |

### Windsurf

| Concept | Configuration |
|---------|--------------|
| **Root instructions** | `.windsurf/rules/*.md` with Always On trigger (legacy: `.windsurfrules`) |
| **Scoped instructions** | `.windsurf/rules/*.md` with Glob trigger |
| **Agents** | Supports `AGENTS.md` |
| **Prompts** | Not supported — paste into chat |

## Adapting the examples

### Claude Code

Claude Code reads project context from `CLAUDE.md` files and `.claude/` configuration. To use the Defra examples:

1. Create a `CLAUDE.md` in your repo root with the content from [copilot-instructions.md]({{ "/tool-setup/github-copilot/instructions/copilot-instructions" | relative_url }})
2. Append the relevant backend instructions ([Node.js]({{ "/tool-setup/github-copilot/instructions/node-backend" | relative_url }}) or [C#]({{ "/tool-setup/github-copilot/instructions/csharp-backend" | relative_url }}))
3. Append the [frontend instructions]({{ "/tool-setup/github-copilot/instructions/frontend" | relative_url }}) if your service has a UI
4. Replace `applyTo` frontmatter with `paths` frontmatter in any `.claude/rules/*.md` files

For scoped rules, you have two options:

**Option A — subdirectory `CLAUDE.md` files** (simpler):

```
your-repo/
├── CLAUDE.md                    # Root instructions (always active)
├── src/
│   └── CLAUDE.md                # Backend-specific rules
└── views/
    └── CLAUDE.md                # Frontend-specific rules
```

**Option B — `.claude/rules/` with `paths` frontmatter** (more precise):

```
your-repo/
├── CLAUDE.md                    # Root instructions
└── .claude/
    └── rules/
        ├── node-backend.md      # Scoped to JS/MJS files
        └── frontend.md          # Scoped to Nunjucks/SCSS files
```

Each rule file uses `paths` frontmatter to target specific file patterns:

```yaml
---
paths:
  - "**/*.js"
  - "**/*.mjs"
---
```

**Agent content**: Claude Code supports custom subagents via `.claude/agents/`. Create agent definitions here to replicate the behaviour of the [Defra App Developer agent]({{ "/tool-setup/github-copilot/agents/defra-app-developer" | relative_url }}).

**Prompt content**: Claude Code supports custom slash commands via `.claude/commands/*.md`. Each file becomes a reusable command invoked as `/project:command-name`. Files can include `$ARGUMENTS` as a placeholder for dynamic input.

Example — `.claude/commands/review.md`:

```markdown
Review the code in $ARGUMENTS for:
- Security vulnerabilities (OWASP Top 10)
- Accessibility issues (WCAG 2.2 AA)
- Defra coding standards compliance
```

Invoke with: `/project:review src/controllers/auth.js`

### Cursor

Cursor uses rule files in `.cursor/rules/`. To use the Defra examples:

1. Create `.cursor/rules/` in your repository root
2. Copy the root instructions into a `.mdc` file with `alwaysApply: true`
3. Copy scoped instructions into separate files with `globs` frontmatter
4. Update the frontmatter from `applyTo` to `globs`:

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

Cursor supports four rule types controlled by frontmatter:

| Rule type | Frontmatter | Behaviour |
|-----------|-------------|-----------|
| **Always** | `alwaysApply: true` | Always included in context (root instructions) |
| **Auto Attached** | `globs: "pattern"` | Included when matching files are referenced |
| **Agent Requested** | `description: "..."` only | AI reads description and decides whether to include |
| **Manual** | No description, no globs | Only included when explicitly referenced with `@rulename` |

**Agent and prompt content**: Cursor does not have separate agent or prompt files. Merge agent rules into your rule files and paste prompt templates into the chat when needed.

### Windsurf

Windsurf uses a rules directory at `.windsurf/rules/`. To use the Defra examples:

1. Create `.windsurf/rules/` in your repository root
2. Create an always-on rule file with root instructions
3. Create scoped rule files with Glob triggers for backend and frontend rules
4. Set the appropriate trigger type in each file's frontmatter

**Windsurf rule frontmatter:**

```yaml
---
trigger: glob
globs: ["**/*.js", "**/*.mjs"]
description: Node.js backend rules
---
```

Windsurf supports four trigger types:

| Trigger | Behaviour |
|---------|-----------|
| `always_on` | Always included in context (root instructions) |
| `glob` | Included when matching files are referenced (scoped instructions) |
| `model_decision` | AI reads description and decides whether to include |
| `manual` | Only included when explicitly referenced by the user |

**Legacy**: `.windsurfrules` in the repo root still works as a single-file alternative. Use it if your team does not need scoped rules.

**Agent content**: Windsurf supports `AGENTS.md` for defining agent personas.

**Prompt content**: Windsurf does not have a prompt file system. Paste prompt templates into the chat when needed.

## What stays the same across tools

Regardless of the tool, the underlying rules are identical:

- Defra software development standards
- GOV.UK Design System and content standards
- WCAG 2.2 Level AA accessibility
- OWASP security practices
- SonarCloud quality gates (SonarWay profile)
- Coding conventions (ESLint + Prettier, vanilla JS, Hapi, joi)
- Test coverage targets (90% minimum)
- No PII in logs, no secrets in code

The format changes. The standards do not.

## Multi-tool setup

If your team uses multiple AI tools, maintain the content in one place and generate tool-specific config files from it. One approach:

1. Write your canonical rules in `.github/copilot-instructions.md` (this is version-controlled and reviewed in PRs)
2. Use the [scaffold prompt]({{ "/tool-setup/github-copilot/prompts/scaffold-repo" | relative_url }}) to generate the initial config
3. Copy the same content into `CLAUDE.md`, `.cursor/rules/`, or `.windsurf/rules/` as needed
4. When rules change, update the canonical source and regenerate

---

[Back to Tool Setup]({{ "/tool-setup" | relative_url }}) · [Back to GitHub Copilot setup guide]({{ "/tool-setup/github-copilot-setup" | relative_url }})

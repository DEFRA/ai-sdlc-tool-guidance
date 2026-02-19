# Copilot Instructions — Defra AI Tool Guidance Site

## Project Overview

This is a **Jekyll-based GitHub Pages site** providing AI tool guidance for Defra (UK Government) pilot teams. It documents approved AI tools and MCP servers with privacy, compliance, and data-handling assessments. The audience is government digital professionals evaluating AI tools for secure adoption.

## Architecture

- **Static site generator:** Jekyll with `jekyll-theme-minimal`, hosted on GitHub Pages
- **Config:** `_config.yml` — sets `baseurl: '/ai-sdlc-tool-guidance'`, version numbers, and excluded paths
- **Layout:** Single custom layout at `_layouts/default.html` with sidebar nav, dark/light theme toggle, and GOV.UK-styled branding
- **Styles:** `_sass/defra-styles.scss` overrides the theme using GOV.UK and Defra colour variables (CSS custom properties with light/dark themes). Imported via `assets/css/style.scss`
- **Content:** All guidance is pure Markdown in `tool-guidance/` (AI tools) and `tool-guidance/mcps/` (MCP servers)

## Content Structure & Naming Conventions

Every tool has exactly two files following this naming pattern:

| Type | Pattern | Example |
|------|---------|---------|
| Summary | `tool-guidance/{tool-slug}-summary.md` | `github-copilot-summary.md` |
| Detailed | `tool-guidance/{tool-slug}-detailed.md` | `github-copilot-detailed.md` |
| MCP Summary | `tool-guidance/mcps/{tool-slug}-mcp-summary.md` | `github-mcp-summary.md` |
| MCP Detailed | `tool-guidance/mcps/{tool-slug}-mcp-detailed.md` | `github-mcp-detailed.md` |

### Required sections — Tool Summary files

Summaries follow the template in `prompts/tool-summary-prompt.md`:
`Tool Overview` → `Privacy Settings` → `Terms of Use and Privacy Policy` → `Data Management` (with sub-sections: Multi-Regional Processing, Data in Transit, Data at Rest) → `Auditing` → `Access Controls` → `Compliance & Regulatory Considerations` → `References`

### Required sections — MCP Summary files

MCP summaries add a `Key Risks & Threat Vectors` section (see `prompts/mcp-tool-summary-prompt.md`).

### Required sections — Detailed files

Detailed guides follow `prompts/deep-research-tool-guidance-prompt.md` with numbered sections (1–8) and sub-sections like `4.1 Server Location`, `4.2 Data in Transit`, `4.3 Data at Rest`, `4.4 Data Retention`.

## Writing Style (Critical)

Follow the rules in `.cursor/rules/playbook-general-rules.mdc`:

- **British English** — "organisation" not "organization", "colour" not "color"
- **GOV.UK style guide** and plain English — sentences under 25 words, active voice, address readers as "you"
- **No hedging** — avoid "please", "simply", "just"
- **Start instructions with verbs** — "Configure the API" not "The API should be configured"
- **Define technical terms** on first use
- Target audience: experienced government digital professionals new to GenAI in SDLC

## Navigation & Linking

When adding a new tool, update these locations:
1. `README.md` — add bullet with Summary and Detailed links
2. `_layouts/default.html` — add `<li>` entry in the sidebar `<nav>` section
3. For MCP tools: also add to `restricted-mcp.md` using Liquid `relative_url` filter syntax: `{{ "/tool-guidance/mcps/{slug}" | relative_url }}`

All internal links in Markdown rendered pages use Liquid's `relative_url` filter (e.g. `{{ "/tool-guidance/claude-summary" | relative_url }}`). In pure Markdown files like `README.md`, use relative paths (e.g. `tool-guidance/claude-summary.md`).

## Local Development

```bash
./scripts/local-dev/setup.sh   # first-time Ruby/Bundler/gem install
./scripts/local-dev/serve.sh   # dev server at http://localhost:4000/ai-sdlc-tool-guidance
./scripts/local-dev/build.sh   # production build to _site/
```

## Key Files

- `_config.yml` — site metadata, version, build exclusions
- `_layouts/default.html` — the only layout; contains all nav links
- `_sass/defra-styles.scss` — GOV.UK/Defra design tokens and component styles
- `restricted-mcp.md` — landing page for restricted MCP server guidance
- `prompts/` — prompt templates used to generate/validate guidance content (excluded from build)
- `scripts/` — local dev and git helper scripts (excluded from build)
- `.cursor/rules/playbook-general-rules.mdc` — voice/tone rules (always apply)

## Things to Avoid

- Do not add OFFICIAL-SENSITIVE or classified data — this is a public guidance site
- Do not change `baseurl` in `_config.yml` without updating all nav links
- Do not edit `prompts/` or `scripts/` expecting them to appear on the built site — they are excluded in `_config.yml`
- Do not use American English spelling

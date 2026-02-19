# Brand Voice Plugin

Claude Cowork plugin by Tribe AI. Discovers brand materials across enterprise platforms, generates LLM-ready brand guidelines, and enforces brand voice on all content creation.

## Repo Layout

Plugin files live at repo root so Cowork can load directly from the git repo.

- `.claude-plugin/plugin.json` — plugin manifest
- `.mcp.json` — MCP server connections
- `agents/` — autonomous agent definitions
- `commands/` — slash command entry points
- `skills/` — skill definitions with `references/` subdirectories
- `settings/` — per-project settings template

## Branches

- `main` — Victor's original version (2 skills, 4 agents, 2 commands)
- `carlos-plugin-updates` — Carlos's expanded version (3 skills, 5 agents, 3 commands, reference files, settings, Microsoft 365 + native Google Drive/Slack)

## Current State (carlos-plugin-updates)

Plugin has been restructured to match the Cowork plugin schema and expanded:

- **3 commands**: `discover-brand`, `generate-guidelines`, `enforce-voice`
- **3 skills** with `references/` subdirectories for progressive disclosure
- **5 agents**: brand-discovery, document-analysis, conversation-analysis, content-generation, quality-assurance
- **6 MCP connectors**: Notion, Atlassian, Box, Figma, Gong, Microsoft 365
- **2 native integrations**: Google Drive, Slack (no MCP URL, referenced in docs only)
- **Per-project settings**: `settings/brand-voice.local.md.example`
- Plugin validated — 0 critical issues, all skill reviews addressed

## Key Differences from Main

1. **Brand discovery workflow** — new `/brand-voice:discover-brand` command with autonomous agent that searches all connected platforms, triages sources, and produces a structured report
2. **Guideline persistence** — guidelines save to `.claude/brand-voice-guidelines.md` in the user's working folder; enforce-voice loads from session context or that file
3. **Microsoft 365 connector** — SharePoint/OneDrive MCP server added
4. **Reference files** — detailed supporting docs (search strategies, source ranking, confidence scoring, before/after examples, tone model, guideline template) broken out of SKILL.md files
5. **Commands split from skills** — separate `commands/` directory with proper frontmatter

## Goals

- [ ] Test all 3 workflows end-to-end in Claude Cowork via zip upload
- [ ] Get team feedback on the brand discovery agent output quality
- [ ] Validate MCP connector behavior (especially Microsoft 365 and Notion federation)
- [ ] Decide whether to merge carlos-plugin-updates into main or keep iterating
- [ ] Explore adding a PostToolUse hook for passive enforcement (auto-validate written content against guidelines)
- [ ] Consider adding example output files (sample discovery report, sample generated guidelines)

## Building the Zip

From the repo root:
```bash
rm -f brand-voice-plugin.zip
zip -r brand-voice-plugin.zip . -x '.git/*' -x '.DS_Store' -x 'CLAUDE.md' -x 'brand-voice-plugin.zip' -x '.claude/*'
```

Upload `brand-voice-plugin.zip` via the Cowork plugin uploader, or point Cowork at the git repo directly.

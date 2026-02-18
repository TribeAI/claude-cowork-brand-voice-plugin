# Brand Voice Plugin

Claude Cowork plugin by Tribe AI. Discovers brand materials across enterprise platforms, generates LLM-ready brand guidelines, and enforces brand voice on all content creation.

## Repo Layout

- `brand-voice/` — the plugin (this is what gets zipped and uploaded to Cowork)
- `brand-voice-plugin.zip` — latest build for upload to Claude Desktop/Cowork plugin installer
- `PRDs/` — original product requirements
- `demo/` — test fixtures, sample inputs, and validation criteria

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
2. **Guideline persistence** — 5-tier loading sequence so enforce-voice finds saved guidelines across sessions (local config, local file, session context, platform search, ask user)
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
cd brand-voice && zip -r ../brand-voice-plugin.zip . -x '.git/*' -x '.DS_Store'
```

Upload `brand-voice-plugin.zip` via the Cowork plugin uploader.

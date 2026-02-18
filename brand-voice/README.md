# Brand Voice Plugin

Transforms scattered brand documents and conversation transcripts into enforceable AI guardrails. Searches across Confluence, Google Drive, Box, SharePoint, Slack, and conversation intelligence platforms like Gong and Granola to discover how your company actually communicates. Creates LLM-ready brand guidelines and continuously validates AI-generated content — from sales emails to marketing copy — ensuring every output matches your established voice, tone, and positioning. Surfaces open branding questions for team discussion when ambiguity is found.

## Features

### 1. Discover Brand (the differentiator)
Autonomously search enterprise platforms to find all brand-related materials — style guides, pitch decks, email templates, sales call transcripts, and design systems. The discovery agent searches, categorizes, ranks, and reports on everything it finds.

**Slash Command:** `/brand-voice:discover-brand`

```
/brand-voice:discover-brand
/brand-voice:discover-brand Acme Corp
```

### 2. Guideline Generation
Generate comprehensive, LLM-ready brand guidelines from discovery reports, documents, transcripts, or any combination. Produces a "We Are / We Are Not" identity table, tone-by-context matrix, terminology guide, and confidence scores.

**Slash Command:** `/brand-voice:generate-guidelines`

```
/brand-voice:generate-guidelines
/brand-voice:generate-guidelines from the discovery report and these 3 PDFs
```

### 3. Brand Voice Enforcement
Apply generated guidelines to all content creation. Voice stays constant while tone flexes by context — formality, energy, and technical depth adapt automatically for cold emails vs. enterprise proposals vs. LinkedIn posts.

**Slash Command:** `/brand-voice:enforce-voice`

```
/brand-voice:enforce-voice Draft a cold email to a VP of Sales at a mid-market SaaS company
/brand-voice:enforce-voice Write a LinkedIn post announcing our new feature
```

### Open Questions
When the plugin encounters ambiguity it can't resolve — conflicting documents, missing guidelines, stated vs. practiced brand divergence — it surfaces open questions for team discussion. Every question includes an agent recommendation, turning ambiguity into a "confirm or override" interaction rather than a dead end.

## MCP Connectors

| Connector | URL | Purpose |
|-----------|-----|---------|
| **Notion** | `https://mcp.notion.com/mcp` | Discovery backbone — federates across connected Google Drive, SharePoint, OneDrive, Slack, Jira. Also stores output guidelines. |
| **Atlassian** | `https://mcp.atlassian.com/v1/mcp` | Deep Confluence search + Jira context for Atlassian-heavy enterprises |
| **Box** | `https://mcp.box.com` | Cloud file storage — official brand docs, shared decks, and style guides often live here |
| **Microsoft 365** | `https://microsoft365.mcp.claude.com/mcp` | SharePoint, OneDrive, Outlook, Teams — enterprise document storage and email templates |
| **Figma** | `https://mcp.figma.com/mcp` | Brand design systems — color, typography, design tokens inform voice |
| **Gong** | `https://mcp.gong.io/mcp` | Enterprise conversation intelligence — sales call transcripts and analysis |
| **Granola** | `https://mcp.granola.ai/mcp` | Meeting intelligence — transcripts and notes from sales, customer, and strategy meetings |

### Native Integrations

These platforms are native Claude integrations — no MCP connector install needed. They are available as tools when the user connects them in Claude Desktop or Cowork.

| Integration | Purpose |
|-------------|---------|
| **Google Drive** | Shared brand documents, style guides, marketing materials, Google Docs and Slides |
| **Slack** | Brand discussions, channel searches, pinned brand guidelines, informal voice patterns |

## Quick Start

1. Install the plugin in Claude Code or Cowork
2. Connect at least one MCP server (Notion recommended as starting point)
3. Run `/brand-voice:discover-brand` to find your brand materials
4. Run `/brand-voice:generate-guidelines` to create guidelines from the discovery report
5. Use `/brand-voice:enforce-voice` when creating sales or marketing content

### Per-Project Settings

Copy `settings/brand-voice.local.md.example` to `.claude/brand-voice.local.md` in your project and fill in your company name, enabled platforms, and known brand material locations.

## File Structure

```
brand-voice/
├── .claude-plugin/
│   └── plugin.json                              # Plugin manifest
├── .mcp.json                                    # 7 MCP server connections
├── README.md
├── agents/
│   ├── discover-brand.md                         # Autonomous platform search agent
│   ├── content-generation.md                    # Brand-aligned content creation
│   ├── conversation-analysis.md                 # Sales call transcript analysis
│   ├── document-analysis.md                     # Brand document parsing
│   └── quality-assurance.md                     # Compliance and open questions audit
├── commands/
│   ├── discover-brand.md                        # /brand-voice:discover-brand
│   ├── enforce-voice.md                         # /brand-voice:enforce-voice
│   └── generate-guidelines.md                   # /brand-voice:generate-guidelines
├── settings/
│   └── brand-voice.local.md.example             # Per-project settings template
└── skills/
    ├── discover-brand/
    │   ├── SKILL.md                             # Discovery orchestration
    │   └── references/
    │       ├── search-strategies.md             # Platform-specific query patterns
    │       └── source-ranking.md                # Ranking algorithm and categories
    ├── brand-voice-enforcement/
    │   ├── SKILL.md                             # Enforcement orchestration
    │   └── references/
    │       ├── before-after-examples.md         # Content type transformation examples
    │       └── voice-constant-tone-flexes.md    # "We Are / We Are Not" + tone matrix
    └── guideline-generation/
        ├── SKILL.md                             # Generation orchestration
        └── references/
            ├── confidence-scoring.md            # Scoring methodology
            └── guideline-template.md            # Full output template
```

## Architecture

**Skills** provide domain knowledge and orchestrate workflows. They activate automatically based on user intent.

**Agents** handle heavy autonomous work — searching platforms, analyzing documents, parsing transcripts, generating content, and validating quality.

**Commands** are explicit user entry points that trigger the skill workflows.

**Key design decisions:**
- Voice is constant, tone flexes — a clear mental model for enforcement
- Discovery agent is autonomous but accountable — shows its work with provenance and conflicts
- Open questions are a feature, not a failure — every ambiguity includes a recommendation
- Progressive disclosure — frontmatter is lean, SKILL.md is focused, detail lives in references/
- Notion AI Search as federated discovery engine — one API searches 8+ platforms via connected sources
- Google Drive and Slack are native Claude integrations — no MCP connector needed

## License

MIT License

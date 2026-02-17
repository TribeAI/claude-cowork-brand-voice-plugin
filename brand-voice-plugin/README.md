# Brand Voice Plugin for Claude Cowork

## Overview
The Brand Voice Plugin helps sales teams maintain consistent brand voice across all content creation. Generate brand guidelines from your existing documents and sales calls, then enforce those guidelines whenever you create content.

## Installation

### From Cowork UI
1. Open Claude Desktop
2. Navigate to Cowork tab
3. Click "Plugins" in sidebar
4. Select "Upload Plugin"
5. Upload the `brand-voice-plugin.zip` file

## Features

### 1. Brand Voice Enforcement
Automatically apply existing brand guidelines to all sales content.

**Slash Command:** `/brand:enforce-voice`

**Example:**
```
/brand:enforce-voice
Draft a cold outreach email to a VP of Sales at a mid-market SaaS company
```

### 2. Guideline Generation
Generate comprehensive brand guidelines from documents, sales call transcripts, or both.

**Slash Command:** `/brand:generate-guidelines`

**Examples:**
```
/brand:generate-guidelines
Convert my pitch deck and style guide into brand guidelines
```
```
/brand:generate-guidelines
Analyze my last 10 customer calls and create brand voice guidelines
```
```
/brand:generate-guidelines
I have 3 brand docs and 5 sales call transcripts -- generate unified guidelines from all of them
```

## Required Connectors

This plugin works best with the following MCP connectors:

- **Canva** (for creating on-brand visual content)
- **Figma** (for accessing brand design assets)
- **Linear** (for tracking brand guideline updates)
- **Slack** (for sharing guidelines with team)
- **Notion** (for storing guidelines)
- **Google Drive** (for accessing documents)
- **Granola** (for meeting transcripts)
- **Gamma** (for presentation generation)

## Quick Start

1. Install the plugin using the upload method above
2. Connect required MCP servers in Cowork settings
3. Gather your brand documents and/or sales call transcripts
4. Use `/brand:generate-guidelines` to create your brand voice guidelines
5. Use `/brand:enforce-voice` when creating sales content

## File Structure

```
brand-voice-plugin/
├── .claude-plugin/
│   └── plugin.json                        # Plugin manifest
├── .mcp.json                              # MCP server connections
├── agents/                                # Specialized sub-agents
│   ├── content-generation.md              # Generates brand-aligned content
│   ├── conversation-analysis.md           # Analyzes sales call transcripts
│   ├── document-analysis.md               # Parses and extracts from documents
│   └── quality-assurance.md               # Validates content and guidelines
├── commands/                              # Slash commands
│   ├── enforce-voice.md                   # /brand:enforce-voice
│   └── generate-guidelines.md             # /brand:generate-guidelines
├── skills/                                # Auto-triggered skills (directories)
│   ├── brand-voice-enforcement/
│   │   └── SKILL.md                       # Brand enforcement logic
│   └── guideline-generation/
│       └── SKILL.md                       # Guideline generation logic
└── README.md
```

## Support

For issues or questions, contact the Tribe AI team.

## License

MIT License

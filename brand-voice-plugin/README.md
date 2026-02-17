# Brand Voice Plugin for Claude Cowork

## Overview
The Brand Voice Plugin helps sales teams maintain consistent brand voice across all content creation by enforcing existing guidelines, converting messy brand documents to LLM-ready format, and generating new guidelines from conversations.

## Installation

### From Cowork UI
1. Open Claude Desktop
2. Navigate to Cowork tab
3. Click "Plugins" in sidebar
4. Select "Upload Plugin"
5. Navigate to the `brand-voice-plugin` directory
6. Click "Install"

### From Command Line
```bash
# Add to Cowork plugins directory
cp -r ~/brand-voice-plugin ~/.cowork/plugins/brand-voice-plugin
```

## Features

### 1. Brand Voice Enforcement
Automatically apply existing brand guidelines to all sales content.

**Slash Command:** `/brand:enforce-voice`

**Example:**
```
/brand:enforce-voice
Draft a cold outreach email to a VP of Sales at a mid-market SaaS company
```

### 2. Document Conversion
Convert scattered brand documents (PDFs, PowerPoints, Google Docs) into a unified LLM-ready format.

**Slash Command:** `/brand:convert-docs`

**Example:**
```
/brand:convert-docs
Convert the 3 brand documents in my Google Drive folder to a single guideline doc
```

### 3. Guideline Generation
Generate comprehensive brand guidelines from recorded sales conversations.

**Slash Command:** `/brand:generate-guidelines`

**Example:**
```
/brand:generate-guidelines
Analyze my last 10 customer calls and create brand voice guidelines
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

1. Install the plugin using one of the methods above
2. Connect required MCP servers in Cowork settings
3. Upload existing brand documents OR prepare meeting transcripts
4. Use `/brand:convert-docs` or `/brand:generate-guidelines` to create your first brand guide
5. Use `/brand:enforce-voice` when creating sales content

## File Structure

```
brand-voice-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin configuration
├── .mcp.json                # MCP server connections
├── commands/                # Slash commands
│   ├── enforce-voice.md
│   ├── convert-docs.md
│   └── generate-guidelines.md
├── skills/                  # Auto-triggered skills
│   ├── brand-voice-enforcement.md
│   ├── document-conversion.md
│   └── guideline-generation.md
└── README.md
```

## Support

For issues or questions, contact the Tribe AI team.

## License

MIT License

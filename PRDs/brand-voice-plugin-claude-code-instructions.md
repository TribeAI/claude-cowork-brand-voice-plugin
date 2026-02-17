# Claude Code Instructions: Brand Voice Plugin Development

## Overview
You are building a Claude Cowork plugin called `brand-voice-plugin` that helps sales teams maintain consistent brand voice across content creation. This document provides complete instructions for file structure creation and implementation.

---

## Architecture Overview

### Cowork Plugin Structure
Claude Cowork plugins follow a specific directory convention:
- **Skills** are directories containing a `SKILL.md` file with YAML frontmatter
- **Commands** are `.md` files with YAML frontmatter in a `commands/` directory
- **Agents** (sub-agents) are `.md` files with YAML frontmatter in an `agents/` directory
- **Plugin manifest** (`plugin.json`) uses a minimal schema -- Cowork auto-discovers skills, commands, and agents from their directories
- **MCP config** (`.mcp.json`) entries require `"type": "http"` for remote servers

### Key Conventions
- Skills use `SKILL.md` as the entrypoint file (must be uppercase)
- YAML frontmatter fields: `name`, `description`, `model`, `tools`, `maxTurns`
- Commands link to skills via a `skill` field in frontmatter
- Agents are invoked by skills via the `Task` tool
- No need to list skills/commands/agents in plugin.json (auto-discovered)

---

## PHASE 1: Create File Structure

### Step 1: Create Root Directory and Structure

```bash
# Create the main plugin directory
mkdir -p ~/brand-voice-plugin

# Create the core directory structure
cd ~/brand-voice-plugin
mkdir -p .claude-plugin
mkdir -p commands
mkdir -p skills/brand-voice-enforcement
mkdir -p skills/document-conversion
mkdir -p skills/guideline-generation
mkdir -p agents

# Create configuration files
touch .claude-plugin/plugin.json
touch .mcp.json
touch README.md
```

### Step 2: Create Plugin Manifest (plugin.json)

Create `.claude-plugin/plugin.json` with minimal schema:

```json
{
  "name": "brand-voice-plugin",
  "version": "1.0.0",
  "description": "Enforce brand voice, convert messy brand docs to LLM-ready format, and generate brand guidelines from conversations",
  "author": "Tribe AI",
  "keywords": ["sales", "marketing", "brand", "content-creation", "guidelines"]
}
```

**Important:** Do NOT include `skills`, `commands`, `sub_agents`, `connectors`, `tags`, `permissions`, or `main_skill` fields. Cowork auto-discovers these from the directory structure.

### Step 3: Create MCP Configuration (.mcp.json)

Create `.mcp.json` with `"type": "http"` for each server:

```json
{
  "mcpServers": {
    "canva": {
      "type": "http",
      "url": "https://mcp.canva.com/mcp"
    },
    "figma": {
      "type": "http",
      "url": "https://mcp.figma.com/mcp"
    },
    "linear": {
      "type": "http",
      "url": "https://mcp.linear.app/mcp"
    },
    "slack": {
      "type": "http",
      "url": "https://mcp.slack.com/mcp"
    },
    "notion": {
      "type": "http",
      "url": "https://mcp.notion.com/mcp"
    },
    "google-drive": {
      "type": "http",
      "url": "https://mcp.googledrive.com/mcp"
    },
    "granola": {
      "type": "http",
      "url": "https://mcp.granola.ai/mcp"
    },
    "gamma": {
      "type": "http",
      "url": "https://mcp.gamma.app/mcp"
    }
  }
}
```

**Important:** Do NOT include `description` per server or `requiredPermissions` at the top level. These are not part of the Cowork MCP schema.

### Step 4: Verify Structure

```bash
tree ~/brand-voice-plugin
```

Expected output:
```
brand-voice-plugin/
├── .claude-plugin/
│   └── plugin.json
├── .mcp.json
├── README.md
├── agents/
│   ├── content-generation.md
│   ├── conversation-analysis.md
│   ├── document-analysis.md
│   └── quality-assurance.md
├── commands/
│   ├── convert-docs.md
│   ├── enforce-voice.md
│   └── generate-guidelines.md
└── skills/
    ├── brand-voice-enforcement/
    │   └── SKILL.md
    ├── document-conversion/
    │   └── SKILL.md
    └── guideline-generation/
        └── SKILL.md
```

---

## PHASE 2: Implement Skills

Skills are directories with a `SKILL.md` file. Each SKILL.md must have YAML frontmatter.

### Skill YAML Frontmatter Format
```yaml
---
name: skill-name
description: What this skill does
model: sonnet
tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - WebFetch
  - Task
maxTurns: 15
---
```

### Skill 1: Brand Voice Enforcement
**File:** `skills/brand-voice-enforcement/SKILL.md`

**Purpose:** Automatically apply existing brand guidelines to all sales and marketing content.

**Key behaviors:**
- Loads brand guidelines from `/mnt/user-data/outputs/brand-guidelines/`, Notion, or Google Drive
- Analyzes content requests (type, audience, key messages)
- Applies voice, tone, messaging, and style constraints
- Generates content and validates against guidelines
- Explains brand choices made

**Delegates to agents:**
- `content-generation` for long-form or complex content
- `quality-assurance` for high-stakes validation

### Skill 2: Document Conversion
**File:** `skills/document-conversion/SKILL.md`

**Purpose:** Transform scattered brand documentation into structured, LLM-optimized Markdown.

**Key behaviors:**
- Ingests documents (PDF, PPTX, DOCX, Google Docs, plain text)
- Extracts brand elements: voice attributes, tone, messages, terminology, examples
- Organizes into structured guideline format
- Handles deduplication and conflict resolution across sources
- Assigns confidence scores per section

**Delegates to agents:**
- `document-analysis` for heavy parsing and cross-document analysis
- `quality-assurance` for completeness validation

### Skill 3: Guideline Generation
**File:** `skills/guideline-generation/SKILL.md`

**Purpose:** Generate brand guidelines from sales call transcripts and conversations.

**Key behaviors:**
- Ingests transcripts from Granola (MCP), Gong, Zoom, manual uploads, Notion
- Analyzes: voice attributes, messaging patterns, tone by context, success patterns, anti-patterns
- Synthesizes findings into comprehensive guidelines with confidence scores
- Protects PII (redacts customer names, contact info)

**Delegates to agents:**
- `conversation-analysis` for deep transcript analysis
- `quality-assurance` for guideline validation

---

## PHASE 3: Implement Commands

Commands are `.md` files with YAML frontmatter in the `commands/` directory.

### Command YAML Frontmatter Format
```yaml
---
name: command-name
description: What this command does
skill: linked-skill-name
---
```

The `skill` field links the command to the skill that handles it.

### Command 1: /brand:enforce-voice
**File:** `commands/enforce-voice.md`
**Links to:** `brand-voice-enforcement` skill

### Command 2: /brand:convert-docs
**File:** `commands/convert-docs.md`
**Links to:** `document-conversion` skill

### Command 3: /brand:generate-guidelines
**File:** `commands/generate-guidelines.md`
**Links to:** `guideline-generation` skill

---

## PHASE 4: Implement Agents (Sub-Agents)

Agents are `.md` files with YAML frontmatter in the `agents/` directory. They are invoked by skills via the `Task` tool.

### Agent YAML Frontmatter Format
```yaml
---
name: agent-name
description: What this agent specializes in
model: sonnet
tools:
  - Read
  - Glob
  - Grep
maxTurns: 15
---
```

The body of the agent file is its system prompt.

### Agent 1: Document Analysis
**File:** `agents/document-analysis.md`
**Model:** sonnet
**Purpose:** Parse and analyze brand documents, extract brand elements, detect cross-document patterns and conflicts.

### Agent 2: Conversation Analysis
**File:** `agents/conversation-analysis.md`
**Model:** sonnet
**Purpose:** Analyze sales call transcripts for voice patterns, messaging effectiveness, tone variations, and success correlation.

### Agent 3: Content Generation
**File:** `agents/content-generation.md`
**Model:** sonnet
**Purpose:** Generate brand-aligned content by applying multiple brand constraints simultaneously.

### Agent 4: Quality Assurance
**File:** `agents/quality-assurance.md`
**Model:** haiku
**Purpose:** Validate content and guidelines against brand standards. Lightweight model since this is checking, not generating.

---

## PHASE 5: Testing & Verification

### Local Testing with Cowork
1. Install the plugin in Claude Cowork:
   ```bash
   cp -r ~/brand-voice-plugin ~/.cowork/plugins/brand-voice-plugin
   ```
2. Open Claude Desktop and navigate to Cowork
3. Verify plugin appears in plugin list
4. Test each command:
   - `/brand:convert-docs` with sample brand documents
   - `/brand:generate-guidelines` with sample transcripts
   - `/brand:enforce-voice` with a content request

### Demo Test Suite
A TDD demo suite is available in the `demo/` directory at the repo root:
- `demo/tests/` - Test scenarios for each skill
- `demo/fixtures/inputs/` - Sample brand docs and transcripts
- `demo/fixtures/expected-outputs/` - Expected guideline outputs
- `demo/validation/` - Validation criteria
- `demo/run-demo.md` - Full 30-45 minute demo walkthrough

### Verification Checklist
- [ ] Plugin loads in Cowork without errors
- [ ] All 3 slash commands are discoverable
- [ ] Skills activate on appropriate triggers
- [ ] Sub-agents are invoked correctly by skills
- [ ] MCP connectors are listed (connection depends on user auth)
- [ ] Brand guidelines output follows expected structure
- [ ] Content generation applies guidelines correctly

---

## Tier 1 MCP Connectors

| Connector | URL | Purpose |
|-----------|-----|---------|
| Canva | https://mcp.canva.com/mcp | Create on-brand visual content |
| Figma | https://mcp.figma.com/mcp | Access brand design assets |
| Linear | https://mcp.linear.app/mcp | Track guideline updates |
| Slack | https://mcp.slack.com/mcp | Share guidelines with team |
| Notion | https://mcp.notion.com/mcp | Store/retrieve guidelines |
| Google Drive | https://mcp.googledrive.com/mcp | Access brand documents |
| Granola | https://mcp.granola.ai/mcp | Meeting transcript access |
| Gamma | https://mcp.gamma.app/mcp | Generate presentations |

---

## Model Selection Guide

| Use Case | Model | Reasoning |
|----------|-------|-----------|
| Primary skill operations | Sonnet 4.5 | Best balance of quality, speed, and cost |
| Document/conversation analysis | Sonnet 4.5 | Complex pattern recognition |
| Content generation | Sonnet 4.5 | High-quality writing |
| Quality assurance/validation | Haiku 4.5 | Lightweight checking tasks |
| High-stakes content (enterprise proposals) | Opus 4.6 | Maximum quality when it matters |

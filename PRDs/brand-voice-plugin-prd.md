# Brand Voice Plugin - Product Requirements Document

## Executive Summary

The Brand Voice Plugin is a high-impact Claude Cowork plugin designed to help sales teams maintain consistent brand voice across all content creation. This plugin addresses the critical need for structured, LLM-ready brand guidelines and provides tools to both enforce existing brand voice and generate new guidelines from scratch.

**Target Launch:** Demo-ready within 24 hours
**Primary Users:** Sales teams, marketing teams, content creators
**Core Value Proposition:** Transform unstructured brand documents into AI-ready guidelines and enforce consistent brand voice across all sales materials

---

## Problem Statement

Sales teams face three critical challenges with brand voice:

1. **Inconsistent Content Generation:** Without structured brand guidelines, AI-generated content lacks consistency in tone, messaging, and positioning
2. **Fragmented Documentation:** Brand guidelines exist in various formats (PDFs, slide decks, Google Docs) that aren't optimized for LLM consumption
3. **Manual Brand Voice Creation:** Developing comprehensive brand guidelines from scratch is time-consuming and requires expertise

---

## Plugin Overview

**Plugin Name:** `brand-voice-plugin`

**Plugin Structure:**
```
brand-voice-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── .mcp.json                # MCP connector configuration
├── commands/                # Slash commands for explicit invocation
│   ├── enforce-voice.md
│   ├── convert-docs.md
│   └── generate-guidelines.md
└── skills/                  # Auto-triggered domain knowledge
    ├── brand-voice-enforcement.md
    ├── document-conversion.md
    └── guideline-generation.md
```

---

## Core Skills (Detailed Specifications)

### Skill 1: Enforce Brand Voice from Existing Guidelines

**File:** `skills/brand-voice-enforcement.md`

**Purpose:** Apply existing LLM-ready brand guidelines to all content generation, ensuring consistency in tone, messaging, and style.

**Functionality:**
- Automatically detect when the user is creating sales/marketing content
- Reference the stored brand guidelines document
- Apply voice, tone, and messaging rules to generated content
- Flag inconsistencies and suggest corrections
- Validate content against brand do's and don'ts

**Input Requirements:**
- Pre-existing brand guidelines document in LLM-ready format (Markdown)
- Document should include:
  - Brand voice attributes (e.g., "confident but not arrogant")
  - Tone guidelines by content type (emails, presentations, proposals)
  - Key messaging pillars
  - Terminology preferences and prohibited words
  - Example content demonstrating brand voice

**Output:**
- Content that adheres to brand guidelines
- Explanation of applied brand principles
- Suggestions for improvement when guidelines are violated

**Slash Command:** `/brand:enforce-voice`

**Use Cases:**
- Drafting sales emails with consistent brand voice
- Creating pitch decks that match brand positioning
- Writing proposals that reflect company values
- Generating social media content with appropriate tone

---

### Skill 2: Convert Messy Brand Documents to LLM-Ready Format

**File:** `skills/document-conversion.md`

**Purpose:** Transform existing brand documentation (PDFs, PowerPoint decks, scattered Google Docs) into a structured, LLM-optimized format.

**Functionality:**
- Ingest documents in various formats (PDF, DOCX, PPTX, Google Docs/Slides)
- Extract brand voice elements:
  - Mission/vision statements
  - Value propositions
  - Tone descriptors
  - Example content
  - Visual brand guidelines (for context)
  - Messaging frameworks
- Reorganize into structured Markdown format with clear sections
- Create a comprehensive, queryable brand guideline document
- Add metadata tags for easy retrieval

**Input Requirements:**
- One or more brand documents (any format)
- Optional: User guidance on priority documents or sections

**Output:**
- Single consolidated Markdown document with:
  - Brand Voice Overview
  - Tone & Style Guidelines
  - Messaging Framework
  - Content Examples (Do's and Don'ts)
  - Terminology Guide
  - Context-specific Guidelines (email vs. presentation vs. proposal)

**Slash Command:** `/brand:convert-docs`

**Use Cases:**
- Onboarding new sales reps with consolidated brand guide
- Migrating from scattered brand documentation to unified source
- Preparing brand guidelines for AI-powered content generation
- Cleaning up legacy brand documentation

---

### Skill 3: Generate Brand Guidelines from Recorded Conversations

**File:** `skills/guideline-generation.md`

**Purpose:** Create comprehensive brand guidelines from scratch by analyzing recorded sales calls, customer conversations, and team discussions.

**Functionality:**
- Analyze conversation transcripts to identify:
  - Consistent messaging patterns
  - Successful pitch language
  - Tone patterns in top performer calls
  - Customer pain points and positioning
  - Common objections and responses
- Extract implicit brand voice attributes from successful conversations
- Generate structured brand guidelines document
- Provide recommendations based on best practices

**Input Requirements:**
- Meeting transcripts (from Zoom, Gong, Granola, etc.)
- Optional: User input on which conversations represent "ideal" brand voice
- Optional: Existing partial brand documentation

**Output:**
- Comprehensive brand guidelines document including:
  - Derived brand voice attributes
  - Tone recommendations
  - Messaging framework based on successful patterns
  - Example phrases from actual conversations
  - Do's and Don'ts extracted from call analysis
  - Context-specific guidelines by conversation type

**Slash Command:** `/brand:generate-guidelines`

**Use Cases:**
- Startup creating first brand guidelines from founder sales calls
- Sales team documenting what actually works in the field
- Capturing implicit brand voice from top performers
- Evolving brand voice based on customer conversations

---

## MCP Connectors & Integrations

### Priority Connectors for Sales Teams

Based on research, the following connectors are most valuable for sales teams:

#### Tier 1 - Essential (Must-Have)
1. **Google Drive** 
   - Access brand documents stored in Drive
   - Save generated guidelines back to Drive
   - **MCP URL:** Use Google Drive connector (available in Claude.ai)

2. **Notion**
   - Store and retrieve brand guidelines from Notion workspace
   - Access existing brand documentation in Notion
   - **MCP URL:** `https://mcp.notion.com/mcp`

3. **Google Slides**
   - Extract brand voice from existing pitch decks
   - Apply brand voice to new presentations
   - **MCP URL:** Use Google Drive connector

#### Tier 2 - High-Value (Recommended)
4. **Gong** *(if available)*
   - Access recorded sales conversations
   - Analyze call transcripts for brand voice patterns
   - Extract successful messaging from top performers
   - **Integration Note:** Gong doesn't have a public MCP server yet, but can be accessed via:
     - Manual transcript upload
     - API integration if available
     - Placeholder for future MCP integration

5. **Granola**
   - Access meeting transcripts and notes
   - Extract brand voice from internal discussions
   - **MCP URL:** `https://mcp.granola.ai/mcp`

6. **Gamma**
   - Generate on-brand presentations
   - Apply brand guidelines to new decks
   - **MCP URL:** `https://mcp.gamma.app/mcp`

#### Tier 3 - Nice-to-Have (Optional)
7. **Slack**
   - Extract brand voice from internal communications
   - Share brand guidelines with team
   - **MCP URL:** `https://mcp.slack.com/mcp`

8. **Linear** (for product positioning)
   - Connect product messaging with brand voice
   - **MCP URL:** `https://mcp.linear.app/mcp`

### Connector Configuration

The `.mcp.json` file should include:

```json
{
  "mcpServers": {
    "notion": {
      "url": "https://mcp.notion.com/mcp"
    },
    "granola": {
      "url": "https://mcp.granola.ai/mcp"
    },
    "gamma": {
      "url": "https://mcp.gamma.app/mcp"
    },
    "slack": {
      "url": "https://mcp.slack.com/mcp"
    }
  }
}
```

**Note:** Google Drive connector will be configured through Claude.ai's built-in connector settings.

---

## Sub-Agents

### 1. Document Analysis Agent
**Purpose:** Parse and extract brand voice elements from documents
**Triggers:** When processing uploaded documents or Drive files
**Capabilities:**
- PDF text extraction
- PPTX content parsing
- Structure recognition
- Brand element identification

### 2. Conversation Analysis Agent
**Purpose:** Analyze meeting transcripts for brand voice patterns
**Triggers:** When generating guidelines from conversations
**Capabilities:**
- Transcript processing
- Pattern recognition across multiple calls
- Tone analysis
- Messaging extraction

### 3. Content Generation Agent
**Purpose:** Apply brand voice to new content
**Triggers:** When creating emails, decks, proposals
**Capabilities:**
- Brand guideline application
- Real-time validation
- Tone adjustment
- Consistency checking

### 4. Quality Assurance Agent
**Purpose:** Validate content against brand guidelines
**Triggers:** When reviewing generated content
**Capabilities:**
- Guideline compliance checking
- Inconsistency flagging
- Improvement suggestions
- Best practice recommendations

---

## Slash Commands

### `/brand:enforce-voice`
Apply existing brand guidelines to current content

**Usage:**
```
/brand:enforce-voice
Draft a sales email to a Fortune 500 CTO about our AI platform
```

### `/brand:convert-docs`
Convert uploaded brand documents to LLM-ready format

**Usage:**
```
/brand:convert-docs
Convert these 3 PDFs into a unified brand guideline document
```

### `/brand:generate-guidelines`
Generate brand guidelines from conversation transcripts

**Usage:**
```
/brand:generate-guidelines
Analyze my last 10 sales calls and create brand guidelines
```

---

## Success Metrics

### Plugin Performance
- Time to generate guidelines: < 5 minutes
- Brand voice consistency score: > 90%
- Document conversion accuracy: > 95%

### User Experience
- Setup time: < 10 minutes
- Time saved per content piece: 15-20 minutes
- User satisfaction: 4.5/5 stars

### Business Impact
- Reduced brand inconsistency incidents
- Faster sales content creation
- Improved message consistency across team
- Reduced onboarding time for new reps

---

## Technical Requirements

### Dependencies
- Python 3.9+ (for MCP server integration)
- Access to Claude Cowork filesystem
- MCP protocol support
- File parsing libraries (pypdf, python-pptx, python-docx)

### File Format Support
**Input:**
- PDF (.pdf)
- PowerPoint (.pptx)
- Word Documents (.docx)
- Google Docs (via Drive connector)
- Google Slides (via Drive connector)
- Plain text (.txt, .md)
- Meeting transcripts (JSON, TXT)

**Output:**
- Markdown (.md) - primary format for guidelines
- JSON (for structured data)

### Storage
- Brand guidelines stored in `/mnt/user-data/outputs/brand-guidelines/`
- Temporary processing in `/home/claude/brand-temp/`

---

## Implementation Phases

### Phase 1: Core Infrastructure (Hours 0-4)
- [ ] Create plugin file structure
- [ ] Configure plugin.json manifest
- [ ] Set up MCP connector configuration
- [ ] Create placeholder skill files

### Phase 2: Skill Development (Hours 4-16)
- [ ] Implement brand voice enforcement skill
- [ ] Build document conversion skill
- [ ] Develop guideline generation skill
- [ ] Create sub-agents

### Phase 3: Integration & Testing (Hours 16-22)
- [ ] Connect MCP servers (Notion, Granola, Gamma, Slack)
- [ ] Test with sample documents
- [ ] Validate output quality
- [ ] Debug and refine

### Phase 4: Polish & Demo Prep (Hours 22-24)
- [ ] Create example workflows
- [ ] Prepare demo script
- [ ] Document usage instructions
- [ ] Create quick-start guide

---

## Demo Scenarios

### Scenario 1: New Sales Rep Onboarding
**Setup:** Scattered brand documents in Google Drive
**Flow:**
1. Use `/brand:convert-docs` to consolidate documents
2. Generate unified brand guide
3. Use `/brand:enforce-voice` to draft first email
4. Show before/after comparison

### Scenario 2: Capturing Founder Voice
**Setup:** 5 recorded sales calls from founder
**Flow:**
1. Upload Granola transcripts
2. Use `/brand:generate-guidelines` 
3. Show extracted brand voice attributes
4. Apply to new pitch deck with Gamma

### Scenario 3: Sales Content Sprint
**Setup:** Need to create 10 personalized outreach emails
**Flow:**
1. Load existing brand guidelines
2. Use `/brand:enforce-voice` for each email
3. Show consistency across all emails
4. Demonstrate time savings

---

## Future Enhancements (Post-Launch)

- **Multi-brand Support:** Manage multiple brand voices for sub-brands
- **A/B Testing:** Test different brand voice variations
- **Performance Analytics:** Track which brand voice patterns convert best
- **Video Analysis:** Extract brand voice from video content
- **Real-time Coaching:** Live brand voice suggestions during writing
- **Brand Voice Drift Detection:** Alert when team strays from guidelines
- **Industry-specific Templates:** Pre-built brand voice templates by industry

---

## Appendix A: Sample Brand Guideline Structure

```markdown
# [Company Name] Brand Voice Guidelines

## Brand Voice Overview
- **Voice Attributes:** [e.g., confident, approachable, technical but accessible]
- **Brand Personality:** [e.g., the expert friend who makes complex simple]
- **Core Values:** [what we stand for]

## Tone Guidelines

### Email Tone
- Professional but warm
- Direct and action-oriented
- Avoid jargon unless technical audience

### Presentation Tone
- Bold and confident
- Data-driven
- Story-led

### Proposal Tone
- Consultative
- Problem-solution focused
- ROI-oriented

## Messaging Framework

### Value Proposition
[Core value prop]

### Key Messages
1. [Message pillar 1]
2. [Message pillar 2]
3. [Message pillar 3]

### Positioning
- **Against Competitor A:** [positioning]
- **Against Competitor B:** [positioning]

## Content Examples

### Do This
[Examples of on-brand content]

### Not This
[Examples of off-brand content with explanations]

## Terminology Guide

### Preferred Terms
- Use "AI-powered" not "AI-driven"
- Use "platform" not "tool"

### Prohibited Terms
- Avoid "revolutionary" (overused)
- Avoid "synergy" (corporate jargon)

## Context-Specific Guidelines

### Cold Outreach
[Specific guidelines]

### Follow-up Emails
[Specific guidelines]

### Closing Conversations
[Specific guidelines]
```

---

## Questions for Clarification

1. Do you have existing brand documentation we should use as input for testing?
2. Which MCP connectors are already configured in your Claude.ai setup?
3. Are there specific sales scenarios you want prioritized for the demo?
4. What's the primary storage location for brand documents (Google Drive, Notion, both)?
5. Do you have access to Gong, or should we focus on Granola for conversation analysis?

# Claude Code Instructions: Brand Voice Plugin Development

## Overview
You are building a Claude Cowork plugin called `brand-voice-plugin` that helps sales teams maintain consistent brand voice across content creation. This document provides complete instructions for file structure creation and implementation.

---

## PHASE 1: Create File Structure

### Step 1: Create Root Directory and Basic Structure

```bash
# Create the main plugin directory
mkdir -p ~/brand-voice-plugin

# Navigate to the plugin directory
cd ~/brand-voice-plugin

# Create the core directory structure
mkdir -p .claude-plugin
mkdir -p commands
mkdir -p skills

# Create the primary configuration files
touch .claude-plugin/plugin.json
touch .mcp.json
touch README.md
```

### Step 2: Create Plugin Manifest (plugin.json)

Create `.claude-plugin/plugin.json` with the following content:

```json
{
  "name": "brand-voice-plugin",
  "version": "1.0.0",
  "description": "Enforce brand voice, convert messy brand docs to LLM-ready format, and generate brand guidelines from conversations",
  "author": "Tribe AI",
  "main_skill": "skills/brand-voice-enforcement.md",
  "skills": [
    "skills/brand-voice-enforcement.md",
    "skills/document-conversion.md",
    "skills/guideline-generation.md"
  ],
  "commands": [
    "commands/enforce-voice.md",
    "commands/convert-docs.md",
    "commands/generate-guidelines.md"
  ],
  "connectors": [
    "canva",
    "figma",
    "linear",
    "slack",
    "notion",
    "google-drive",
    "granola",
    "gamma"
  ],
  "sub_agents": [
    "document-analysis",
    "conversation-analysis",
    "content-generation",
    "quality-assurance"
  ],
  "tags": ["sales", "marketing", "brand", "content-creation", "guidelines"],
  "permissions": {
    "file_access": true,
    "network_access": true,
    "mcp_servers": true
  }
}
```

### Step 3: Create MCP Configuration (.mcp.json)

Create `.mcp.json` with the following content:

```json
{
  "mcpServers": {
    "canva": {
      "url": "https://mcp.canva.com/mcp",
      "description": "Create on-brand visual content and graphics"
    },
    "figma": {
      "url": "https://mcp.figma.com/mcp",
      "description": "Access brand design assets and visual guidelines"
    },
    "linear": {
      "url": "https://mcp.linear.app/mcp",
      "description": "Track brand guideline updates and content requests"
    },
    "slack": {
      "url": "https://mcp.slack.com/mcp",
      "description": "Share brand guidelines with team"
    },
    "notion": {
      "url": "https://mcp.notion.com/mcp",
      "description": "Store and retrieve brand guidelines from Notion workspace"
    },
    "google-drive": {
      "url": "https://mcp.googledrive.com/mcp",
      "description": "Access brand documents from Google Drive folders"
    },
    "granola": {
      "url": "https://mcp.granola.ai/mcp",
      "description": "Access meeting transcripts for brand voice analysis"
    },
    "gamma": {
      "url": "https://mcp.gamma.app/mcp",
      "description": "Generate on-brand presentations"
    }
  },
  "requiredPermissions": [
    "read_files",
    "write_files",
    "network_requests"
  ]
}
```

### Step 4: Create Skill Files (Templates)

Create empty skill files that will be populated in Phase 2:

```bash
touch skills/brand-voice-enforcement.md
touch skills/document-conversion.md
touch skills/guideline-generation.md
```

### Step 5: Create Command Files (Templates)

Create empty command files:

```bash
touch commands/enforce-voice.md
touch commands/convert-docs.md
touch commands/generate-guidelines.md
```

### Step 6: Create README

Create `README.md` with the following content:

```markdown
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
```

### Step 7: Verify Structure

Run this command to verify the structure is correct:

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
├── commands/
│   ├── enforce-voice.md
│   ├── convert-docs.md
│   └── generate-guidelines.md
└── skills/
    ├── brand-voice-enforcement.md
    ├── document-conversion.md
    └── guideline-generation.md
```

---

## PHASE 2: Implement Skills

### Skill 1: Brand Voice Enforcement

Edit `skills/brand-voice-enforcement.md`:

```markdown
# Brand Voice Enforcement Skill

## Purpose
Automatically apply existing brand guidelines to all sales and marketing content to ensure consistency in tone, messaging, and style.

## When This Skill Activates

This skill automatically activates when:
- The user is drafting emails, proposals, or presentations
- The user explicitly uses `/brand:enforce-voice`
- Content contains sales or marketing language
- The user references "brand voice" or "on-brand"

## What This Skill Does

### 1. Load Brand Guidelines
- Check for existing brand guidelines in:
  - `/mnt/user-data/outputs/brand-guidelines/`
  - Connected Notion workspace
  - Google Drive folder labeled "Brand Guidelines"
- If no guidelines found, prompt user to either:
  - Upload brand documents (trigger Skill 2)
  - Generate guidelines from calls (trigger Skill 3)

### 2. Analyze Content Request
When the user asks to create content:
- Identify content type (email, presentation, proposal, social post)
- Determine target audience
- Identify key messages needed
- Note any specific requirements

### 3. Apply Brand Guidelines
**Voice & Tone:**
- Apply brand personality attributes
- Adjust formality level based on context
- Ensure consistent use of terminology

**Messaging:**
- Incorporate key message pillars
- Use approved value propositions
- Follow positioning statements

**Style:**
- Follow preferred sentence structure
- Use approved terminology
- Avoid prohibited words/phrases
- Match example content patterns

### 4. Generate Content
Create content that:
- Matches brand voice attributes
- Follows tone guidelines for content type
- Incorporates key messages naturally
- Uses approved terminology
- Mirrors successful example patterns

### 5. Validate & Explain
After generation:
- Highlight where brand guidelines were applied
- Explain key brand voice decisions
- Note any areas where guidelines were adapted for context
- Suggest improvements if user wants to refine

## Example Workflows

### Workflow 1: Cold Outreach Email
```
User: "Draft a cold email to a VP of Sales at a Series B SaaS company"

Skill Actions:
1. Load brand guidelines
2. Identify this is cold outreach → apply "professional but warm" tone
3. Use value proposition: "AI that helps sales teams close faster"
4. Incorporate key message: "data-driven insights"
5. Generate email following successful cold email examples
6. Avoid prohibited term "synergy"
7. Present email with explanation of brand choices
```

### Workflow 2: Pitch Deck Creation
```
User: "/brand:enforce-voice Create a 10-slide pitch deck for an enterprise client"

Skill Actions:
1. Load brand guidelines
2. Apply "bold and confident" presentation tone
3. Use data-driven approach per guidelines
4. Structure following approved pitch format
5. Generate deck outline with brand-aligned messaging
6. If Gamma connector available, create actual slides
7. Explain brand voice application in each section
```

### Workflow 3: Proposal Writing
```
User: "Write a proposal for our AI platform implementation"

Skill Actions:
1. Load brand guidelines
2. Apply "consultative" proposal tone
3. Lead with problem-solution framework per guidelines
4. Include ROI-focused language
5. Use approved case study examples
6. Format following proposal template
7. Validate against brand do's and don'ts
```

## Brand Guideline Structure

This skill expects brand guidelines in this format:

```markdown
# Brand Voice Guidelines

## Voice Attributes
- Attribute 1: [description]
- Attribute 2: [description]

## Tone by Content Type
### Email
- [tone description]
- [key principles]

### Presentations
- [tone description]
- [key principles]

## Key Messages
1. [Message pillar 1]
2. [Message pillar 2]

## Terminology
### Preferred
- [term]: [usage]

### Prohibited
- [term]: [reason]

## Examples
### Good Example
[example with explanation]

### Bad Example
[example with explanation]
```

## Sub-Agent: Content Generation Agent

When generating content, delegate to specialized sub-agent:

**Capabilities:**
- Apply multiple brand constraints simultaneously
- Balance brand voice with user's specific requirements
- Adapt guidelines for different contexts
- Maintain consistency across long-form content

**Invocation:**
```
Invoke Content-Generation-Agent with:
- Brand guidelines document
- Content type and requirements
- Target audience
- Specific user instructions
```

## Error Handling

### No Brand Guidelines Found
```
I don't see any brand guidelines yet. I can help you:
1. Convert existing brand documents to guidelines (/brand:convert-docs)
2. Generate guidelines from your sales calls (/brand:generate-guidelines)
3. Create a basic template to get started

Which would you prefer?
```

### Conflicting Requirements
```
I notice the user's request [specific requirement] conflicts with 
brand guideline [specific guideline]. 

Options:
1. Follow brand guideline strictly
2. Adapt guideline for this specific context
3. Ask user for clarification

Recommendation: [choice with reasoning]
```

## Best Practices

1. **Always explain brand choices:** Help users understand why content is written a certain way
2. **Adapt, don't force:** Brand guidelines are principles, not rigid rules
3. **Learn from feedback:** Note when users change generated content
4. **Context matters:** Sales email to CEO vs. junior employee needs different approach
5. **Be specific:** Don't just say "on-brand," explain what that means

## Integration Points

### With Document Conversion Skill
- If no guidelines exist, automatically offer to convert documents
- Update enforcement when guidelines are regenerated

### With Guideline Generation Skill
- If generating new guidelines, immediately apply them
- Suggest updating guidelines based on successful content

### With MCP Connectors
- **Notion:** Retrieve guidelines from shared workspace
- **Google Drive:** Access brand document folders
- **Gamma:** Apply brand to presentation generation
- **Slack:** Reference shared brand messaging
```

### Skill 2: Document Conversion

Edit `skills/document-conversion.md`:

```markdown
# Document Conversion Skill

## Purpose
Transform scattered brand documentation (PDFs, PowerPoints, Google Docs) into a structured, LLM-optimized Markdown format.

## When This Skill Activates

This skill automatically activates when:
- The user uploads brand-related documents
- The user uses `/brand:convert-docs`
- The user mentions "converting" or "consolidating" brand materials
- Multiple brand documents are detected in the workspace

## What This Skill Does

### 1. Document Discovery & Ingestion

**Supported Formats:**
- PDF (.pdf)
- PowerPoint (.pptx)
- Word Documents (.docx)
- Google Docs (via Drive connector)
- Google Slides (via Drive connector)
- Plain text (.txt, .md)
- Images with text (OCR)

**Document Sources:**
- User uploads to Cowork
- Google Drive folders
- Notion pages
- Direct file paths

**Ingestion Process:**
```python
# Pseudo-code for reference
def ingest_documents(file_paths):
    documents = []
    for path in file_paths:
        if path.endswith('.pdf'):
            text = extract_pdf_text(path)
        elif path.endswith('.pptx'):
            text = extract_pptx_content(path)
        elif path.endswith('.docx'):
            text = extract_docx_content(path)
        
        documents.append({
            'filename': path,
            'content': text,
            'type': detect_content_type(text)
        })
    return documents
```

### 2. Content Analysis & Extraction

**Brand Elements to Extract:**

1. **Voice Attributes**
   - Look for: adjectives describing tone, personality descriptors
   - Extract from: mission statements, about pages, messaging docs
   - Examples: "confident," "approachable," "technical but accessible"

2. **Tone Guidelines**
   - Look for: instructions on how to write different content types
   - Extract from: style guides, email templates, presentation rules
   - Organize by: content type, audience, situation

3. **Key Messages**
   - Look for: repeated themes, value propositions, positioning
   - Extract from: pitch decks, sales playbooks, marketing materials
   - Identify: primary, secondary, and tertiary messages

4. **Terminology**
   - Look for: glossaries, preferred/prohibited terms, industry jargon
   - Extract from: product docs, competitive positioning, style guides
   - Categorize: must-use, preferred, avoid, never-use

5. **Example Content**
   - Look for: successful emails, presentations, proposals
   - Extract from: templates, previous campaigns, top performer content
   - Label: good examples vs. what to avoid

6. **Visual Brand Elements** (for context only)
   - Look for: color codes, logo usage, typography rules
   - Extract from: brand guideline PDFs, design documents
   - Note: These inform tone but aren't directly applied

### 3. Content Organization

**Structured Output Format:**

```markdown
# [Company Name] Brand Voice Guidelines

## Document Metadata
- Created: [date]
- Source Documents: [list]
- Last Updated: [date]
- Version: 1.0

## Executive Summary
[2-3 paragraph overview of brand voice]

## Brand Voice Overview

### Core Voice Attributes
1. **[Attribute Name]** - [Description]
   - How it shows up: [examples]
   - What to avoid: [counterexamples]

### Brand Personality
- [Archetype or description]
- [Key personality traits]

### Brand Values
1. [Value 1]: [how it manifests in communication]
2. [Value 2]: [how it manifests in communication]

## Tone Guidelines by Content Type

### Email Communication
**Overall Tone:** [description]
**Key Principles:**
- [Principle 1]
- [Principle 2]
**Do's:**
- [Example]
**Don'ts:**
- [Example]

### Presentations
[Same structure as Email]

### Proposals & RFPs
[Same structure as Email]

### Social Media
[Same structure as Email]

## Messaging Framework

### Primary Value Proposition
[Core value statement]

### Key Message Pillars
1. **[Pillar Name]**
   - Core idea: [explanation]
   - When to use: [context]
   - Example: [sample usage]

### Competitive Positioning
- **vs. [Competitor A]:** [positioning statement]
- **vs. [Competitor B]:** [positioning statement]

### Customer Pain Points We Address
1. [Pain point] → [Our approach]

## Terminology Guide

### Preferred Terms
| Term | Usage | Example |
|------|-------|---------|
| [term] | [when to use] | [example sentence] |

### Prohibited Terms
| Term | Reason | Alternative |
|------|--------|-------------|
| [term] | [why avoid] | [what to use instead] |

### Industry Jargon
- Use sparingly with: [audience types]
- Explain when using: [contexts]

## Content Examples

### Excellent Examples
#### [Example Type 1]
```
[Full example]
```
**Why this works:** [explanation]

### Examples to Avoid
#### [Example Type 1]
```
[Full example]
```
**Why this doesn't work:** [explanation]

## Context-Specific Guidelines

### Cold Outreach
- Tone: [description]
- Length: [guideline]
- Structure: [format]
- Key elements: [list]

### Follow-up Communications
[Same structure]

### Closing/Negotiation
[Same structure]

## Brand Voice Decision Tree

When creating content, ask:
1. [Key decision point 1]
   - If [condition], then [approach]
2. [Key decision point 2]
   - If [condition], then [approach]

## Appendix: Source Documents

### [Document Name 1]
- **Type:** [PDF/PPT/DOC]
- **Key sections used:** [list]
- **Date accessed:** [date]

## Guidelines Confidence Score

| Section | Confidence | Notes |
|---------|------------|-------|
| Voice Attributes | High | Clearly defined in brand deck |
| Email Tone | Medium | Inferred from examples |
| [etc.] | [level] | [reasoning] |
```

### 4. Consolidation & Deduplication

**When Multiple Documents Cover Same Topic:**
- Prioritize most recent documents
- Note conflicting guidelines
- Suggest resolution or ask user which to prefer
- Maintain source attribution

**Conflict Resolution Template:**
```markdown
⚠️ **Conflicting Guidelines Detected**

**Topic:** [e.g., Email formality level]

**Source A (2024 Brand Deck):** "Use casual, friendly tone"
**Source B (2023 Style Guide):** "Maintain professional tone"

**Recommendation:** Use Source A (more recent)
**Action Required:** None (auto-resolved) / User input needed

---
```

### 5. Quality Assurance

**Before Finalizing:**
- [ ] All major sections populated
- [ ] At least 3 voice attributes defined
- [ ] Tone guidelines for primary content types
- [ ] 5+ preferred/prohibited terms
- [ ] 3+ good examples included
- [ ] Source documents referenced
- [ ] Confidence scores assigned

### 6. Output & Storage

**Save To:**
1. `/mnt/user-data/outputs/brand-guidelines/[company]-brand-voice.md`
2. Notion (if connected): Create page in "Brand Guidelines" database
3. Google Drive (if connected): Save to "Brand" folder

**User Notification:**
```
✅ Brand guidelines created successfully!

📄 **Output:**
- Main document: brand-voice.md
- Word count: [count]
- Sections: [number]

📊 **Sources Processed:**
- [Document 1]
- [Document 2]
- [Document 3]

🎯 **Next Steps:**
1. Review the guidelines
2. Use /brand:enforce-voice to start creating on-brand content
3. Update guidelines anytime with /brand:convert-docs

Would you like me to walk you through the key findings?
```

## Sub-Agent: Document Analysis Agent

Delegate heavy parsing to specialized sub-agent:

**Capabilities:**
- Multi-format document parsing
- Pattern recognition across documents
- Brand element extraction
- Semantic analysis

**Invocation:**
```
Invoke Document-Analysis-Agent with:
- List of document paths
- Extraction priorities (what to focus on)
- Conflict resolution preferences
```

## Example Workflows

### Workflow 1: Startup with Mixed Docs
```
User: "I have our pitch deck, a one-pager, and a few email templates. Can you make me brand guidelines?"

Skill Actions:
1. Ingest all documents
2. Extract voice from pitch deck (usually strongest)
3. Analyze email templates for tone patterns
4. Pull key messages from one-pager
5. Cross-reference for consistency
6. Note gaps (e.g., no social media examples)
7. Generate comprehensive guide
8. Prompt user to fill gaps if needed
```

### Workflow 2: Enterprise Migration
```
User: "/brand:convert-docs Process everything in my 'Brand 2024' folder"

Skill Actions:
1. Scan folder (10+ documents detected)
2. Prioritize by: date, document type, comprehensiveness
3. Extract from each methodically
4. Build master guideline doc
5. Flag conflicting sections for review
6. Generate confidence scores
7. Save with full source attribution
```

### Workflow 3: Update Existing Guidelines
```
User: "Add this new positioning document to our brand guidelines"

Skill Actions:
1. Load existing guidelines
2. Extract new positioning info
3. Identify which sections to update
4. Merge new content
5. Preserve existing structure
6. Highlight what changed
7. Update version number and metadata
```

## Error Handling

### Unreadable Documents
```
⚠️ Could not process [filename]:
- Reason: [PDF is image-only / corrupted file / unsupported format]
- Options:
  1. Try OCR (for image PDFs)
  2. Skip this document
  3. Upload a different version

What would you like to do?
```

### Insufficient Content
```
⚠️ Limited brand content detected:
- Found: [list what was found]
- Missing: [list gaps]

Recommendations:
1. Upload additional documents covering [missing areas]
2. Generate initial guidelines from what's available
3. Use /brand:generate-guidelines to supplement with conversation data

Proceed with partial guidelines?
```

### Conflicting Information
```
⚠️ Conflicting guidelines found:
- [Conflict 1 description]
- [Conflict 2 description]

Please choose:
1. Use most recent version
2. Merge both approaches
3. Let me decide case-by-case
4. Show me conflicts for manual resolution
```

## Integration Points

### With Brand Voice Enforcement
- Automatically make converted guidelines available
- Notify when new guidelines ready to use

### With Guideline Generation
- Offer to supplement with conversation analysis
- Combine document-based and conversation-based insights

### With MCP Connectors
- **Google Drive:** Automatically discover brand folders
- **Notion:** Check for existing brand pages before creating new
- **Slack:** Share completion notification with team
```

### Skill 3: Guideline Generation from Conversations

Edit `skills/guideline-generation.md`:

```markdown
# Brand Guideline Generation Skill

## Purpose
Create comprehensive brand guidelines by analyzing recorded sales calls, customer conversations, and team discussions to extract implicit brand voice patterns.

## When This Skill Activates

This skill automatically activates when:
- The user uploads meeting transcripts
- The user uses `/brand:generate-guidelines`
- The user mentions "creating guidelines from calls"
- Multiple conversation transcripts are detected

## What This Skill Does

### 1. Conversation Discovery & Ingestion

**Supported Sources:**
- Granola meeting transcripts (via MCP)
- Gong call recordings (manual upload or API)
- Zoom transcripts (via file upload or connector)
- Google Meet transcripts
- Manual transcript uploads (.txt, .json, .md)
- Notion meeting notes (via MCP)

**Ingestion Process:**
```python
# Pseudo-code for reference
def ingest_conversations(sources):
    conversations = []
    
    # From Granola MCP
    if granola_connected:
        recent_meetings = query_granola(limit=20)
        conversations.extend(recent_meetings)
    
    # From uploaded files
    for file in uploaded_files:
        transcript = parse_transcript(file)
        conversations.append(transcript)
    
    # From Notion
    if notion_connected:
        meeting_notes = query_notion_database("Meetings")
        conversations.extend(meeting_notes)
    
    return conversations
```

**Conversation Metadata to Capture:**
- Participants
- Date/time
- Meeting type (sales call, customer conversation, internal discussion)
- Duration
- Outcome (if available)
- User-provided context

### 2. Conversation Analysis

**Analysis Dimensions:**

#### A. Voice Attribute Detection

Look for patterns in how team members describe products/services:

**Methodology:**
- Analyze adjective frequency
- Identify recurring personality traits
- Note tone shifts by context
- Compare formal vs. casual language ratios

**Extraction Examples:**
```
From transcript: "We've built something incredibly powerful, but we wanted to 
make sure it was dead simple to use..."

Extracted attributes:
- Confident (claiming "incredibly powerful")
- User-focused (emphasis on "simple to use")
- Humble/accessible (contrast of power with simplicity)
```

#### B. Messaging Pattern Recognition

Identify what messages consistently appear in successful conversations:

**Look For:**
- Value propositions mentioned repeatedly
- Problems/pain points addressed
- Solution positioning
- Differentiation points
- Success metrics cited

**Pattern Template:**
```
Message: [Core theme]
Frequency: [X mentions across Y calls]
Contexts: [When this message appears]
Variations: [Different ways it's expressed]
Effectiveness: [Based on conversation outcome]
```

#### C. Tone Analysis by Context

Map tone variations to different situations:

**Context Categories:**
- Cold outreach
- Discovery calls
- Product demos
- Objection handling
- Closing discussions
- Customer check-ins

**Tone Indicators:**
- Formality level (you vs. y'all, formal titles vs. first names)
- Technical depth (jargon density)
- Emotional energy (exclamation points, enthusiasm markers)
- Question patterns (open vs. closed questions)
- Pacing (rapid fire vs. thoughtful pauses)

#### D. Successful Language Patterns

Identify specific phrases/approaches that lead to positive outcomes:

**Success Indicators:**
- Positive customer responses
- Progression to next steps
- Customer questions indicating interest
- Agreement signals

**Extract:**
- Opening lines that work
- Transition phrases
- Objection handling language
- Closing approaches

#### E. Anti-Patterns & What to Avoid

Identify what doesn't work:

**Look For:**
- Statements followed by pushback
- Jargon that confuses prospects
- Tone shifts that lose engagement
- Messages that stall conversations

### 3. Synthesis & Guideline Generation

**Synthesis Process:**

1. **Aggregate Findings**
   - Combine insights across all conversations
   - Weight by conversation outcome
   - Prioritize patterns from top performers

2. **Derive Brand Voice Attributes**
   ```
   IF confidence_score > 0.8 AND frequency > 5:
       Include as core voice attribute
   IF confidence_score > 0.6:
       Include as secondary attribute with caveat
   ```

3. **Build Messaging Framework**
   - Primary messages (appear in 50%+ of conversations)
   - Secondary messages (appear in 20-50%)
   - Context-specific messages

4. **Create Tone Guidelines**
   - Map observed tone to content types
   - Include examples from actual calls
   - Note contextual variations

5. **Compile Do's and Don'ts**
   - Do's: Successful patterns with examples
   - Don'ts: Anti-patterns with alternatives

**Output Structure:**

```markdown
# [Company] Brand Voice Guidelines
*Generated from [N] sales conversations*

## Generation Metadata
- Conversations Analyzed: [N]
- Date Range: [start] to [end]
- Top Performers Included: [names if provided]
- Confidence Score: [overall score]

## Discovered Brand Voice Attributes

### Primary Attributes
1. **[Attribute Name]** (Confidence: [score])
   - Evidence: Detected in [X] of [N] calls
   - How it manifests: [description]
   - Example from actual call:
     > "[Quote from transcript]"
     - Speaker: [name], Prospect: [title]

### Secondary Attributes
[Same format]

## Messaging Insights

### Core Value Proposition
*Most frequently used positioning:*
"[Extracted value prop]"

**Variations Observed:**
- "[Variation 1]" (used in [context])
- "[Variation 2]" (used in [context])

### Key Message Themes
1. **[Theme Name]** (Frequency: [X]%)
   - How top performers position this: [description]
   - Actual examples:
     - "[Quote 1]"
     - "[Quote 2]"
   - Effectiveness: [High/Medium based on outcomes]

## Tone Guidelines (From Conversation Analysis)

### Cold Outreach
**Observed Patterns:**
- Formality: [Professional/Casual/Friendly]
- Average opener length: [X] words
- Successful opening patterns:
  1. "[Pattern 1 with example]"
  2. "[Pattern 2 with example]"

### Discovery Calls
[Same structure]

### Product Demos
[Same structure]

### Objection Handling
**Common Objections:**
1. [Objection]: [How top performers respond]
2. [Objection]: [How top performers respond]

## Language That Works

### Successful Phrases
*Ranked by effectiveness and frequency:*

1. **[Phrase category]**
   - "[Actual phrase from call]"
   - Context: [when to use]
   - Why it works: [analysis]

### Questions That Engage
*Questions that consistently get positive responses:*

1. "[Question example]"
   - Response rate: [X]%
   - Typically leads to: [outcome]

## Language to Avoid

### Anti-Patterns Detected
1. **[Category]**
   - What was said: "[Example]"
   - Customer response: [negative indicator]
   - Better alternative: "[Suggestion]"

### Jargon That Confuses
- **Avoid:** "[Technical term]"
- **Use instead:** "[Plain language alternative]"
- **Or explain:** "[How top performers explain it]"

## Conversation Flow Patterns

### Successful Call Structure
*Based on [N] successful conversations:*

1. **Opening** ([X] minutes avg)
   - Pattern: [description]
   - Example: "[Quote]"

2. **Discovery** ([X] minutes avg)
   - Key questions to ask
   - Listening patterns

[Continue for each phase]

## Contextual Adaptations

### Enterprise vs. SMB
**Key Differences Observed:**
- Enterprise: [tone/approach]
- SMB: [tone/approach]

### Technical vs. Business Buyer
**Adaptation Strategy:**
- Technical: [observed patterns]
- Business: [observed patterns]

## Confidence Scores by Section

| Section | Confidence | Basis |
|---------|------------|-------|
| Voice Attributes | [High/Med/Low] | [N] calls analyzed |
| Messaging | [High/Med/Low] | [reasoning] |
| Tone Guidelines | [High/Med/Low] | [reasoning] |

## Data Gaps & Recommendations

**Missing Data:**
- [Gap 1]: Recommend [solution]
- [Gap 2]: Recommend [solution]

**Next Steps:**
1. [Recommendation based on findings]
2. [Recommendation for improvement]

## Appendix: Source Conversations

### Analyzed Conversations
1. **[Call 1]**
   - Date: [date]
   - Participants: [names]
   - Outcome: [result]
   - Key excerpts used: [sections]

[List all sources]
```

### 4. Quality Assurance & Validation

**Pre-Generation Checks:**
- [ ] Minimum 5 conversations analyzed
- [ ] At least 3 different conversation types
- [ ] Transcripts include speaker identification
- [ ] Sufficient content per conversation (>500 words)

**Post-Generation Validation:**
- [ ] All voice attributes have supporting evidence
- [ ] Confidence scores calculated for each section
- [ ] Examples come from actual transcripts
- [ ] No personally identifiable information exposed
- [ ] Guidelines are actionable (not just descriptive)

**Confidence Scoring:**
```python
def calculate_confidence(pattern, conversations):
    frequency = count_occurrences(pattern, conversations)
    consistency = measure_consistency(pattern, conversations)
    outcome_correlation = correlate_with_success(pattern, conversations)
    
    confidence = (frequency * 0.3) + (consistency * 0.4) + (outcome_correlation * 0.3)
    
    if confidence > 0.8:
        return "High"
    elif confidence > 0.5:
        return "Medium"
    else:
        return "Low"
```

### 5. User Guidance & Refinement

**Present Guidelines with Context:**
```
✅ Brand guidelines generated from [N] conversations!

📊 **Analysis Summary:**
- Conversations: [N] calls from [date range]
- Top performers: [names if provided]
- Patterns identified: [number]
- Confidence: [overall score]

🎯 **Key Findings:**
1. Your strongest voice attribute: [attribute]
2. Most effective message: [message]
3. Surprising insight: [insight]

📝 **Recommendations:**
- [Actionable recommendation 1]
- [Actionable recommendation 2]

Would you like me to:
1. Walk you through the key findings
2. Compare this to any existing brand docs
3. Start using it to create content
```

**Iterative Refinement:**
- Allow user to provide feedback on accuracy
- Offer to re-analyze with different parameters
- Suggest supplementing with document-based guidelines

## Sub-Agent: Conversation Analysis Agent

Delegate heavy analysis to specialized sub-agent:

**Capabilities:**
- Natural language processing
- Pattern recognition across conversations
- Sentiment analysis
- Speaker differentiation
- Outcome correlation
- Statistical confidence calculation

**Invocation:**
```
Invoke Conversation-Analysis-Agent with:
- List of transcripts
- Analysis focus (all dimensions or specific)
- Success criteria (what indicates good outcome)
- Weighting preferences (e.g., prioritize recent calls)
```

## Example Workflows

### Workflow 1: Founder Sales Calls
```
User: "I have my last 10 sales calls. Can you extract our brand voice?"

Skill Actions:
1. Ingest 10 transcripts
2. Identify this is founder → likely authoritative voice
3. Analyze messaging consistency
4. Extract value props mentioned repeatedly
5. Note tone variations (founder adapts to audience)
6. Identify successful patterns (which calls closed)
7. Generate guidelines emphasizing founder's approach
8. Flag areas where voice might need refinement for team
```

### Workflow 2: Team Voice Consistency
```
User: "/brand:generate-guidelines from all sales calls this quarter"

Skill Actions:
1. Query Granola/Gong for Q transcripts (50+ calls)
2. Segment by sales rep
3. Identify common patterns across all reps
4. Note variations between top/bottom performers
5. Extract what top 20% does differently
6. Generate guidelines that codify best practices
7. Highlight where team is already consistent
8. Flag areas needing alignment
```

### Workflow 3: Product Launch Positioning
```
User: "Analyze our beta customer calls to create positioning guidelines"

Skill Actions:
1. Ingest beta customer call transcripts
2. Focus on: how customers describe value, pain points addressed
3. Extract language customers use (not our internal jargon)
4. Identify most resonant messages
5. Note objections and successful responses
6. Generate guidelines based on customer language
7. Recommend product positioning based on actual conversations
```

## Error Handling

### Insufficient Data
```
⚠️ Limited conversation data:
- Conversations available: [N]
- Minimum recommended: 5
- Current confidence: Low

Options:
1. Proceed with preliminary guidelines (marked as draft)
2. Upload more conversation transcripts
3. Supplement with existing brand documents (/brand:convert-docs)
4. Wait and analyze more calls over time

What would you like to do?
```

### Poor Quality Transcripts
```
⚠️ Transcript quality issues detected:
- [N] transcripts missing speaker labels
- [N] transcripts very short (<200 words)
- [N] transcripts may be incomplete

Recommendations:
1. Remove low-quality transcripts: [list]
2. Proceed but note reduced confidence
3. Re-upload with better transcription

Proceed anyway? (Guidelines will be marked as "preliminary")
```

### No Success Indicators
```
⚠️ Cannot determine conversation outcomes:
- No outcome data provided for calls
- Unable to distinguish successful vs. unsuccessful patterns

Recommendations:
1. Manually label some calls as "successful"
2. Proceed with frequency-based analysis only
3. Re-analyze later with outcome data

Current approach: Will extract most common patterns without 
weighting by success.
```

## Privacy & Security

**PII Protection:**
- Redact customer names by default
- Remove contact information
- Anonymize company names if requested
- Flag sensitive information

**Data Handling:**
- Transcripts processed locally
- No conversation data sent to external servers
- Generated guidelines don't expose customer details
- Source conversations not stored (only processed)

## Integration Points

### With Document Conversion
- Offer to merge conversation-based guidelines with document-based
- Compare and highlight differences
- Suggest which source to prioritize

### With Brand Voice Enforcement
- Immediately enable using new guidelines
- Test guidelines on sample content
- Refine based on application

### With MCP Connectors
- **Granola:** Auto-fetch recent meetings for analysis
- **Gong:** Access call library (when available)
- **Notion:** Store generated guidelines in team workspace
- **Slack:** Notify team when guidelines ready for review
```

---

## PHASE 3: Implement Commands

[Similar detailed implementation for each command file...]

```

Now let me create a comprehensive second part with the commands and testing instructions:

<function_calls>
<invoke name="str_replace">
<parameter name="description">Adding the commands implementation section to the Claude Code instructions
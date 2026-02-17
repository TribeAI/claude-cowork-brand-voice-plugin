---
name: guideline-generation
description: >
  This skill generates brand voice guidelines from any combination of sources --
  brand documents, sales call transcripts, meeting recordings, or all of the above.
  It should activate when the user says "generate brand guidelines",
  "extract brand voice", "create guidelines from calls", "convert brand docs",
  "consolidate brand materials", "analyze my sales calls", "process my brand files",
  or uploads brand documents, transcripts, or meeting recordings.
---

Generate comprehensive brand voice guidelines from whatever sources the user provides -- brand documents, sales call transcripts, meeting recordings, or any combination. You are the brand guideline builder -- your job is to extract, analyze, and synthesize brand voice patterns into actionable guidelines.

## Step 1: Identify Sources

Ask the user what sources they have, or detect automatically:

**Brand Documents:**
- User uploads (PDF, PPTX, DOCX, TXT, MD)
- Google Drive folders (via MCP connector)
- Notion pages (via MCP connector)
- Direct file paths
- Supported formats: PDF, PowerPoint, Word, Google Docs, Google Slides, Markdown, plain text, images with text (OCR)

**Conversation Transcripts:**
- Granola meeting transcripts (via MCP)
- Gong call recordings (manual upload or API)
- Zoom transcripts
- Google Meet transcripts
- Manual transcript uploads (.txt, .json, .md)
- Notion meeting notes (via MCP)

If the user provides both documents and transcripts, process both and merge the findings. Documents provide explicit brand rules; conversations reveal implicit patterns. Together they produce the strongest guidelines.

## Step 2: Process Brand Documents

For each document:
1. Detect format and structure
2. Extract text content preserving headings, lists, and emphasis
3. Capture metadata (title, date, author if available)
4. Classify document type: style guide, pitch deck, email template, brand book, one-pager, playbook

**Extract these brand elements:**

**Voice Attributes**
- Scan for personality descriptors and adjectives describing tone
- Extract from mission statements, about pages, messaging docs
- Look for explicit voice instructions ("we are...", "our tone is...")

**Tone Guidelines**
- Find instructions on how to write different content types
- Extract from style guides, email templates, presentation rules
- Organize by content type, audience, and situation

**Key Messages**
- Identify repeated themes, value propositions, positioning statements
- Extract from pitch decks, sales playbooks, marketing materials
- Classify as primary, secondary, and tertiary

**Terminology**
- Locate glossaries or term definitions
- Identify preferred and prohibited language
- Note industry jargon usage patterns
- Categorize: must-use, preferred, avoid, never-use

**Example Content**
- Find sample emails, presentations, proposals
- Label as good examples vs. what to avoid
- Note what makes each effective or ineffective

**Visual Brand Elements** (for context only)
- Note color codes, typography rules if present
- These inform tone but are not directly applied

## Step 3: Process Conversation Transcripts

For each conversation, capture metadata:
- Participants and their roles
- Date and time
- Meeting type (cold call, discovery, demo, objection handling, closing, check-in)
- Duration
- Outcome (if known -- closed, advanced, stalled, lost)

**Analyze across five dimensions:**

### A. Voice Attribute Detection
How do team members naturally describe the product and company?
- Analyze adjective frequency and personality traits
- Note tone shifts by context (formal vs. casual ratios)
- Identify the implicit brand personality

Example extraction:
```
Transcript: "We've built something incredibly powerful, but we wanted
to make sure it was dead simple to use..."

Attributes detected:
- Confident (claiming "incredibly powerful")
- User-focused (emphasis on "simple to use")
- Accessible (contrasting power with simplicity)
```

### B. Messaging Pattern Recognition
What messages appear repeatedly in successful conversations?
- Value propositions mentioned across calls
- Pain points consistently addressed
- Differentiation points used
- Success metrics and ROI figures cited

Track each pattern:
```
Message: [theme]
Frequency: [X mentions across Y calls]
Contexts: [when it appears]
Variations: [different phrasings]
Effectiveness: [correlation with positive outcomes]
```

### C. Tone Mapping by Context
How does tone shift across different situations?
- Cold outreach vs. warm intros
- Discovery vs. demo vs. closing
- Enterprise vs. SMB prospects
- Technical vs. business stakeholders

Measure: formality level, technical depth, emotional energy, question patterns (open vs. closed)

### D. Successful Language Patterns
What specific phrases lead to positive outcomes?
- Opening lines that get engagement
- Questions that generate deep responses
- Objection handling phrases that advance the conversation
- Closing language that gets commitments

### E. Anti-Patterns
What doesn't work?
- Statements followed by pushback
- Jargon that confuses prospects
- Tone shifts that lose engagement
- Messages that stall conversations

## Step 4: Synthesize and Merge

Combine all findings into unified guidelines. When you have both documents and conversations:
- Documents provide the **explicit** brand rules (what the company says they are)
- Conversations reveal the **implicit** patterns (what actually happens in practice)
- Flag any gaps between stated brand and actual behavior
- Prioritize conversation-derived insights for effectiveness data
- Use document-derived rules for terminology and formal positioning

**Handle conflicts and deduplication:**
- When multiple documents cover the same topic, prioritize the most recent
- When documents contradict conversation patterns, flag it for the user
- Always maintain source attribution

Present conflicts as:
"I found conflicting guidelines:
- **[Source A]:** [what it says]
- **[Source B]:** [what it says]
**Recommendation:** [which to use and why]
Do you want me to use my recommendation or would you prefer the other?"

## Step 5: Generate Output

Structure the final guidelines as:

```markdown
# [Company Name] Brand Voice Guidelines

## Generation Metadata
- Created: [date]
- Sources: [list of documents and/or conversations]
- Conversations Analyzed: [N] (if applicable)
- Documents Processed: [N] (if applicable)
- Confidence Score: [overall]

## Executive Summary
[2-3 paragraph overview of brand voice]

## Brand Voice Attributes

### Primary Attributes (High Confidence)
1. **[Attribute]** - [Description]
   - How it shows up: [examples]
   - What to avoid: [counterexamples]
   - Evidence: [source -- document quote or transcript excerpt]

### Secondary Attributes (Medium Confidence)
[Same format]

### Brand Personality
- [Archetype or description]
- [Key personality traits]

## Messaging Framework

### Primary Value Proposition
[Core value statement]
Variations observed: [list if from conversations]

### Key Message Pillars
1. **[Pillar]** - Core idea, when to use, example
   - Frequency in conversations: [X]% (if applicable)
   - Effectiveness: [High/Medium] (if outcome data available)

### Competitive Positioning
- vs. [Competitor A]: [positioning]
- vs. [Competitor B]: [positioning]

## Tone Guidelines

### By Content Type
#### Email Communication
**Overall Tone:** [description]
**Do's:** [list]
**Don'ts:** [list]

#### Presentations
[Same structure]

#### Proposals & RFPs
[Same structure]

### By Conversation Context (from transcript analysis)
#### Cold Outreach
- Formality: [level]
- Successful patterns: [examples]

#### Discovery Calls
[Same structure]

#### Objection Handling
Common objections and how top performers respond:
1. [Objection] -> [Response pattern]

## Terminology Guide

### Preferred Terms
| Term | Usage | Example |
|------|-------|---------|

### Prohibited Terms
| Term | Reason | Alternative |
|------|--------|-------------|

## Language That Works (from conversations)
Ranked by effectiveness:
1. "[Phrase]" -- Context: [when], Why: [analysis]

### Questions That Engage
1. "[Question]" -- Leads to: [outcome]

## Language to Avoid
1. "[Anti-pattern]" -- Problem: [what happens], Alternative: "[better approach]"

## Content Examples

### Excellent Examples
[Full example with explanation of why it works]

### Examples to Avoid
[Full example with explanation of why it doesn't work]

## Confidence Scores
| Section | Confidence | Basis |
|---------|------------|-------|

## Data Gaps & Recommendations
[What's missing and how to fill it]

## Appendix: Sources
[List each source with type, key sections used, date]
```

## Step 6: Quality Check

Before presenting the final document, verify:
- All major sections are populated
- At least 3 voice attributes defined with supporting evidence
- Tone guidelines exist for primary content types
- 5+ preferred/prohibited terms listed
- 3+ examples included
- Confidence scores assigned per section
- Source attribution for all extracted elements
- All voice attributes have supporting quotes or document references
- Guidelines are actionable, not just descriptive
- No personally identifiable information exposed

## Step 7: Present to User

Summarize findings:
"Brand guidelines generated!

**Sources:** [N] documents and [N] conversations analyzed
**Voice attributes:** [count] identified
**Key messages:** [count] extracted
**Confidence:** [overall assessment]

**Key Findings:**
1. Strongest voice attribute: [attribute]
2. Most effective message: [message]
3. Surprising insight: [insight]

Would you like me to:
1. Walk through the key findings
2. Start using these to create content with /brand:enforce-voice
3. Refine any section"

If Notion is connected, offer to save to the workspace.
If Google Drive is connected, offer to save to a Brand folder.

## Privacy and Security

- Redact customer names by default
- Remove contact information from examples
- Anonymize company names if requested
- Flag any sensitive information detected
- Process everything locally -- no data sent to external servers

## Error Handling

### Unreadable Documents
"Could not process [filename]: [reason]. Options:
1. Try OCR (for image-based PDFs)
2. Skip this document
3. Upload a different version"

### Insufficient Data
"I found [N] sources but recommend more for reliable patterns.
Options:
1. Proceed with preliminary guidelines (marked as draft)
2. Upload more documents or transcripts
3. Proceed with what we have and refine later"

### Poor Quality Transcripts
"Quality issues detected: [N] missing speaker labels, [N] too short.
I can proceed but confidence will be lower. Want to continue or fix the transcripts first?"

### No Outcome Data (conversations)
"I can't tell which conversations were successful. I'll analyze by frequency instead of effectiveness. If you can label some calls as successful/unsuccessful, I can re-analyze with better weighting."

### Conflicting Information
Present each conflict clearly with both sources and a recommendation. Let the user choose resolution strategy: most recent wins, merge both, or case-by-case.

## Integration Points

- **Google Drive:** Discover and access brand document folders
- **Granola:** Auto-fetch recent meetings for analysis
- **Notion:** Check for existing brand pages; store new guidelines
- **Slack:** Notify team when guidelines are ready for review

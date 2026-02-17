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

---
name: guideline-generation
description: >
  This skill should be used when the user asks to "generate brand guidelines",
  "create brand guidelines", "extract brand voice", "create guidelines from calls",
  "consolidate brand materials", "analyze my sales calls for brand voice",
  "process my brand files", "build brand guidelines from documents",
  "create a brand voice document", or uploads brand documents, transcripts,
  or meeting recordings for brand analysis. Also triggers when the user has a
  discovery report and wants to synthesize it into actionable guidelines.
---

# Guideline Generation

Generate comprehensive, LLM-ready brand voice guidelines from any combination of sources — brand documents, sales call transcripts, discovery reports, or direct user input. Transform raw materials into structured, enforceable guidelines with confidence scoring and open questions.

## Inputs

Accept any combination of:
- **Discovery report** from the brand-discovery skill (structured, pre-triaged)
- **Brand documents** uploaded or from connected platforms (PDF, PPTX, DOCX, MD, TXT)
- **Conversation transcripts** from Gong, manual uploads, or Notion meeting notes
- **Direct user input** about their brand voice and values

When a discovery report is provided, use it as the primary input — sources are already triaged and ranked. Supplement with additional analysis as needed.

## Generation Workflow

### 1. Identify and Classify Sources

Determine what the user has provided. If no sources are available:
- Check if a discovery report exists from a previous `/brand-voice:discover-brand` run
- Check `.claude/brand-voice.local.md` for known brand material locations
- Suggest running discovery first: `/brand-voice:discover-brand`

### 2. Process Sources

**For documents:** Delegate to the document-analysis agent for heavy parsing. Extract voice attributes, messaging themes, terminology, tone guidance, and examples.

**For transcripts:** Delegate to the conversation-analysis agent for pattern recognition. Extract implicit voice attributes, successful language patterns, tone by context, and anti-patterns.

**For discovery reports:** Extract pre-triaged sources, conflicts, and gaps. Use the ranked sources directly.

### 3. Synthesize Into Guidelines

Merge all findings into a unified guideline document following the template in `references/guideline-template.md`. Key sections:

**"We Are / We Are Not" Table** — The core brand identity anchor:

| We Are | We Are Not |
|--------|------------|
| [Attribute — e.g., "Confident"] | [Counter — e.g., "Arrogant"] |
| [Attribute — e.g., "Approachable"] | [Counter — e.g., "Casual or sloppy"] |

Derive attributes from the most consistent patterns across sources. Each row should have supporting evidence.

**Voice Constants vs. Tone Flexes** — Clarify what stays fixed and what adapts:
- **Voice** = personality, values, "We Are / We Are Not" — constant across all content
- **Tone** = formality, energy, technical depth — flexes by context

**Tone-by-Context Matrix:**

| Context | Formality | Energy | Technical Depth | Example |
|---------|-----------|--------|-----------------|---------|
| Cold outreach | Medium | High | Low | "[example phrase]" |
| Enterprise proposal | High | Medium | High | "[example phrase]" |
| Social media | Low | High | Low | "[example phrase]" |

### 4. Assign Confidence Scores

Score each section using the methodology in `references/confidence-scoring.md`:
- **High confidence**: 3+ corroborating sources, explicit guidance found
- **Medium confidence**: 1-2 sources, or inferred from patterns
- **Low confidence**: Single source, inferred, or conflicting data

### 5. Surface Open Questions

Generate open questions for any ambiguity that cannot be resolved:

```markdown
## Open Questions for Team Discussion

### High Priority (blocks guideline completion)
1. **[Question Title]**
   - What was found: [conflicting or incomplete info]
   - Agent recommendation: [suggested resolution with reasoning]
   - Need from you: [specific decision or confirmation needed]
```

Every open question MUST include an agent recommendation. Turn ambiguity into "confirm or override" — never a dead end.

### 6. Quality Check

Before presenting, verify via the quality-assurance agent:
- All major sections populated
- At least 3 voice attributes with evidence
- "We Are / We Are Not" table has 4+ rows
- Tone matrix covers at least 3 contexts
- Confidence scores assigned per section
- Source attribution for all extracted elements
- No PII exposed
- Open questions include recommendations

### 7. Present and Offer Next Steps

Summarize key findings:
- Total sections generated with confidence breakdown
- Strongest voice attribute and most effective message
- Number of open questions (if any)

### 8. Save for Future Sessions

Immediately after presenting, prompt the user to save so guidelines persist across sessions:

"Where should I save these guidelines so they're available in future sessions?
1. **Notion** — I'll create a page titled 'Brand Voice Guidelines' in your workspace
2. **Google Drive** — I'll save a file named 'Brand Voice Guidelines' to your Drive
3. **Local file** — I'll save to `.claude/brand-voice-guidelines.md` in this project
4. **Skip** — Don't save (guidelines will only be available in this session)"

**When saving to Notion:**
- Create or update a page titled exactly **"Brand Voice Guidelines"** in the user's connected workspace. This exact title is required so the enforcement skill can find it later via search.
- Confirm success: "Guidelines saved to Notion. You can now use `/brand-voice:enforce-voice` in any session and it will automatically load these guidelines."

**When saving to Google Drive:**
- Create or update a file named exactly **"Brand Voice Guidelines"** in the user's Drive. Same naming convention for discovery.
- Confirm success: "Guidelines saved to Google Drive. The enforcement skill will find them automatically in future sessions."

**When saving locally:**
- Write the full guidelines to `.claude/brand-voice-guidelines.md` in the project root.
- Confirm success: "Guidelines saved locally. The enforcement skill will pick them up automatically in this project."

**If save fails** (service not connected, permissions issue, etc.):
- Tell the user what went wrong
- Suggest an alternative save method
- Remind them the guidelines are still available in the current session since they're in conversation context

After saving (or skipping), offer:
1. Walk through the guidelines section by section
2. Start creating content with `/brand-voice:enforce-voice`
3. Resolve open questions

## Privacy and Security

- Redact customer names and contact information from all examples
- Anonymize company names in transcript excerpts if requested
- Flag any sensitive information detected during processing

## Additional Resources

### Reference Files

For detailed output templates and scoring methodology, consult:

- **`references/guideline-template.md`** — Complete output template with all sections, field definitions, and formatting guidance
- **`references/confidence-scoring.md`** — Confidence scoring methodology, thresholds, and examples

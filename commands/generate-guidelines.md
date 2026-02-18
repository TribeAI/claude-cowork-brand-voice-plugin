---
description: Generate brand voice guidelines from documents, transcripts, discovery reports, or any combination
argument-hint: "<sources — documents, transcripts, or description of what you have>"
---

Generate comprehensive, LLM-ready brand voice guidelines from whatever sources the user provides — brand documents, conversation transcripts, a discovery report from `/brand-voice:discover-brand`, or direct input.

Process the sources specified in $ARGUMENTS. If none specified, check:
1. Whether a discovery report was generated in this session
2. `.claude/brand-voice.local.md` for known brand material locations
3. Connected platforms (Notion, Confluence, Google Drive, Box, SharePoint, Gong) for existing materials
4. If nothing is available, suggest running `/brand-voice:discover-brand` first

Follow the guideline-generation skill instructions to:
1. Identify and classify all available sources (discovery report, documents, transcripts)
2. Delegate to document-analysis and conversation-analysis agents as needed
3. Synthesize findings into unified guidelines with "We Are / We Are Not" table and tone-by-context matrix
4. Assign confidence scores per section
5. Surface open questions with agent recommendations for any ambiguity
6. Present key findings and offer next steps
7. Prompt to save guidelines for future sessions (Notion, Google Drive, Box, local file, or skip)
   If guidelines already exist at the save destination, archive the previous version before saving (see guideline-generation skill step 8 for archive naming conventions).

After generation, the skill will prompt to save the guidelines so `/brand-voice:enforce-voice` can automatically find them in future sessions.

Supported document formats: PDF, PowerPoint, Word, Markdown, plain text.
Supported transcript sources: Gong (MCP), Granola (MCP), Notion meeting notes, manual uploads.

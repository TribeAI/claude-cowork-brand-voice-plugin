---
description: Generate brand voice guidelines from documents, transcripts, discovery reports, or any combination
argument-hint: "<sources — documents, transcripts, or description of what you have>"
---

**Before doing anything else**, check whether the user has a working folder selected for this session. If there is no working folder, warn the user: "Heads up — you don't have a working folder selected. I can still generate guidelines, but I won't be able to save them to a file, so they'll only be available in this conversation. To persist guidelines between sessions, select a working folder and re-run this command."

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
7. Ask the user for their project path, then save guidelines to `<project-root>/.claude/brand-voice-guidelines.md` (archiving any existing file first). Do NOT use relative paths — the agent's working directory may not be the user's project.

After generation, guidelines are saved locally so `/brand-voice:enforce-voice` can automatically find them in future sessions.

Supported document formats: PDF, PowerPoint, Word, Markdown, plain text.
Supported transcript sources: Gong (MCP), Granola (MCP), Notion meeting notes, manual uploads.

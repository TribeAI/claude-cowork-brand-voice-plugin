---
description: Generate brand guidelines from documents, transcripts, or both
argument-hint: "<sources - documents, transcripts, or description>"
---

Generate comprehensive brand voice guidelines from whatever sources the user provides. This handles both brand documents (PDFs, pitch decks, style guides) and conversation transcripts (sales calls, meeting recordings) -- or any combination of both.

Process the sources specified in $ARGUMENTS, or if none specified, ask the user what they have available. Check connected services (Granola, Notion, Google Drive) for existing materials.

Follow the guideline-generation skill instructions to:
1. Identify all available sources (documents, transcripts, or both)
2. Process brand documents: extract voice attributes, tone, messaging, terminology, examples
3. Process conversation transcripts: analyze voice patterns, messaging effectiveness, tone by context, success/anti-patterns
4. Merge and synthesize findings from all sources into unified guidelines
5. Handle conflicts and deduplication across sources
6. Assign confidence scores based on data quality and consistency
7. Present key findings, surprising insights, and recommendations
8. Offer to save to Notion or Google Drive if connected

Supported document formats: PDF, PowerPoint, Word, Google Docs, Google Slides, Markdown, plain text, images with text (OCR).
Supported transcript sources: Granola (MCP), Gong, Zoom, Google Meet, Notion meeting notes, manual uploads.

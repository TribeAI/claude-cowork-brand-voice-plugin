---
description: Search connected platforms for brand materials and produce a discovery report
argument-hint: "[company name or platforms to search]"
---

Discover brand materials across the user's connected enterprise platforms. Search Notion, Confluence, Google Drive, Figma, and Gong for brand guidelines, style guides, messaging frameworks, templates, and conversation transcripts.

If $ARGUMENTS includes a company name, use it for targeted searches. If platforms are specified, limit search to those platforms.

Follow the brand-discovery skill instructions to:
1. Check `.claude/brand-voice.local.md` for settings (company name, enabled platforms, search depth)
2. Briefly confirm scope with the user (which platforms, include transcripts?)
3. Delegate to the brand-discovery agent for autonomous 4-phase search
4. Present the structured discovery report with sources, brand elements, conflicts, and open questions
5. Offer next steps: generate guidelines, resolve open questions, save report, or expand search

If no platforms are connected, inform the user which MCP servers the plugin supports (Notion, Atlassian Confluence, Google Drive, Figma, Gong) and how to connect them.

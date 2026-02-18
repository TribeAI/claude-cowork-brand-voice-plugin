---
name: brand-discovery
description: >
  This skill orchestrates autonomous discovery of brand materials across enterprise
  platforms (Notion, Confluence, Google Drive, Box, SharePoint, Figma, Gong, Slack).
  It should be used when the user asks to "discover brand materials",
  "find brand documents", "search for brand guidelines", "audit brand content",
  "what brand materials do we have", "find our style guide", "where are our brand docs",
  "do we have a style guide", "discover brand voice", "brand content audit",
  or "find brand assets".
---

# Brand Discovery

Orchestrate autonomous discovery of brand materials across enterprise platforms. This skill coordinates the brand-discovery agent to search connected platforms (Notion, Confluence, Google Drive, Box, Microsoft 365, Figma, Gong, Slack), triage sources, and produce a structured discovery report with open questions.

## Discovery Workflow

### 1. Check Settings

Read `.claude/brand-voice.local.md` if it exists. Extract:
- Company name
- Which platforms are enabled (notion, confluence, google-drive, box, microsoft-365, figma, gong, slack)
- Search depth preference (standard or deep)
- Max sources limit
- Any known brand material locations listed under "Known Brand Materials"

If no settings file exists, proceed with all connected platforms and standard search depth.

### 2. Confirm Scope with User

Before launching discovery, confirm:
- Which platforms to search (default: all connected)
- Whether to include conversation transcripts (Gong) or just documents
- Any known locations to prioritize

Keep this brief — one question, not a questionnaire.

### 3. Delegate to Brand Discovery Agent

Launch the brand-discovery agent via the Task tool. Provide:
- Company name (from settings or user input)
- Enabled platforms
- Search depth
- Any known URLs or locations to check first

The agent executes the 4-phase discovery algorithm autonomously:
1. **Broad Discovery** — parallel searches across platforms
2. **Source Triage** — categorize and rank sources
3. **Deep Fetch** — retrieve and extract from top sources
4. **Discovery Report** — structured output with open questions

### 4. Present Discovery Report

When the agent returns, present the report to the user with a summary:
- Total sources found and analyzed
- Key brand elements discovered
- Any conflicts between sources
- Open questions requiring team input

### 5. Offer Next Steps

After presenting the report, offer:
1. **Generate guidelines now** — chain to `/brand-voice:generate-guidelines` using discovery report as input
2. **Resolve open questions first** — work through high-priority questions before generating
3. **Save report** — store the discovery report to Notion or as a local file
4. **Expand search** — search additional platforms or deeper if coverage is low

## Open Questions

Open questions arise when the discovery agent encounters ambiguity it cannot resolve:
- Conflicting documents (e.g., 2023 style guide vs. 2024 brand update)
- Missing critical sections (e.g., no social media guidelines found)
- Inconsistent terminology across platforms

Every open question includes an agent recommendation. Present questions as "confirm or override" — not dead ends.

## Integration with Other Skills

- **Guideline Generation**: The discovery report is returned by the brand-discovery agent via the Task tool. Pass it directly to the guideline-generation skill as structured input, replacing the need for users to manually gather sources.
- **Brand Voice Enforcement**: Once guidelines are generated from discovery, enforcement uses them automatically.

## Error Handling

- If zero platforms are connected, inform the user which platforms the plugin supports and how to connect them.
- If all searches return empty results, flag the discovery as "low coverage" and suggest the user provide documents manually or check platform connections.
- If a platform is connected but returns permission errors, note the gap and continue with other platforms.

## Reference Files

For detailed discovery patterns and algorithms, consult:

- **`references/search-strategies.md`** — Platform-specific search queries, query patterns by platform, and tips for maximizing discovery coverage
- **`references/source-ranking.md`** — Source category definitions, ranking algorithm weights, and triage decision criteria

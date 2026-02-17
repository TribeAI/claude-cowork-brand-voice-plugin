---
name: brand-discovery
description: >
  This skill should be used when the user asks to "discover brand materials",
  "find brand documents", "search for brand guidelines", "audit brand content",
  "what brand materials do we have", "find our style guide", "search Notion for brand",
  "search Confluence for brand", or wants to locate scattered brand assets across
  enterprise platforms before generating guidelines. Also triggers on
  "discover brand voice", "brand content audit", or "find brand assets".
---

# Brand Discovery

Orchestrate autonomous discovery of brand materials across enterprise platforms. This skill coordinates the brand-discovery agent to search connected platforms (Notion, Confluence, Google Drive, Figma, Gong), triage sources, and produce a structured discovery report with open questions.

## When to Use

Activate when the user needs to find brand materials before generating guidelines, wants a comprehensive audit of existing brand content, or doesn't know where brand documents live. This is typically the first step before guideline generation.

## Discovery Workflow

### 1. Check Settings

Read `.claude/brand-voice.local.md` if it exists. Extract:
- Company name
- Which platforms are enabled (notion, confluence, google-drive, figma, gong)
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

Refer to `references/search-strategies.md` for platform-specific search patterns and `references/source-ranking.md` for the ranking algorithm and category definitions.

## Integration with Other Skills

- **Guideline Generation**: Discovery report feeds directly into the guideline-generation skill as structured input, replacing the need for users to manually gather sources.
- **Brand Voice Enforcement**: Once guidelines are generated from discovery, enforcement uses them automatically.

## Additional Resources

### Reference Files

For detailed discovery patterns and algorithms, consult:

- **`references/search-strategies.md`** — Platform-specific search queries, query patterns by platform, and tips for maximizing discovery coverage
- **`references/source-ranking.md`** — Source category definitions, ranking algorithm weights, and triage decision criteria

# Brand Voice Plugin for Claude Cowork

## The Problem: Your Brand Lives Everywhere and Nowhere

The brand knowledge that makes a company recognizable rarely lives anywhere useful. It's in a deck from 2022, a Confluence page that hasn't been touched since the last rebrand, and the instincts of a few senior people who've been there long enough to just know. AI didn't create this problem. It made it urgent.

We see what happens next across almost every enterprise we work with. Content volume doubles, then triples. Sales reps are generating outreach. New hires are writing blog posts in their first week. Everyone is moving faster. And somewhere in that acceleration, the thing that made the brand recognizable starts to blur -- a slightly off tone here, a positioning inconsistency there. Not enough to flag on any single piece. Enough to matter across thousands. By the time most teams notice, it's already in front of prospects, investors, and customers.

## What Brand Voice Does

Brand Voice is a Tribe plugin for Claude Cowork that transforms scattered brand materials into enforceable AI guardrails. It works across three core workflows:

**Brand Discovery:** Your brand knowledge is buried across Notion, Confluence, Google Drive, Gong, Slack, and years of sales calls and meeting transcripts. Brand Voice searches across all of it to distill your strongest brand signals into a single, current source of truth -- grounded in how your best people communicate, not just how a style guide written three years ago says you should.

**Brand Voice Creation:** Once your materials are unified, Brand Voice synthesizes them into LLM-ready guidelines: voice pillars, tone parameters, a "We Are / We Are Not" framework that gives Claude a clear operating boundary, and terminology standards that reflect real company language -- not aspirational copy. The same guardrails that keep veteran teams on-brand mean new hires produce quality content in week one instead of month three.

**Brand Enforcement:** Every piece of AI-generated content (sales emails, proposals, marketing pages, press releases) gets written against those guidelines from the start. Claude doesn't just write faster. It writes like you. Tone drift and positioning gaps get caught before they reach a prospect or investor.

## Installation

### Prerequisites

- [Claude Desktop](https://claude.ai/download) with Cowork enabled

### Install the Plugin

1. Download the `brand-voice-plugin.zip` file from this repository
2. Open Claude Desktop
3. Navigate to the **Cowork** tab
4. Click **Plugins** in the sidebar
5. Click **Upload Plugin**
6. Select the `brand-voice-plugin.zip` file
7. The plugin will be available immediately after upload

### Connect Your Data Sources (Optional)

Brand Voice works best when connected to your existing tools. After installing the plugin, connect any of the following MCP services in Cowork settings:

| Connector | Purpose |
|-----------|---------|
| **Notion** | Store and retrieve brand guidelines, access meeting notes |
| **Atlassian** | Store and retrieve brand guidelines, access meeting notes |
| **Box** | Store and retrieve brand guidelines, access meeting notes |
| **Figma** | Access brand design assets |
| **Gong** | Generate on-brand presentations |
| **Microsoft-365** | Track brand guideline updates |

## Usage

### Generate Brand Guidelines

Use `/brand:generate-guidelines` to create your brand voice guidelines from any combination of sources -- documents, sales call transcripts, or both.

```
/brand:generate-guidelines
Analyze my pitch deck, style guide, and last 10 sales calls to create brand guidelines
```

Brand Voice will extract voice attributes, messaging patterns, tone guidelines, and terminology from your sources, then prompt you to save the guidelines to Notion or Google Drive for future sessions.

### Enforce Brand Voice

Use `/brand:enforce-voice` to create content that follows your brand guidelines.

```
/brand:enforce-voice
Draft a cold email to a VP of Engineering at a Series B infrastructure company
```

Brand Voice automatically loads your saved guidelines (from Notion, Google Drive, or the current session) and applies them to every piece of content it generates. It explains the brand choices it made so your team learns the voice, not just follows it.

## How It Works

```
Your Sources                    Brand Voice Plugin                Output
--------------                  ------------------                ------
Pitch decks
Style guides          -->       /brand:generate-guidelines  -->   Brand Voice
Email templates                 (discover + synthesize)           Guidelines
Sales call transcripts                                            (saved to Notion
Meeting recordings                                                 or Google Drive)
Notion pages
Google Drive docs

                                /brand:enforce-voice        -->   On-brand emails,
Brand Voice Guidelines  -->     (load + apply + validate)         proposals, decks,
                                                                  LinkedIn posts...
```

## Plugin Structure

```
brand-voice-plugin/
├── .claude-plugin/
│   └── plugin.json                        # Plugin manifest
├── .mcp.json                              # MCP server connections
├── agents/                                # Specialized sub-agents
│   ├── brand-discovery.md                 # Generates brand-aligned content
│   ├── content-generation.md              # Generates brand-aligned content
│   ├── conversation-analysis.md           # Analyzes sales call transcripts
│   ├── document-analysis.md               # Parses and extracts from documents
│   └── quality-assurance.md               # Validates content and guidelines
├── commands/                              # Slash commands
│   ├── discover-brand.md                  # /brand:brand-discover
│   ├── enforce-voice.md                   # /brand:enforce-voice
│   └── generate-guidelines.md             # /brand:generate-guidelines
└── skills/                                # Auto-triggered skills
    ├── brand-discovery/
    │   └── SKILL.md                       # Guideline generation logic
    ├── brand-voice-enforcement/
    │   └── SKILL.md                       # Brand enforcement logic
    └── guideline-generation/
        └── SKILL.md                       # Guideline generation logic
```

## Built By

[Tribe AI](https://www.tribeai.com) -- we help enterprises deploy AI that actually works.

## License

MIT License

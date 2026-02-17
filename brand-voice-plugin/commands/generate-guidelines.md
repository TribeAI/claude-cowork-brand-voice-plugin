# /brand:generate-guidelines Command

## Command
`/brand:generate-guidelines`

## Description
Generate comprehensive brand guidelines by analyzing recorded sales calls, customer conversations, and team discussions to extract implicit brand voice patterns.

## Usage
```
/brand:generate-guidelines [source specification]
```

## Examples

### Example 1: Analyze Uploaded Transcripts
```
/brand:generate-guidelines
I've uploaded my last 10 sales call transcripts. Please extract our brand voice.
```

### Example 2: Query from Granola
```
/brand:generate-guidelines
Analyze all my sales calls from the past month using Granola
```

### Example 3: Specific Call Types
```
/brand:generate-guidelines
Analyze discovery calls with enterprise prospects to create positioning guidelines
```

### Example 4: Team Analysis
```
/brand:generate-guidelines
Generate guidelines from our top-performing reps' calls this quarter
```

## What Happens
1. Discovers and ingests conversation transcripts from specified sources
2. Analyzes voice attributes, messaging patterns, tone variations
3. Identifies successful language patterns and anti-patterns
4. Extracts what works in different contexts (cold calls, demos, objections)
5. Generates comprehensive brand guidelines with evidence from actual calls
6. Assigns confidence scores based on data quality and consistency
7. Saves output to `/mnt/user-data/outputs/brand-guidelines/`
8. Provides key findings and recommendations

## Supported Sources
- Granola meeting transcripts (via MCP)
- Gong call recordings
- Zoom transcripts
- Google Meet transcripts
- Manual transcript uploads
- Notion meeting notes (via MCP)

## Output
Brand guidelines document including:
- Discovered voice attributes with supporting evidence
- Messaging insights from successful conversations
- Tone guidelines by conversation type
- Successful phrases and questions
- Anti-patterns to avoid
- Confidence scores and recommendations

## Quality Requirements
- Minimum 5 conversations recommended
- At least 3 different conversation types
- Transcripts with speaker identification
- Sufficient content per conversation (>500 words)

## Related Commands
- `/brand:enforce-voice` - Use generated guidelines for content creation
- `/brand:convert-docs` - Generate guidelines from documents instead

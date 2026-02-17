# Brand Guideline Generation Skill

## Purpose
Create comprehensive brand guidelines by analyzing recorded sales calls, customer conversations, and team discussions to extract implicit brand voice patterns.

## When This Skill Activates

This skill automatically activates when:
- The user uploads meeting transcripts
- The user uses `/brand:generate-guidelines`
- The user mentions "creating guidelines from calls"
- Multiple conversation transcripts are detected

## What This Skill Does

### 1. Conversation Discovery & Ingestion

**Supported Sources:**
- Granola meeting transcripts (via MCP)
- Gong call recordings (manual upload or API)
- Zoom transcripts (via file upload or connector)
- Google Meet transcripts
- Manual transcript uploads (.txt, .json, .md)
- Notion meeting notes (via MCP)

**Ingestion Process:**
```python
# Pseudo-code for reference
def ingest_conversations(sources):
    conversations = []

    # From Granola MCP
    if granola_connected:
        recent_meetings = query_granola(limit=20)
        conversations.extend(recent_meetings)

    # From uploaded files
    for file in uploaded_files:
        transcript = parse_transcript(file)
        conversations.append(transcript)

    # From Notion
    if notion_connected:
        meeting_notes = query_notion_database("Meetings")
        conversations.extend(meeting_notes)

    return conversations
```

**Conversation Metadata to Capture:**
- Participants
- Date/time
- Meeting type (sales call, customer conversation, internal discussion)
- Duration
- Outcome (if available)
- User-provided context

### 2. Conversation Analysis

**Analysis Dimensions:**

#### A. Voice Attribute Detection

Look for patterns in how team members describe products/services:

**Methodology:**
- Analyze adjective frequency
- Identify recurring personality traits
- Note tone shifts by context
- Compare formal vs. casual language ratios

**Extraction Examples:**
```
From transcript: "We've built something incredibly powerful, but we wanted to
make sure it was dead simple to use..."

Extracted attributes:
- Confident (claiming "incredibly powerful")
- User-focused (emphasis on "simple to use")
- Humble/accessible (contrast of power with simplicity)
```

#### B. Messaging Pattern Recognition

Identify what messages consistently appear in successful conversations:

**Look For:**
- Value propositions mentioned repeatedly
- Problems/pain points addressed
- Solution positioning
- Differentiation points
- Success metrics cited

**Pattern Template:**
```
Message: [Core theme]
Frequency: [X mentions across Y calls]
Contexts: [When this message appears]
Variations: [Different ways it's expressed]
Effectiveness: [Based on conversation outcome]
```

#### C. Tone Analysis by Context

Map tone variations to different situations:

**Context Categories:**
- Cold outreach
- Discovery calls
- Product demos
- Objection handling
- Closing discussions
- Customer check-ins

**Tone Indicators:**
- Formality level (you vs. y'all, formal titles vs. first names)
- Technical depth (jargon density)
- Emotional energy (exclamation points, enthusiasm markers)
- Question patterns (open vs. closed questions)
- Pacing (rapid fire vs. thoughtful pauses)

#### D. Successful Language Patterns

Identify specific phrases/approaches that lead to positive outcomes:

**Success Indicators:**
- Positive customer responses
- Progression to next steps
- Customer questions indicating interest
- Agreement signals

**Extract:**
- Opening lines that work
- Transition phrases
- Objection handling language
- Closing approaches

#### E. Anti-Patterns & What to Avoid

Identify what doesn't work:

**Look For:**
- Statements followed by pushback
- Jargon that confuses prospects
- Tone shifts that lose engagement
- Messages that stall conversations

### 3. Synthesis & Guideline Generation

**Synthesis Process:**

1. **Aggregate Findings**
   - Combine insights across all conversations
   - Weight by conversation outcome
   - Prioritize patterns from top performers

2. **Derive Brand Voice Attributes**
   ```
   IF confidence_score > 0.8 AND frequency > 5:
       Include as core voice attribute
   IF confidence_score > 0.6:
       Include as secondary attribute with caveat
   ```

3. **Build Messaging Framework**
   - Primary messages (appear in 50%+ of conversations)
   - Secondary messages (appear in 20-50%)
   - Context-specific messages

4. **Create Tone Guidelines**
   - Map observed tone to content types
   - Include examples from actual calls
   - Note contextual variations

5. **Compile Do's and Don'ts**
   - Do's: Successful patterns with examples
   - Don'ts: Anti-patterns with alternatives

**Output Structure:**

```markdown
# [Company] Brand Voice Guidelines
*Generated from [N] sales conversations*

## Generation Metadata
- Conversations Analyzed: [N]
- Date Range: [start] to [end]
- Top Performers Included: [names if provided]
- Confidence Score: [overall score]

## Discovered Brand Voice Attributes

### Primary Attributes
1. **[Attribute Name]** (Confidence: [score])
   - Evidence: Detected in [X] of [N] calls
   - How it manifests: [description]
   - Example from actual call:
     > "[Quote from transcript]"
     - Speaker: [name], Prospect: [title]

### Secondary Attributes
[Same format]

## Messaging Insights

### Core Value Proposition
*Most frequently used positioning:*
"[Extracted value prop]"

**Variations Observed:**
- "[Variation 1]" (used in [context])
- "[Variation 2]" (used in [context])

### Key Message Themes
1. **[Theme Name]** (Frequency: [X]%)
   - How top performers position this: [description]
   - Actual examples:
     - "[Quote 1]"
     - "[Quote 2]"
   - Effectiveness: [High/Medium based on outcomes]

## Tone Guidelines (From Conversation Analysis)

### Cold Outreach
**Observed Patterns:**
- Formality: [Professional/Casual/Friendly]
- Average opener length: [X] words
- Successful opening patterns:
  1. "[Pattern 1 with example]"
  2. "[Pattern 2 with example]"

### Discovery Calls
[Same structure]

### Product Demos
[Same structure]

### Objection Handling
**Common Objections:**
1. [Objection]: [How top performers respond]
2. [Objection]: [How top performers respond]

## Language That Works

### Successful Phrases
*Ranked by effectiveness and frequency:*

1. **[Phrase category]**
   - "[Actual phrase from call]"
   - Context: [when to use]
   - Why it works: [analysis]

### Questions That Engage
*Questions that consistently get positive responses:*

1. "[Question example]"
   - Response rate: [X]%
   - Typically leads to: [outcome]

## Language to Avoid

### Anti-Patterns Detected
1. **[Category]**
   - What was said: "[Example]"
   - Customer response: [negative indicator]
   - Better alternative: "[Suggestion]"

### Jargon That Confuses
- **Avoid:** "[Technical term]"
- **Use instead:** "[Plain language alternative]"
- **Or explain:** "[How top performers explain it]"

## Conversation Flow Patterns

### Successful Call Structure
*Based on [N] successful conversations:*

1. **Opening** ([X] minutes avg)
   - Pattern: [description]
   - Example: "[Quote]"

2. **Discovery** ([X] minutes avg)
   - Key questions to ask
   - Listening patterns

[Continue for each phase]

## Contextual Adaptations

### Enterprise vs. SMB
**Key Differences Observed:**
- Enterprise: [tone/approach]
- SMB: [tone/approach]

### Technical vs. Business Buyer
**Adaptation Strategy:**
- Technical: [observed patterns]
- Business: [observed patterns]

## Confidence Scores by Section

| Section | Confidence | Basis |
|---------|------------|-------|
| Voice Attributes | [High/Med/Low] | [N] calls analyzed |
| Messaging | [High/Med/Low] | [reasoning] |
| Tone Guidelines | [High/Med/Low] | [reasoning] |

## Data Gaps & Recommendations

**Missing Data:**
- [Gap 1]: Recommend [solution]
- [Gap 2]: Recommend [solution]

**Next Steps:**
1. [Recommendation based on findings]
2. [Recommendation for improvement]

## Appendix: Source Conversations

### Analyzed Conversations
1. **[Call 1]**
   - Date: [date]
   - Participants: [names]
   - Outcome: [result]
   - Key excerpts used: [sections]

[List all sources]
```

### 4. Quality Assurance & Validation

**Pre-Generation Checks:**
- [ ] Minimum 5 conversations analyzed
- [ ] At least 3 different conversation types
- [ ] Transcripts include speaker identification
- [ ] Sufficient content per conversation (>500 words)

**Post-Generation Validation:**
- [ ] All voice attributes have supporting evidence
- [ ] Confidence scores calculated for each section
- [ ] Examples come from actual transcripts
- [ ] No personally identifiable information exposed
- [ ] Guidelines are actionable (not just descriptive)

**Confidence Scoring:**
```python
def calculate_confidence(pattern, conversations):
    frequency = count_occurrences(pattern, conversations)
    consistency = measure_consistency(pattern, conversations)
    outcome_correlation = correlate_with_success(pattern, conversations)

    confidence = (frequency * 0.3) + (consistency * 0.4) + (outcome_correlation * 0.3)

    if confidence > 0.8:
        return "High"
    elif confidence > 0.5:
        return "Medium"
    else:
        return "Low"
```

### 5. User Guidance & Refinement

**Present Guidelines with Context:**
```
✅ Brand guidelines generated from [N] conversations!

📊 **Analysis Summary:**
- Conversations: [N] calls from [date range]
- Top performers: [names if provided]
- Patterns identified: [number]
- Confidence: [overall score]

🎯 **Key Findings:**
1. Your strongest voice attribute: [attribute]
2. Most effective message: [message]
3. Surprising insight: [insight]

📝 **Recommendations:**
- [Actionable recommendation 1]
- [Actionable recommendation 2]

Would you like me to:
1. Walk you through the key findings
2. Compare this to any existing brand docs
3. Start using it to create content
```

**Iterative Refinement:**
- Allow user to provide feedback on accuracy
- Offer to re-analyze with different parameters
- Suggest supplementing with document-based guidelines

## Sub-Agent: Conversation Analysis Agent

Delegate heavy analysis to specialized sub-agent:

**Capabilities:**
- Natural language processing
- Pattern recognition across conversations
- Sentiment analysis
- Speaker differentiation
- Outcome correlation
- Statistical confidence calculation

**Invocation:**
```
Invoke Conversation-Analysis-Agent with:
- List of transcripts
- Analysis focus (all dimensions or specific)
- Success criteria (what indicates good outcome)
- Weighting preferences (e.g., prioritize recent calls)
```

## Example Workflows

### Workflow 1: Founder Sales Calls
```
User: "I have my last 10 sales calls. Can you extract our brand voice?"

Skill Actions:
1. Ingest 10 transcripts
2. Identify this is founder → likely authoritative voice
3. Analyze messaging consistency
4. Extract value props mentioned repeatedly
5. Note tone variations (founder adapts to audience)
6. Identify successful patterns (which calls closed)
7. Generate guidelines emphasizing founder's approach
8. Flag areas where voice might need refinement for team
```

### Workflow 2: Team Voice Consistency
```
User: "/brand:generate-guidelines from all sales calls this quarter"

Skill Actions:
1. Query Granola/Gong for Q transcripts (50+ calls)
2. Segment by sales rep
3. Identify common patterns across all reps
4. Note variations between top/bottom performers
5. Extract what top 20% does differently
6. Generate guidelines that codify best practices
7. Highlight where team is already consistent
8. Flag areas needing alignment
```

### Workflow 3: Product Launch Positioning
```
User: "Analyze our beta customer calls to create positioning guidelines"

Skill Actions:
1. Ingest beta customer call transcripts
2. Focus on: how customers describe value, pain points addressed
3. Extract language customers use (not our internal jargon)
4. Identify most resonant messages
5. Note objections and successful responses
6. Generate guidelines based on customer language
7. Recommend product positioning based on actual conversations
```

## Error Handling

### Insufficient Data
```
⚠️ Limited conversation data:
- Conversations available: [N]
- Minimum recommended: 5
- Current confidence: Low

Options:
1. Proceed with preliminary guidelines (marked as draft)
2. Upload more conversation transcripts
3. Supplement with existing brand documents (/brand:convert-docs)
4. Wait and analyze more calls over time

What would you like to do?
```

### Poor Quality Transcripts
```
⚠️ Transcript quality issues detected:
- [N] transcripts missing speaker labels
- [N] transcripts very short (<200 words)
- [N] transcripts may be incomplete

Recommendations:
1. Remove low-quality transcripts: [list]
2. Proceed but note reduced confidence
3. Re-upload with better transcription

Proceed anyway? (Guidelines will be marked as "preliminary")
```

### No Success Indicators
```
⚠️ Cannot determine conversation outcomes:
- No outcome data provided for calls
- Unable to distinguish successful vs. unsuccessful patterns

Recommendations:
1. Manually label some calls as "successful"
2. Proceed with frequency-based analysis only
3. Re-analyze later with outcome data

Current approach: Will extract most common patterns without
weighting by success.
```

## Privacy & Security

**PII Protection:**
- Redact customer names by default
- Remove contact information
- Anonymize company names if requested
- Flag sensitive information

**Data Handling:**
- Transcripts processed locally
- No conversation data sent to external servers
- Generated guidelines don't expose customer details
- Source conversations not stored (only processed)

## Integration Points

### With Document Conversion
- Offer to merge conversation-based guidelines with document-based
- Compare and highlight differences
- Suggest which source to prioritize

### With Brand Voice Enforcement
- Immediately enable using new guidelines
- Test guidelines on sample content
- Refine based on application

### With MCP Connectors
- **Granola:** Auto-fetch recent meetings for analysis
- **Gong:** Access call library (when available)
- **Notion:** Store generated guidelines in team workspace
- **Slack:** Notify team when guidelines ready for review

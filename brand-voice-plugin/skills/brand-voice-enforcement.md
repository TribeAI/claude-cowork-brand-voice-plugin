# Brand Voice Enforcement Skill

## Purpose
Automatically apply existing brand guidelines to all sales and marketing content to ensure consistency in tone, messaging, and style.

## When This Skill Activates

This skill automatically activates when:
- The user is drafting emails, proposals, or presentations
- The user explicitly uses `/brand:enforce-voice`
- Content contains sales or marketing language
- The user references "brand voice" or "on-brand"

## What This Skill Does

### 1. Load Brand Guidelines
- Check for existing brand guidelines in:
  - `/mnt/user-data/outputs/brand-guidelines/`
  - Connected Notion workspace
  - Google Drive folder labeled "Brand Guidelines"
- If no guidelines found, prompt user to either:
  - Upload brand documents (trigger Skill 2)
  - Generate guidelines from calls (trigger Skill 3)

### 2. Analyze Content Request
When the user asks to create content:
- Identify content type (email, presentation, proposal, social post)
- Determine target audience
- Identify key messages needed
- Note any specific requirements

### 3. Apply Brand Guidelines
**Voice & Tone:**
- Apply brand personality attributes
- Adjust formality level based on context
- Ensure consistent use of terminology

**Messaging:**
- Incorporate key message pillars
- Use approved value propositions
- Follow positioning statements

**Style:**
- Follow preferred sentence structure
- Use approved terminology
- Avoid prohibited words/phrases
- Match example content patterns

### 4. Generate Content
Create content that:
- Matches brand voice attributes
- Follows tone guidelines for content type
- Incorporates key messages naturally
- Uses approved terminology
- Mirrors successful example patterns

### 5. Validate & Explain
After generation:
- Highlight where brand guidelines were applied
- Explain key brand voice decisions
- Note any areas where guidelines were adapted for context
- Suggest improvements if user wants to refine

## Example Workflows

### Workflow 1: Cold Outreach Email
```
User: "Draft a cold email to a VP of Sales at a Series B SaaS company"

Skill Actions:
1. Load brand guidelines
2. Identify this is cold outreach → apply "professional but warm" tone
3. Use value proposition: "AI that helps sales teams close faster"
4. Incorporate key message: "data-driven insights"
5. Generate email following successful cold email examples
6. Avoid prohibited term "synergy"
7. Present email with explanation of brand choices
```

### Workflow 2: Pitch Deck Creation
```
User: "/brand:enforce-voice Create a 10-slide pitch deck for an enterprise client"

Skill Actions:
1. Load brand guidelines
2. Apply "bold and confident" presentation tone
3. Use data-driven approach per guidelines
4. Structure following approved pitch format
5. Generate deck outline with brand-aligned messaging
6. If Gamma connector available, create actual slides
7. Explain brand voice application in each section
```

### Workflow 3: Proposal Writing
```
User: "Write a proposal for our AI platform implementation"

Skill Actions:
1. Load brand guidelines
2. Apply "consultative" proposal tone
3. Lead with problem-solution framework per guidelines
4. Include ROI-focused language
5. Use approved case study examples
6. Format following proposal template
7. Validate against brand do's and don'ts
```

## Brand Guideline Structure

This skill expects brand guidelines in this format:

```markdown
# Brand Voice Guidelines

## Voice Attributes
- Attribute 1: [description]
- Attribute 2: [description]

## Tone by Content Type
### Email
- [tone description]
- [key principles]

### Presentations
- [tone description]
- [key principles]

## Key Messages
1. [Message pillar 1]
2. [Message pillar 2]

## Terminology
### Preferred
- [term]: [usage]

### Prohibited
- [term]: [reason]

## Examples
### Good Example
[example with explanation]

### Bad Example
[example with explanation]
```

## Sub-Agent: Content Generation Agent

When generating content, delegate to specialized sub-agent:

**Capabilities:**
- Apply multiple brand constraints simultaneously
- Balance brand voice with user's specific requirements
- Adapt guidelines for different contexts
- Maintain consistency across long-form content

**Invocation:**
```
Invoke Content-Generation-Agent with:
- Brand guidelines document
- Content type and requirements
- Target audience
- Specific user instructions
```

## Error Handling

### No Brand Guidelines Found
```
I don't see any brand guidelines yet. I can help you:
1. Convert existing brand documents to guidelines (/brand:convert-docs)
2. Generate guidelines from your sales calls (/brand:generate-guidelines)
3. Create a basic template to get started

Which would you prefer?
```

### Conflicting Requirements
```
I notice the user's request [specific requirement] conflicts with
brand guideline [specific guideline].

Options:
1. Follow brand guideline strictly
2. Adapt guideline for this specific context
3. Ask user for clarification

Recommendation: [choice with reasoning]
```

## Best Practices

1. **Always explain brand choices:** Help users understand why content is written a certain way
2. **Adapt, don't force:** Brand guidelines are principles, not rigid rules
3. **Learn from feedback:** Note when users change generated content
4. **Context matters:** Sales email to CEO vs. junior employee needs different approach
5. **Be specific:** Don't just say "on-brand," explain what that means

## Integration Points

### With Document Conversion Skill
- If no guidelines exist, automatically offer to convert documents
- Update enforcement when guidelines are regenerated

### With Guideline Generation Skill
- If generating new guidelines, immediately apply them
- Suggest updating guidelines based on successful content

### With MCP Connectors
- **Notion:** Retrieve guidelines from shared workspace
- **Google Drive:** Access brand document folders
- **Gamma:** Apply brand to presentation generation
- **Slack:** Reference shared brand messaging

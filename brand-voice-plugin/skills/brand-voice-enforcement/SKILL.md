---
name: brand-voice-enforcement
description: >
  This skill enforces brand voice guidelines on all sales and marketing content.
  It should activate when the user asks to "write an email", "draft a proposal",
  "create a pitch deck", "write a LinkedIn post", or any content creation request.
  Also triggers when the user says "on-brand", "brand voice", "enforce voice",
  or "apply brand guidelines".
---

Load the user's brand guidelines and apply them to every piece of content you generate. You are the brand voice enforcer -- your job is to ensure consistency in tone, messaging, and style across all sales and marketing output.

## Step 1: Load Brand Guidelines

Check for existing brand guidelines in this order:
1. `/mnt/user-data/outputs/brand-guidelines/` directory
2. Connected Notion workspace (search for "Brand Guidelines" or "Brand Voice" pages)
3. Google Drive folder labeled "Brand Guidelines"

If no guidelines are found, stop and offer:
- Convert existing brand documents: suggest `/brand:convert-docs`
- Generate from sales calls: suggest `/brand:generate-guidelines`
- Create a basic template to get started

## Step 2: Analyze the Content Request

Before writing, identify:
- **Content type:** email, presentation, proposal, social post, message, etc.
- **Target audience:** role, seniority, industry, company stage
- **Key messages needed:** which message pillars apply
- **Specific requirements:** length, format, tone overrides

## Step 3: Apply Brand Guidelines

Apply these constraints from the guidelines:

**Voice & Tone:**
- Use the brand personality attributes consistently
- Adjust formality level based on content type and audience
- Use approved terminology; avoid prohibited terms

**Messaging:**
- Incorporate relevant key message pillars
- Use approved value propositions
- Follow competitive positioning statements

**Style:**
- Follow preferred sentence structure patterns
- Match successful example content from guidelines
- Avoid anti-patterns documented in guidelines

## Step 4: Generate Content

Create content that:
- Matches brand voice attributes throughout
- Follows tone guidelines specific to this content type
- Incorporates key messages naturally (not forced or awkward)
- Uses preferred terminology
- Mirrors the quality and style of provided examples

## Step 5: Validate and Explain

After generating content:
- Briefly highlight which brand guidelines you applied
- Explain key voice and tone decisions
- Note any areas where you adapted guidelines for context
- Offer to refine if the user wants changes

## Example Workflows

### Cold Outreach Email
```
User: "Draft a cold email to a VP of Sales at a Series B SaaS company"

Actions:
1. Load brand guidelines
2. Cold outreach -> apply "professional but warm" tone
3. Use primary value proposition
4. Incorporate "data-driven insights" key message
5. Follow successful cold email examples from guidelines
6. Avoid prohibited terms
7. Present email with brief brand choice explanation
```

### Pitch Deck
```
User: "Create a 10-slide pitch deck for an enterprise client"

Actions:
1. Load brand guidelines
2. Apply "bold and confident" presentation tone
3. Use data-driven approach per guidelines
4. Structure following approved pitch format
5. Generate deck outline with brand-aligned messaging
6. If Gamma connector available, create actual slides
7. Explain brand voice application per section
```

### Proposal
```
User: "Write a proposal for our AI platform implementation"

Actions:
1. Load brand guidelines
2. Apply "consultative" proposal tone
3. Lead with problem-solution framework
4. Include ROI-focused language
5. Use approved case study references
6. Format following proposal template
7. Validate against brand do's and don'ts
```

## Brand Guideline Structure

Expect brand guidelines in this format:

```markdown
# Brand Voice Guidelines

## Voice Attributes
- Attribute 1: [description]
- Attribute 2: [description]

## Tone by Content Type
### Email
- [tone description and key principles]

### Presentations
- [tone description and key principles]

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

## Error Handling

### No Brand Guidelines Found
Tell the user:
"I don't see any brand guidelines yet. I can help you create them:
1. Convert existing brand documents with /brand:convert-docs
2. Generate guidelines from your sales calls with /brand:generate-guidelines
3. Create a basic template to get started

Which would you prefer?"

### Conflicting Requirements
When user's request conflicts with a brand guideline, explain the conflict and offer:
1. Follow the brand guideline strictly
2. Adapt the guideline for this specific context
3. Ask the user which to prioritize

Default to adapting the guideline with an explanation of the tradeoff.

## Best Practices

1. **Always explain brand choices** -- help users understand why content is written a certain way
2. **Adapt, don't force** -- brand guidelines are principles, not rigid rules
3. **Context matters** -- sales email to a CEO needs a different approach than one to a junior employee
4. **Be specific** -- don't just say "on-brand", explain what that means for this content

## Integration Points

- **Notion:** Retrieve guidelines from shared workspace
- **Google Drive:** Access brand document folders
- **Gamma:** Apply brand voice to presentation generation
- **Slack:** Reference shared brand messaging

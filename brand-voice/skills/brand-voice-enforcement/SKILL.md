---
name: brand-voice-enforcement
description: >
  This skill should be used when the user asks to "write an email", "draft a proposal",
  "create a pitch deck", "write a LinkedIn post", "draft sales content", or any
  content creation request where brand voice should be applied. Also triggers on
  "on-brand", "brand voice", "enforce voice", "apply brand guidelines",
  "brand-aligned content", "write in our voice", or "use our brand tone".
---

# Brand Voice Enforcement

Apply existing brand guidelines to all sales and marketing content generation. Load the user's brand guidelines, apply voice constants and tone flexes to the content request, validate output, and explain brand choices.

## Loading Brand Guidelines

Check for existing brand guidelines in this order:
1. `.claude/brand-voice.local.md` — per-project settings and brand context
2. Connected Notion workspace — search for "Brand Guidelines" or "Brand Voice" pages
3. Any guideline document generated in the current session

If no guidelines are found, inform the user and suggest:
- Discover brand materials: `/brand-voice:discover-brand`
- Generate guidelines from existing sources: `/brand-voice:generate-guidelines`
- Provide guidelines manually or point to a file

Read `.claude/brand-voice.local.md` for enforcement settings:
- `strictness`: strict | balanced | flexible
- `always-explain`: whether to always explain brand choices

## Enforcement Workflow

### 1. Analyze the Content Request

Before writing, identify:
- **Content type**: email, presentation, proposal, social post, message, etc.
- **Target audience**: role, seniority, industry, company stage
- **Key messages needed**: which message pillars apply
- **Specific requirements**: length, format, tone overrides

### 2. Apply Voice Constants

Voice is the brand's personality — it stays constant across all content:
- Apply "We Are / We Are Not" attributes from guidelines
- Use brand personality consistently
- Incorporate approved terminology; reject prohibited terms
- Follow messaging framework and value propositions

Refer to `references/voice-constant-tone-flexes.md` for the "voice constant, tone flexes" model.

### 3. Flex Tone for Context

Tone adapts by content type and audience. Use the tone-by-context matrix from guidelines to set:
- **Formality**: How formal or casual should this be?
- **Energy**: How much urgency or enthusiasm?
- **Technical depth**: How detailed or accessible?

### 4. Generate Content

Create content that:
- Matches brand voice attributes throughout
- Follows tone guidelines for this specific content type
- Incorporates key messages naturally (not forced)
- Uses preferred terminology
- Mirrors the quality and style of guideline examples

For complex or long-form content, delegate to the content-generation agent.
For high-stakes content, delegate to the quality-assurance agent for validation.

### 5. Validate and Explain

After generating content:
- Briefly highlight which brand guidelines were applied
- Explain key voice and tone decisions
- Note any areas where guidelines were adapted for context
- Offer to refine based on feedback

If `always-explain` is true in settings, always include brand application notes.

## Handling Conflicts

When the user's request conflicts with brand guidelines:
1. Explain the conflict clearly
2. Provide a recommendation
3. Offer options: follow guidelines strictly, adapt for context, or override

Default to adapting guidelines with an explanation of the tradeoff.

## Open Questions Awareness

When generating content, check if the brand guidelines contain open questions:
- If content touches an unresolved open question, note it
- Apply the agent's recommendation from the open question unless the user specifies otherwise
- Suggest resolving the question if it significantly impacts the content

## Before/After Examples

Refer to `references/before-after-examples.md` for content type-specific examples showing how brand guidelines transform generic content into on-brand output.

## Additional Resources

### Reference Files

For detailed enforcement patterns and examples, consult:

- **`references/voice-constant-tone-flexes.md`** — The "voice constant, tone flexes" mental model, "We Are / We Are Not" table structure, and tone-by-context matrix explanation
- **`references/before-after-examples.md`** — Before/after content examples per content type showing enforcement in practice

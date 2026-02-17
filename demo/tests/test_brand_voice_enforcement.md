# Test Suite: Brand Voice Enforcement Skill

## Overview
Tests for applying brand guidelines to content creation (emails, presentations, proposals, social posts).

---

## Test 1: Cold Email Generation

### Test ID
`ENFORCE-001`

### Given
- Loaded brand guidelines with:
  - Voice: "Professional but approachable"
  - Tone for cold email: "Confident, value-first"
  - Key message: "AI-powered sales intelligence"
  - Prohibited terms: "synergy", "revolutionary"

### When
User requests: "Draft a cold email to a VP of Sales at a Series B SaaS company"

### Then
Should generate email that:
- ✓ Uses professional but warm tone
- ✓ Leads with value (not company intro)
- ✓ Mentions "AI-powered sales intelligence"
- ✓ Avoids prohibited terms
- ✓ Appropriate length (150-200 words)
- ✓ Includes explanation of brand choices made

### Validation Criteria
```yaml
brand_adherence:
  - tone_matches_guidelines: true
  - key_message_included: true
  - prohibited_terms_absent: true
  - voice_attributes_present: true

content_quality:
  - word_count: 150-250
  - clear_value_proposition: true
  - appropriate_call_to_action: true

transparency:
  - explains_brand_choices: true
  - highlights_guideline_application: true
```

---

## Test 2: Pitch Deck Outline

### Test ID
`ENFORCE-002`

### Given
- Brand guidelines with:
  - Presentation tone: "Bold and data-driven"
  - Key messages: ROI focus, proven results
  - Structure: Problem-Solution-Proof

### When
User requests: "/brand:enforce-voice Create a 10-slide pitch deck for an enterprise prospect"

### Then
Should generate:
- ✓ 10-slide outline
- ✓ Bold, confident language throughout
- ✓ Data-driven approach (metrics, stats)
- ✓ Problem-Solution-Proof structure
- ✓ ROI-focused messaging
- ✓ Enterprise-appropriate formality
- ✓ Explanation of brand alignment per section

### Validation Criteria
```yaml
structure:
  - slide_count: 10
  - follows_problem_solution_proof: true
  - logical_flow: true

brand_adherence:
  - bold_confident_tone: true
  - data_driven_content: true
  - roi_messaging_present: true

audience_appropriateness:
  - enterprise_level_formality: true
  - appropriate_depth: true
```

---

## Test 3: LinkedIn Post Creation

### Test ID
`ENFORCE-003`

### Given
- Brand guidelines with:
  - Social media tone: "Authentic, conversational"
  - Voice: "Knowledgeable without being preachy"
  - Length: Short-form preferred (< 150 words)

### When
User requests: "Write a LinkedIn post about our new AI feature"

### Then
Should generate:
- ✓ Conversational, authentic tone
- ✓ Under 150 words
- ✓ Knowledge-sharing approach (not salesy)
- ✓ Appropriate hashtags (if in guidelines)
- ✓ Call-to-action that feels natural
- ✓ Explanation of tone choices

### Validation Criteria
```yaml
tone:
  - conversational: true
  - authentic_not_corporate: true
  - knowledgeable_not_preachy: true

format:
  - word_count: "< 150"
  - appropriate_hashtags: true
  - natural_cta: true
```

---

## Test 4: Proposal Writing

### Test ID
`ENFORCE-004`

### Given
- Brand guidelines with:
  - Proposal tone: "Consultative and partnership-oriented"
  - Structure: Executive summary, problem, solution, implementation, ROI
  - Messaging: Co-creation approach

### When
User requests: "Write a proposal for our AI platform implementation for a Fortune 500 client"

### Then
Should generate:
- ✓ Full proposal structure (all sections)
- ✓ Consultative, collaborative tone throughout
- ✓ Partnership language ("together", "co-create")
- ✓ Executive summary leading with outcomes
- ✓ ROI section with quantified value
- ✓ Enterprise-appropriate formality
- ✓ Section-by-section brand explanation

### Validation Criteria
```yaml
structure:
  - has_exec_summary: true
  - has_problem_section: true
  - has_solution_section: true
  - has_implementation_plan: true
  - has_roi_section: true

tone:
  - consultative: true
  - partnership_oriented: true
  - collaborative_language: true

audience:
  - enterprise_appropriate: true
  - c_suite_ready: true
```

---

## Test 5: Brand Voice Adaptation by Audience

### Test ID
`ENFORCE-005`

### Given
- Same brand guidelines
- Two requests with different audiences

### When
1. User requests: "Email to a junior SDR"
2. User requests: "Email to a CEO"

### Then
Should generate two emails with:
- ✓ Same core brand voice
- ✓ Different formality levels
- ✓ Junior SDR: Friendly, helpful, detailed
- ✓ CEO: Concise, high-level, respectful of time
- ✓ Both follow brand guidelines appropriately
- ✓ Explanation of adaptation choices

### Validation Criteria
```yaml
consistency:
  - core_voice_consistent: true
  - key_messages_present_in_both: true

adaptation:
  - sdr_email_more_detailed: true
  - sdr_email_warmer_tone: true
  - ceo_email_concise: true
  - ceo_email_high_level: true

explanation:
  - adaptation_reasoning_provided: true
```

---

## Test 6: Handling Conflicting Requirements

### Test ID
`ENFORCE-006`

### Given
- Brand guideline: "Always professional tone"
- User request: "Write a super casual, fun email"

### When
User requests: "Write a super casual email for our cold outreach"

### Then
Should:
- ✓ Detect the conflict
- ✓ Present options to user:
  1. Follow brand guideline (professional)
  2. Adapt guideline for this context (professional-casual)
  3. Override guideline as requested
- ✓ Recommend option with reasoning
- ✓ Explain the tradeoff

### Validation Criteria
```yaml
conflict_detection:
  - conflict_identified: true
  - options_presented: ">= 2"
  - recommendation_with_reasoning: true

user_guidance:
  - explains_tradeoff: true
  - respects_user_intent: true
  - preserves_brand_integrity: true
```

---

## Test 7: No Guidelines Available

### Test ID
`ENFORCE-007`

### Given
- No brand guidelines loaded

### When
User requests: "Draft an email using our brand voice"

### Then
Should:
- ✓ Detect no guidelines exist
- ✓ Explain the situation clearly
- ✓ Offer alternatives:
  1. Convert existing brand docs (/brand:convert-docs)
  2. Generate from calls (/brand:generate-guidelines)
  3. Create basic template to get started
- ✓ Ask user preference
- ✓ NOT proceed without guidance

### Validation Criteria
```yaml
detection:
  - no_guidelines_detected: true
  - clear_message_to_user: true

options:
  - offers_document_conversion: true
  - offers_guideline_generation: true
  - offers_basic_template: true

behavior:
  - does_not_generate_without_guidelines: true
```

---

## Test 8: Multi-Constraint Application

### Test ID
`ENFORCE-008`

### Given
- Complex brand guidelines with:
  - 5 voice attributes
  - 3 key messages to incorporate
  - 10+ prohibited terms
  - Tone guidelines for email
  - Required terminology list
  - Example patterns to follow

### When
User requests: "Draft a follow-up email after a demo"

### Then
Should successfully:
- ✓ Apply all 5 voice attributes
- ✓ Weave in 2-3 key messages naturally
- ✓ Avoid all prohibited terms
- ✓ Use required terminology where appropriate
- ✓ Match example patterns
- ✓ Maintain natural flow (not robotic)
- ✓ Explain how all constraints were balanced

### Validation Criteria
```yaml
constraint_handling:
  - voice_attributes_present: 5
  - key_messages_included: ">= 2"
  - prohibited_terms_absent: true
  - required_terms_used: true

quality:
  - natural_language_flow: true
  - not_overly_constrained: true
  - reads_authentically: true

transparency:
  - explains_constraint_balancing: true
```

---

## Test 9: Content Refinement Loop

### Test ID
`ENFORCE-009`

### Given
- Generated email from previous request
- User feedback: "Make it shorter and more urgent"

### When
User requests: "Revise to be more concise and add urgency"

### Then
Should:
- ✓ Shorten content significantly
- ✓ Add urgency while maintaining brand voice
- ✓ Keep core brand voice attributes
- ✓ Maintain key messages
- ✓ Explain how urgency was added on-brand
- ✓ Show what was changed and why

### Validation Criteria
```yaml
revision:
  - word_count_reduced: true
  - urgency_added: true
  - brand_voice_maintained: true

transparency:
  - changes_explained: true
  - shows_before_after: true
  - reasoning_provided: true
```

---

## Test 10: Cross-Content Consistency

### Test ID
`ENFORCE-010`

### Given
- Same brand guidelines
- Multiple content requests in sequence:
  1. Cold email
  2. Follow-up email
  3. LinkedIn post about same topic

### When
User requests all three pieces

### Then
Should generate content with:
- ✓ Consistent brand voice across all three
- ✓ Appropriate tone shifts per medium
- ✓ Same key messages (adapted per format)
- ✓ Consistent terminology
- ✓ Complementary (not repetitive)
- ✓ Cohesive multi-touch campaign feel

### Validation Criteria
```yaml
consistency:
  - voice_consistent_across_all: true
  - key_messages_present_in_all: true
  - terminology_consistent: true

adaptation:
  - tone_appropriate_per_medium: true
  - format_appropriate: true
  - not_repetitive: true

campaign_coherence:
  - pieces_complement_each_other: true
  - logical_progression: true
```

---

## Test 11: Integration with MCP Connectors

### Test ID
`ENFORCE-011`

### Given
- Brand guidelines stored in Notion
- User request to create presentation

### When
User requests: "/brand:enforce-voice Create a presentation (use Gamma)"

### Then
Should:
- ✓ Load guidelines from Notion MCP
- ✓ Generate presentation outline
- ✓ Apply brand voice to all slides
- ✓ If Gamma MCP available: create actual slides
- ✓ Confirm where guidelines were loaded from
- ✓ Offer to save output back to Notion/Slack

### Validation Criteria
```yaml
integration:
  - notion_guidelines_loaded: true
  - gamma_invoked_if_available: true
  - cross_connector_workflow: true

user_experience:
  - seamless_integration: true
  - clear_source_attribution: true
  - save_options_offered: true
```

---

## Performance Benchmarks

| Test | Max Generation Time | Expected Output Size |
|------|---------------------|---------------------|
| ENFORCE-001 | 20 seconds | 150-250 words |
| ENFORCE-002 | 45 seconds | 500-800 words |
| ENFORCE-004 | 60 seconds | 1000-1500 words |

---

## Common Validation Checks (All Tests)

```yaml
brand_adherence:
  - follows_voice_guidelines: true
  - follows_tone_guidelines: true
  - includes_key_messages: true
  - avoids_prohibited_terms: true
  - uses_approved_terminology: true

content_quality:
  - natural_language: true
  - appropriate_length: true
  - clear_purpose: true
  - appropriate_cta: true

user_experience:
  - explains_brand_choices: true
  - transparent_about_tradeoffs: true
  - offers_refinement_options: true

technical:
  - generates_valid_markdown: true
  - no_hallucinated_brand_rules: true
  - references_actual_guidelines: true
```

# Test Suite: Guideline Generation Skill

## Overview
Tests for generating brand guidelines from sales conversation transcripts and meeting recordings.

---

## Test 1: Single Sales Call Analysis

### Test ID
`GUIDE-GEN-001`

### Given
- 1 detailed sales call transcript (~3000 words)
- Includes: discovery, demo, objection handling
- Clear speaker labels

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/sales-call-01.md`

### Then
Should produce guidelines with:
- ✓ 2-3 discovered voice attributes
- ✓ Key messaging themes identified
- ✓ Tone analysis by call phase
- ✓ Successful language patterns extracted
- ✓ Confidence marked as "Low-Medium" (single source)
- ✓ Recommendation to analyze more calls

### Validation Criteria
```yaml
extraction:
  - voice_attributes_count: ">= 2"
  - messaging_themes_count: ">= 2"
  - tone_analysis_present: true
  - examples_from_transcript: true

confidence:
  - overall_confidence: "Low" or "Medium"
  - recommends_more_data: true

quality:
  - quotes_from_actual_transcript: true
  - no_hallucinated_content: true
```

---

## Test 2: Multi-Call Pattern Recognition

### Test ID
`GUIDE-GEN-002`

### Given
- 10 sales call transcripts
- Mix of: cold calls, discovery, demos, closing
- Different sales reps
- Varying outcomes (won/lost deals)

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/`

### Then
Should produce guidelines with:
- ✓ 4+ voice attributes with frequency data
- ✓ Primary value proposition (most common)
- ✓ Tone guidelines per conversation type
- ✓ Successful patterns (from won deals)
- ✓ Anti-patterns (from lost deals)
- ✓ Confidence marked as "High"
- ✓ Statistical support for findings

### Validation Criteria
```yaml
pattern_recognition:
  - patterns_identified: ">= 5"
  - frequency_data_included: true
  - cross_call_analysis: true

success_correlation:
  - won_deal_patterns_highlighted: true
  - lost_deal_antipatterns_flagged: true

statistical_rigor:
  - confidence_scores_calculated: true
  - sample_size_noted: true
  - percentage_frequency: true
```

---

## Test 3: Top Performer vs Team Analysis

### Test ID
`GUIDE-GEN-003`

### Given
- 15 transcripts: 5 from top performer, 10 from team average
- Labeled with outcomes

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/performance-comparison/`

### Then
Should:
- ✓ Identify patterns unique to top performer
- ✓ Highlight differences in approach
- ✓ Extract what works better
- ✓ Recommend adopting top performer patterns
- ✓ Note areas where team is already aligned

### Validation Criteria
```yaml
comparison:
  - top_performer_patterns_identified: true
  - differences_highlighted: true
  - recommendations_provided: true

insights:
  - specific_language_differences: true
  - tone_variations_noted: true
  - outcome_correlation: true
```

---

## Test 4: Customer Language Extraction

### Test ID
`GUIDE-GEN-004`

### Given
- 8 customer call transcripts
- Focus on: how customers describe their problems
- Customer feedback on product value

### When
User executes: `/brand:generate-guidelines --focus=customer-language fixtures/inputs/transcripts/customer-calls/`

### Then
Should:
- ✓ Extract language customers use (not internal jargon)
- ✓ Identify pain points in customer words
- ✓ Capture value descriptions from customers
- ✓ Recommend customer-centric messaging
- ✓ Flag jargon that confused customers

### Validation Criteria
```yaml
customer_focus:
  - customer_quotes_included: true
  - pain_points_in_customer_words: true
  - jargon_confusion_flagged: true

recommendations:
  - suggests_customer_language: true
  - avoids_internal_terminology: true
```

---

## Test 5: Insufficient Data Handling

### Test ID
`GUIDE-GEN-005`

### Given
- Only 2 short transcripts (~500 words each)
- Limited diversity in conversation types

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/limited/`

### Then
Should:
- ✓ Display warning about limited data
- ✓ Note minimum is 5 conversations
- ✓ Offer to proceed with "preliminary" guidelines
- ✓ Mark output as "Draft" with low confidence
- ✓ Suggest uploading more transcripts
- ✓ Offer to supplement with document conversion

### Validation Criteria
```yaml
warning:
  - insufficient_data_warning: true
  - minimum_requirement_stated: true
  - options_presented: true

if_user_proceeds:
  - marked_as_draft: true
  - low_confidence_noted: true
  - recommendations_for_improvement: true
```

---

## Test 6: Poor Quality Transcript Handling

### Test ID
`GUIDE-GEN-006`

### Given
- 5 transcripts with issues:
  - 2 missing speaker labels
  - 1 very short (< 200 words)
  - 1 with garbled text
  - 1 good quality

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/quality-issues/`

### Then
Should:
- ✓ Flag quality issues per transcript
- ✓ Offer to exclude problematic ones
- ✓ Process good quality transcript
- ✓ Note reduced confidence due to limited data
- ✓ Suggest re-uploading better versions

### Validation Criteria
```yaml
quality_check:
  - issues_identified: 4
  - specific_problems_listed: true
  - exclusion_recommendations: true

processing:
  - good_transcript_processed: true
  - reduced_confidence_noted: true
```

---

## Test 7: Privacy & PII Protection

### Test ID
`GUIDE-GEN-007`

### Given
- Transcripts containing:
  - Customer names
  - Company names
  - Email addresses
  - Phone numbers

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/with-pii/`

### Then
Should:
- ✓ Redact customer names in output
- ✓ Remove contact information
- ✓ Anonymize company names (or mark as [Company])
- ✓ Preserve quotes but protect identity
- ✓ Note PII was redacted in metadata

### Validation Criteria
```yaml
pii_protection:
  - customer_names_redacted: true
  - contact_info_removed: true
  - companies_anonymized: true

output_quality:
  - quotes_still_valuable: true
  - context_preserved: true
  - pii_redaction_noted: true
```

---

## Test 8: Tone Variation by Context

### Test ID
`GUIDE-GEN-008`

### Given
- 10 transcripts across different contexts:
  - 3 cold calls (formal)
  - 3 demos (enthusiastic)
  - 2 pricing discussions (consultative)
  - 2 customer success check-ins (friendly)

### When
User executes: `/brand:generate-guidelines fixtures/inputs/transcripts/tone-variation/`

### Then
Should:
- ✓ Identify different tones by context
- ✓ Create tone guidelines per conversation type
- ✓ Note formality shifts
- ✓ Extract context-appropriate language patterns
- ✓ Provide examples for each context

### Validation Criteria
```yaml
tone_analysis:
  - contexts_identified: ">= 4"
  - tone_per_context: true
  - formality_shifts_noted: true

guidelines:
  - context_specific_guidance: true
  - examples_per_context: true
```

---

## Test 9: Objection Handling Patterns

### Test ID
`GUIDE-GEN-009`

### Given
- 8 transcripts featuring common objections:
  - Price concerns
  - Implementation complexity
  - Competitive comparisons
  - Timing issues

### When
User executes: `/brand:generate-guidelines --focus=objections fixtures/inputs/transcripts/objection-heavy/`

### Then
Should:
- ✓ Extract common objections
- ✓ Document successful responses
- ✓ Note unsuccessful approaches
- ✓ Provide objection handling language
- ✓ Include confidence based on outcomes

### Validation Criteria
```yaml
objection_analysis:
  - common_objections_listed: ">= 3"
  - successful_responses_included: true
  - unsuccessful_approaches_flagged: true

guidelines:
  - objection_handling_section: true
  - specific_language_provided: true
```

---

## Test 10: Merge with Existing Guidelines

### Test ID
`GUIDE-GEN-010`

### Given
- Existing brand guidelines (from documents)
- 10 new conversation transcripts

### When
User executes: `/brand:generate-guidelines --merge-existing fixtures/inputs/transcripts/`

### Then
Should:
- ✓ Load existing guidelines
- ✓ Extract patterns from conversations
- ✓ Compare document-based vs conversation-based findings
- ✓ Highlight alignments
- ✓ Flag discrepancies
- ✓ Offer to merge or keep separate
- ✓ Preserve existing structure

### Validation Criteria
```yaml
comparison:
  - existing_guidelines_loaded: true
  - alignments_noted: true
  - discrepancies_flagged: true

merge_options:
  - merge_option_offered: true
  - discrepancy_resolution_proposed: true
  - structure_preserved: true
```

---

## Performance Benchmarks

| Test | Max Processing Time | Expected Output Size |
|------|---------------------|---------------------|
| GUIDE-GEN-001 | 45 seconds | 2-3 KB |
| GUIDE-GEN-002 | 120 seconds | 8-12 KB |
| GUIDE-GEN-003 | 90 seconds | 6-10 KB |
| GUIDE-GEN-008 | 90 seconds | 7-10 KB |

---

## Common Validation Checks (All Tests)

```yaml
extraction_quality:
  - quotes_from_actual_transcripts: true
  - no_fabricated_examples: true
  - proper_attribution: true

privacy:
  - no_pii_exposed: true
  - customer_identity_protected: true

actionability:
  - guidelines_are_actionable: true
  - specific_language_examples: true
  - clear_do_and_dont_lists: true

metadata:
  - source_conversations_listed: true
  - confidence_scores_present: true
  - sample_size_noted: true
```

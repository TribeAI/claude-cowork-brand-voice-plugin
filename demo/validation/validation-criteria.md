# Validation Criteria for Brand Voice Plugin Tests

## Overview
This document defines how to validate that the Brand Voice Plugin is working correctly across all three skills: Document Conversion, Guideline Generation, and Brand Voice Enforcement.

---

## Document Conversion Validation

### Automated Checks

```yaml
structure_validation:
  required_sections:
    - "Brand Voice Overview"
    - "Core Voice Attributes"
    - "Tone Guidelines by Content Type"
    - "Messaging Framework"
    - "Terminology Guide"
    - "Content Examples"

  metadata_present:
    - creation_date
    - source_documents_list
    - version_number
    - confidence_scores

  format:
    - valid_markdown: true
    - proper_heading_hierarchy: true
    - no_broken_links: true
```

### Content Quality Checks

**Voice Attributes:**
- ✓ Minimum 3 attributes extracted
- ✓ Each attribute has description
- ✓ Each attribute has "how it shows up" examples
- ✓ Each attribute has "what to avoid" guidance

**Tone Guidelines:**
- ✓ At least 2 content types covered (email, presentations, etc.)
- ✓ Each content type has specific guidance
- ✓ Do's and Don'ts provided
- ✓ Examples included

**Terminology:**
- ✓ Preferred terms table with usage examples
- ✓ Prohibited terms with alternatives
- ✓ At least 5 entries in each category

**Source Attribution:**
- ✓ All source documents listed in appendix
- ✓ Key sections attributed to sources
- ✓ Confidence scores per section

### Manual Review Criteria

**Accuracy:**
- Does extracted content match source documents?
- Are voice attributes faithful to original intent?
- Are examples properly extracted (not fabricated)?

**Completeness:**
- Are major brand elements captured?
- Are gaps identified and noted?
- Are recommendations provided for missing content?

**Usability:**
- Can someone use these guidelines to create content?
- Is guidance specific enough to be actionable?
- Are examples helpful and clear?

---

## Guideline Generation Validation

### Automated Checks

```yaml
structure_validation:
  required_sections:
    - "Generation Metadata"
    - "Discovered Brand Voice Attributes"
    - "Messaging Insights"
    - "Tone Guidelines"
    - "Language That Works"
    - "Language to Avoid"
    - "Appendix: Source Conversations"

  metadata_required:
    - conversations_analyzed_count
    - date_range
    - confidence_scores
    - sample_size_noted

  evidence_required:
    - quotes_from_transcripts: true
    - frequency_data: true
    - no_fabricated_content: true
```

### Content Quality Checks

**Voice Attributes:**
- ✓ Minimum 2 attributes (low confidence) or 4 (high confidence)
- ✓ Each attribute has evidence from transcripts
- ✓ Frequency data included (appeared in X of Y calls)
- ✓ Actual quotes from transcripts provided

**Pattern Recognition:**
- ✓ Successful patterns identified with examples
- ✓ Anti-patterns identified (if unsuccessful calls present)
- ✓ Frequency percentages provided
- ✓ Outcome correlation noted

**Privacy:**
- ✓ No PII exposed (names redacted where appropriate)
- ✓ No contact information in output
- ✓ Company names handled appropriately

**Confidence Scoring:**
- ✓ Overall confidence score provided
- ✓ Section-by-section confidence scores
- ✓ Confidence reflects sample size and data quality
- ✓ Low confidence triggers warnings/recommendations

### Manual Review Criteria

**Accuracy:**
- Do quotes actually appear in transcripts?
- Are patterns genuinely present across multiple calls?
- Are anti-patterns correctly identified?

**Insight Quality:**
- Are discovered patterns actionable?
- Do messaging themes make sense?
- Would sales team find this useful?

**Statistical Rigor:**
- Are frequency claims accurate?
- Is sample size sufficient for confidence level?
- Are limitations acknowledged?

---

## Brand Voice Enforcement Validation

### Automated Checks

```yaml
brand_adherence:
  voice_attributes:
    - all_loaded_attributes_considered: true
    - no_contradicting_attributes: true

  terminology:
    - no_prohibited_terms_used: true
    - preferred_terms_used_appropriately: true

  tone:
    - matches_content_type_guidelines: true
    - appropriate_formality_level: true

  messaging:
    - key_messages_incorporated: true
    - value_prop_aligned: true
```

### Content Quality Checks

**Brand Compliance:**
- ✓ Follows voice attribute guidelines
- ✓ Uses appropriate tone for content type
- ✓ Incorporates key messages naturally
- ✓ Avoids all prohibited terms
- ✓ Uses preferred terminology

**Content Quality:**
- ✓ Natural language (not robotic)
- ✓ Appropriate length for content type
- ✓ Clear call-to-action if applicable
- ✓ Well-structured and scannable

**Transparency:**
- ✓ Explains which brand choices were made
- ✓ Highlights guideline applications
- ✓ Notes any tradeoffs or adaptations

**User Experience:**
- ✓ Content meets user's request
- ✓ Appropriate for stated audience
- ✓ Refinement options offered

### Manual Review Criteria

**Brand Accuracy:**
- Does content "feel" on-brand?
- Would brand stakeholders approve?
- Are adaptations appropriate for context?

**Effectiveness:**
- Would this content achieve its purpose?
- Is it compelling and well-written?
- Does it balance brand constraints with creativity?

**Audience Appropriateness:**
- Is formality level right for audience?
- Is technical depth appropriate?
- Would target audience respond positively?

---

## Cross-Skill Integration Validation

### Workflow Continuity

**Document Conversion → Brand Enforcement:**
- ✓ Converted guidelines immediately available for enforcement
- ✓ No manual steps required to use guidelines
- ✓ Guidelines format compatible with enforcement skill

**Guideline Generation → Brand Enforcement:**
- ✓ Generated guidelines automatically loaded
- ✓ Confidence scores inform enforcement approach
- ✓ Seamless transition from generation to application

**Document Conversion + Guideline Generation:**
- ✓ Can merge insights from both sources
- ✓ Conflicting guidelines flagged
- ✓ Prioritization logic clear

---

## Error Handling Validation

### Expected Error Scenarios

**1. Insufficient Data**
- ✓ Warning displayed to user
- ✓ Minimum requirements stated
- ✓ Options presented (proceed anyway, add more data)
- ✓ If proceeding, output marked as "Draft" or "Preliminary"

**2. Quality Issues**
- ✓ Specific problems identified
- ✓ Per-item quality assessment
- ✓ Recommendations for improvement
- ✓ Option to exclude low-quality inputs

**3. Conflicting Guidelines**
- ✓ Conflicts detected and flagged
- ✓ Both perspectives shown with sources
- ✓ Resolution recommendation provided
- ✓ User input requested if needed

**4. Missing Guidelines**
- ✓ Situation clearly explained
- ✓ Multiple resolution options offered
- ✓ Does NOT generate content without guidelines

---

## Performance Validation

### Speed Benchmarks

| Operation | Max Time | Target Time |
|-----------|----------|-------------|
| Convert 1 document | 30s | 20s |
| Convert 3 documents | 60s | 45s |
| Analyze 5 transcripts | 90s | 60s |
| Analyze 10 transcripts | 120s | 90s |
| Generate email | 20s | 15s |
| Generate pitch deck | 45s | 30s |

### Resource Usage
- Memory usage stays under 2GB
- No hanging processes
- Clean error handling (no crashes)

---

## Integration Validation (MCP Connectors)

### Connector Functionality

**Notion:**
- ✓ Can read brand guidelines from Notion pages
- ✓ Can write generated guidelines to Notion
- ✓ Proper authentication handling

**Google Drive:**
- ✓ Can access brand document folders
- ✓ Handles various file formats
- ✓ Permission errors handled gracefully

**Granola:**
- ✓ Can fetch meeting transcripts
- ✓ Proper transcript parsing
- ✓ Speaker identification preserved

**Gamma:**
- ✓ Can generate presentations
- ✓ Brand voice applied to slide content
- ✓ Visual format appropriate

**Slack:**
- ✓ Can share guidelines with team
- ✓ Notifications sent appropriately
- ✓ Proper formatting in Slack

---

## Test Result Scoring

### Pass Criteria by Test Level

**Level 1: Must Pass (Critical)**
- All automated structure checks pass
- No prohibited terms in output
- No fabricated content/hallucinations
- No PII exposure
- Error scenarios handled correctly

**Level 2: Should Pass (Important)**
- Content quality checks pass
- Appropriate confidence scores
- Useful explanations provided
- Performance within benchmarks

**Level 3: Nice to Have (Enhancement)**
- Exceptional insight quality
- Superior user experience
- Above-target performance
- Innovative applications

### Overall Test Status

**Pass:** All Level 1 + 80% of Level 2 criteria met
**Pass with Issues:** All Level 1 + 60% of Level 2
**Fail:** Any Level 1 criteria failed

---

## Regression Testing

### Areas to Monitor

**After Code Changes:**
- Re-run full test suite
- Verify no existing functionality broken
- Check performance hasn't degraded

**After Guideline Updates:**
- Validate new guidelines load correctly
- Ensure backward compatibility
- Test enforcement with updated guidelines

**After Connector Changes:**
- Verify MCP integrations still work
- Test error handling
- Validate data flow

---

## Continuous Validation

### Automated Testing
- Run test suite on every commit
- Flag failures immediately
- Track performance trends

### Manual Spot Checks
- Weekly review of generated content
- Monthly audit of brand adherence
- Quarterly user feedback collection

### Success Metrics to Track
- Test pass rate (target: 95%+)
- Average confidence scores (target: High for 80%+ of outputs)
- User satisfaction with outputs
- Time to generate content
- Adoption rate among sales team

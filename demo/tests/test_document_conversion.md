# Test Suite: Document Conversion Skill

## Overview
Tests for the brand document conversion skill that transforms scattered brand materials into unified, LLM-ready guidelines.

---

## Test 1: Basic Document Conversion - Style Guide

### Test ID
`DOC-CONV-001`

### Given
- Single brand style guide document (Markdown simulating PDF)
- Contains: voice attributes, tone guidelines, messaging

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/style-guide.md`

### Then
Should produce `brand-voice-guidelines.md` with:
- ✓ Extracted 3+ voice attributes with descriptions
- ✓ Tone guidelines organized by content type
- ✓ Key messaging section present
- ✓ Terminology guide (preferred/prohibited terms)
- ✓ Source document referenced in appendix
- ✓ Confidence scores included
- ✓ Document metadata (creation date, version)

### Validation Criteria
```yaml
structure:
  - has_section: "Brand Voice Overview"
  - has_section: "Tone Guidelines by Content Type"
  - has_section: "Messaging Framework"
  - has_section: "Terminology Guide"

content_quality:
  - voice_attributes_count: ">= 3"
  - tone_categories_count: ">= 2"
  - has_examples: true

metadata:
  - has_source_attribution: true
  - has_confidence_scores: true
  - has_creation_date: true
```

---

## Test 2: Multi-Document Consolidation

### Test ID
`DOC-CONV-002`

### Given
- 3 documents: style guide, pitch deck, email templates
- Some overlapping content, some unique to each

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/`

### Then
Should produce consolidated guidelines with:
- ✓ Voice attributes merged from all sources
- ✓ Messaging extracted from pitch deck
- ✓ Email tone derived from templates
- ✓ All 3 sources listed in appendix
- ✓ No duplicate content
- ✓ Conflicts resolved or flagged
- ✓ Source attribution for each section

### Validation Criteria
```yaml
consolidation:
  - sources_processed: 3
  - all_sources_referenced: true
  - no_duplicate_attributes: true

conflict_handling:
  - conflicts_detected: true/false
  - conflicts_resolved_or_flagged: true

completeness:
  - pitch_messaging_included: true
  - email_tone_guidelines_present: true
  - style_guide_attributes_present: true
```

---

## Test 3: Conflicting Guidelines Detection

### Test ID
`DOC-CONV-003`

### Given
- 2 documents with conflicting tone guidance
  - Doc A (2024): "Use casual, friendly tone"
  - Doc B (2023): "Maintain professional, formal tone"

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/conflicting/`

### Then
Should:
- ✓ Detect the conflict
- ✓ Flag conflict in output with ⚠️ marker
- ✓ Show both perspectives with sources
- ✓ Recommend resolution (prefer more recent)
- ✓ Request user input OR auto-resolve with explanation

### Validation Criteria
```yaml
conflict_detection:
  - conflict_flagged: true
  - both_sources_shown: true
  - recommendation_provided: true

resolution:
  - prefers_recent_doc: true
  - explains_reasoning: true
```

---

## Test 4: Insufficient Content Handling

### Test ID
`DOC-CONV-004`

### Given
- Single brief document (~200 words)
- Missing: tone guidelines, examples, terminology

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/brief-doc.md`

### Then
Should:
- ✓ Extract available content
- ✓ Flag missing sections with warnings
- ✓ Suggest what additional docs needed
- ✓ Mark confidence as "Low" for incomplete sections
- ✓ Offer to supplement with conversation analysis

### Validation Criteria
```yaml
handling:
  - warning_displayed: true
  - missing_sections_listed: true
  - recommendations_provided: true

confidence:
  - overall_confidence: "Low"
  - section_scores_reflect_gaps: true

user_guidance:
  - suggests_upload_more_docs: true
  - suggests_conversation_analysis: true
```

---

## Test 5: Multiple Format Support

### Test ID
`DOC-CONV-005`

### Given
- Mixed formats (simulated):
  - Markdown (simulating PDF extraction)
  - Structured text (simulating PPTX)
  - Plain text (simulating DOCX)

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/mixed-formats/`

### Then
Should:
- ✓ Successfully parse all formats
- ✓ Extract content regardless of format
- ✓ Normalize formatting in output
- ✓ Preserve semantic meaning across formats

### Validation Criteria
```yaml
format_handling:
  - all_formats_parsed: true
  - content_extracted_from_each: true
  - output_formatting_consistent: true
```

---

## Test 6: Large Document Set (10+ docs)

### Test ID
`DOC-CONV-006`

### Given
- 12 brand-related documents of varying quality

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/large-set/`

### Then
Should:
- ✓ Process all documents
- ✓ Prioritize by relevance and date
- ✓ Complete within reasonable time
- ✓ Produce comprehensive but not overwhelming output
- ✓ Group related content logically

### Validation Criteria
```yaml
performance:
  - all_docs_processed: true
  - processing_completed: true

output_quality:
  - not_overly_verbose: true
  - well_organized: true
  - prioritizes_key_content: true
```

---

## Test 7: Empty/Unreadable Document Handling

### Test ID
`DOC-CONV-007`

### Given
- 3 documents: 2 valid, 1 corrupted/empty

### When
User executes: `/brand:convert-docs fixtures/inputs/brand-docs/with-errors/`

### Then
Should:
- ✓ Skip unreadable document with warning
- ✓ Process valid documents successfully
- ✓ Complete conversion despite error
- ✓ Report which files had issues
- ✓ Suggest re-uploading problematic files

### Validation Criteria
```yaml
error_handling:
  - skipped_corrupted_file: true
  - warning_displayed: true
  - processing_continued: true

output:
  - valid_docs_processed: 2
  - guidelines_generated: true
  - error_report_included: true
```

---

## Performance Benchmarks

| Test | Max Processing Time | Expected Output Size |
|------|---------------------|---------------------|
| DOC-CONV-001 | 30 seconds | 2-4 KB |
| DOC-CONV-002 | 60 seconds | 5-8 KB |
| DOC-CONV-003 | 45 seconds | 3-5 KB |
| DOC-CONV-006 | 120 seconds | 10-15 KB |

---

## Common Validation Checks (All Tests)

```yaml
output_structure:
  - valid_markdown: true
  - has_table_of_contents: true
  - proper_heading_hierarchy: true

content_requirements:
  - no_pii_exposed: true
  - source_attribution_present: true
  - actionable_guidelines: true

metadata:
  - creation_timestamp: present
  - version_number: present
  - processing_stats: present
```

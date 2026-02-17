# Brand Voice Plugin Demo Walkthrough

## Overview
This document provides a comprehensive guide to demonstrating the Brand Voice Plugin using the TDD fixtures and tests.

**Demo Duration:** 30-45 minutes
**Audience:** Sales teams, marketing leaders, operations managers
**Goal:** Prove the plugin works and delivers value

---

## Pre-Demo Setup

### 1. Environment Preparation
```bash
# Navigate to demo directory
cd /path/to/claude-cowork-brand-voice-plugin/demo

# Verify test fixtures exist
ls -R fixtures/

# Verify expected outputs exist
ls -R fixtures/expected-outputs/
```

### 2. Plugin Installation
```bash
# Install the brand voice plugin
cp -r ../brand-voice-plugin ~/.cowork/plugins/brand-voice-plugin

# Verify installation
# (Check in Claude Desktop Cowork tab → Plugins)
```

### 3. Demo Data Ready
- ✓ Brand documents in `fixtures/inputs/brand-docs/`
- ✓ Conversation transcripts in `fixtures/inputs/transcripts/`
- ✓ Test cases in `tests/`
- ✓ Expected outputs in `fixtures/expected-outputs/`

---

## Demo Flow

### Part 1: Document Conversion (10 minutes)

**Scenario:** "We have scattered brand documents. Can we create unified guidelines?"

**Step 1: Show the Problem**
```bash
# Show the raw brand documents
ls fixtures/inputs/brand-docs/

# Open style guide
cat fixtures/inputs/brand-docs/style-guide.md
```

**Talking Points:**
- "Most companies have brand materials scattered across docs, decks, and templates"
- "Hard for sales teams to know what's on-brand"
- "Takes hours to manually compile into useful guidelines"

**Step 2: Run Document Conversion**
```
User: "/brand:convert-docs fixtures/inputs/brand-docs/"
```

**Expected Output:**
- Plugin ingests all 3 documents (style guide, pitch deck, email templates)
- Extracts voice attributes, tone guidelines, messaging, terminology
- Generates unified `brand-voice-guidelines.md`
- Shows confidence scores

**Step 3: Compare to Expected Output**
```bash
# Show the generated output
cat /mnt/user-data/outputs/brand-guidelines/brand-voice-guidelines.md

# Compare to expected
diff /mnt/user-data/outputs/brand-guidelines/brand-voice-guidelines.md \
     fixtures/expected-outputs/generated-guidelines/from-documents-expected.md
```

**Validation (TEST DOC-CONV-002):**
- ✓ All 3 sources processed and referenced
- ✓ No duplicate content
- ✓ Voice attributes extracted from style guide
- ✓ Messaging from pitch deck
- ✓ Email tone from templates
- ✓ High confidence scores

**Talking Points:**
- "In 60 seconds, we went from 3 disconnected docs to unified guidelines"
- "Notice how it pulled voice attributes from the style guide, messaging from the pitch deck, and tone from email examples"
- "Everything is sourced—you can see where each guideline came from"
- "Confidence scores tell you how solid each section is"

---

### Part 2: Guideline Generation from Conversations (10 minutes)

**Scenario:** "We don't have formal brand docs. Can we extract brand voice from our sales calls?"

**Step 1: Show the Source Material**
```bash
# List conversation transcripts
ls fixtures/inputs/transcripts/

# Show a sample successful call
cat fixtures/inputs/transcripts/cold-call-success-01.md
```

**Talking Points:**
- "What if you don't have brand docs, but you have great sales reps?"
- "We can analyze your best sales calls to extract what's already working"
- "This is your actual brand voice—how your team talks to customers"

**Step 2: Run Guideline Generation**
```
User: "/brand:generate-guidelines fixtures/inputs/transcripts/"
```

**Expected Output:**
- Analyzes all 7 transcripts (6 successful, 1 unsuccessful)
- Extracts voice attributes with evidence from calls
- Identifies successful messaging patterns
- Flags anti-patterns from unsuccessful call
- Shows frequency data and confidence scores

**Step 3: Show the Insights**
```bash
# View generated guidelines
cat /mnt/user-data/outputs/brand-guidelines/brand-voice-from-conversations.md
```

**Validation (TEST GUIDE-GEN-002):**
- ✓ 4+ voice attributes discovered
- ✓ Each attribute has supporting quotes from transcripts
- ✓ Successful patterns vs. anti-patterns
- ✓ Frequency data included
- ✓ High confidence (7 conversations analyzed)

**Key Insights to Highlight:**
- "Research-Driven and Personalized" - appeared in 6 of 7 successful calls
- "Problem-First, Not Product-First" - all successful calls led with customer problem
- Anti-pattern from unsuccessful call: Buzzword overload led to prospect disengagement
- Specific phrases that work: "How are you maintaining deal velocity while scaling?"

**Talking Points:**
- "We analyzed 7 calls and found clear patterns"
- "Your top reps are already doing this—now we can codify it"
- "See these quotes? These are actual statements from your successful calls"
- "We even caught what NOT to do from the unsuccessful call"
- "This isn't generic advice—this is YOUR playbook"

---

### Part 3: Brand Voice Enforcement (15 minutes)

**Scenario:** "Now that we have guidelines, can the AI help us create on-brand content?"

**Step 1: Load Guidelines**
```
User: "Load the brand guidelines we just created"
```

**Confirm:**
- Guidelines from Part 1 or Part 2 are loaded
- Plugin confirms guidelines are available

**Step 2: Cold Email Generation**
```
User: "Draft a cold email to a VP of Sales at a Series B SaaS company"
```

**Expected Output:**
- Generates email following brand guidelines
- Professional but warm tone
- Research-based opener
- Specific challenge (Series B scaling)
- Proof point with metrics
- Low-friction CTA
- Under 100 words
- **Explanation of brand choices made**

**Validation (TEST ENFORCE-001):**
- ✓ Matches voice attributes (confident, expert but accessible)
- ✓ Follows email tone guidelines (concise, value-first)
- ✓ Incorporates key message (deal velocity)
- ✓ No prohibited terms (synergy, leverage, paradigm)
- ✓ Appropriate length
- ✓ Clear explanation provided

**Step 3: Show the Explanation**
```
The plugin should output:

"Here's the cold email, applying TribeAI's brand voice:

[EMAIL CONTENT]

Brand Voice Explanation:
- Expert but Accessible: Used simple language (\"keeping deal cycles under control\")
  instead of jargon
- Confident and Proven: Included specific metric (\"30-40% longer\") and real company
  example
- Partnership-Oriented: Conversational tone (\"Quick question\"), collaborative offer
  (\"can show you\")
- Pragmatic: Led with business problem, connected to measurable outcome
- Followed email guidelines: Under 100 words, value-first, no generic opening
- Key message: Maintaining deal velocity during growth
- No prohibited terms used"
```

**Talking Points:**
- "Notice it didn't just write an email—it explained WHY it made each choice"
- "This is how teams learn what 'on-brand' actually means"
- "Compare this to generic AI output"

**Step 4: Show Adaptability - Different Audience**
```
User: "Now write the same email but for a junior SDR manager"
```

**Expected Output:**
- Same core brand voice
- More detailed and helpful tone
- Less executive-level language
- Explains more context
- Warmer, friendlier

**Validation (TEST ENFORCE-005):**
- ✓ Core voice consistent
- ✓ Adapted appropriately for junior audience
- ✓ Explanation of adaptation provided

**Talking Points:**
- "Same brand, different audience = different approach"
- "It knows when to be more formal vs. more helpful"
- "This is brand voice intelligence, not just templates"

**Step 5: Conflict Handling**
```
User: "Write a super casual, fun cold email with lots of emojis"
```

**Expected Output:**
- Detects conflict with "professional but warm" guideline
- Presents options to user:
  1. Follow brand guideline (professional but warm)
  2. Adapt for casual-but-still-professional
  3. Override and go casual as requested
- Recommends option with reasoning
- Explains tradeoff

**Validation (TEST ENFORCE-006):**
- ✓ Conflict detected
- ✓ Options presented
- ✓ Recommendation with reasoning
- ✓ Respects user choice

**Talking Points:**
- "It catches when you're going off-brand"
- "Doesn't just block you—gives you options and explains tradeoffs"
- "You're always in control, but you get smart guidance"

---

## Part 4: Full Workflow Demo (5 minutes)

**Scenario:** "Show me the complete workflow from zero to brand-enforced content"

**Step-by-Step:**

1. **Start with Raw Materials**
   ```
   User: "I have brand docs and some sales call recordings. Create brand guidelines."
   ```

2. **Plugin Routes Intelligently**
   - Detects both documents and transcripts
   - Offers to:
     a) Convert documents only
     b) Analyze conversations only
     c) Do both and merge

3. **User Chooses: "Do both and merge"**

4. **Plugin Executes:**
   - Converts documents → guidelines v1
   - Analyzes conversations → guidelines v2
   - Compares and merges
   - Highlights alignments and discrepancies
   - Creates unified guidelines

5. **Immediately Use for Content**
   ```
   User: "Now write a pitch deck outline"
   ```
   - Plugin applies merged guidelines
   - Generates on-brand pitch deck
   - Explains brand choices

**Talking Points:**
- "From scattered materials to generated content in under 5 minutes"
- "It handles the complexity—you just tell it what you need"
- "This is what happens when AI understands brand voice"

---

## Part 5: Test Verification (Optional, 5 minutes)

**For Technical Audiences:**

**Show Test Results:**
```bash
# Run automated tests
./run-tests.sh

# Show test results
cat test-results/summary.txt
```

**Test Results to Highlight:**
- ✓ 25/25 tests passing
- ✓ Document conversion accuracy: 98%
- ✓ Brand guideline quality: High confidence
- ✓ No prohibited terms in any generated content
- ✓ All performance benchmarks met

**Validation Checks:**
```bash
# Show validation for a specific test
cat test-results/DOC-CONV-002-validation.yaml
```

**Talking Points:**
- "We've built comprehensive tests to ensure quality"
- "Every piece of content is validated against brand guidelines"
- "This isn't subjective—we have clear pass/fail criteria"

---

## Demo Variations by Audience

### For Sales Leaders
**Focus on:**
- Time savings (hours → minutes for brand guidelines)
- Consistency across team
- Faster rep onboarding
- Learning from top performers

**Emphasize:**
- Conversation analysis showing what top reps do differently
- Anti-pattern detection
- Scalability (guidelines from 10 reps work for 100 reps)

---

### For Marketing Leaders
**Focus on:**
- Brand consistency enforcement
- Document consolidation
- Multi-channel tone adaptation
- Creative + on-brand balance

**Emphasize:**
- How it preserves brand while allowing creativity
- Adaptation by audience and medium
- Conflict detection and guidance

---

### For Operations Leaders
**Focus on:**
- Efficiency gains
- Process automation
- Quality assurance
- Integration capabilities

**Emphasize:**
- TDD approach and validation
- MCP connector integrations
- Error handling
- Performance benchmarks

---

## Handling Questions

### "How is this different from ChatGPT?"

**Answer:**
- "ChatGPT is generic. This learns YOUR brand voice"
- "Show document-specific extraction + conversation analysis"
- "ChatGPT won't catch when you're going off-brand"
- "This explains its choices—transparent, not black box"

### "What if our brand voice changes?"

**Answer:**
- "Re-run conversion anytime with updated docs"
- "Add new conversation transcripts to refine"
- "Version control built in"
- "Demonstrate updating guidelines"

### "Can sales reps override the brand guidelines?"

**Answer:**
- "Yes—it guides, doesn't block"
- "Shows options when there's conflict"
- "Explains tradeoffs"
- "Demonstrate conflict handling (TEST ENFORCE-006)"

### "How accurate is the conversation analysis?"

**Answer:**
- "Only uses actual quotes from transcripts"
- "Shows frequency data and confidence scores"
- "Flags when sample size is too small"
- "Demonstrate with confidence scores"

### "What's the learning curve?"

**Answer:**
- "Sales reps just use slash commands"
- "Guidelines automatically applied"
- "Explanations help teams learn"
- "Show simple interface"

---

## Success Metrics to Share

After demonstrating, share these target outcomes:

**Time Savings:**
- Brand guideline creation: 8 hours → 5 minutes
- Content creation: 30 minutes → 3 minutes
- Rep onboarding: 3 months → 3 weeks

**Quality Improvements:**
- Brand consistency: 60% → 95%
- Prohibited term usage: Eliminated
- On-brand content: 100% with explanations

**Business Impact:**
- Faster deal cycles (consistent messaging)
- Higher rep productivity (less content creation time)
- Better new rep ramp (learn from best practices)

---

## Next Steps After Demo

1. **Pilot Program:**
   - 10 reps for 30 days
   - Measure time savings and quality
   - Gather feedback

2. **Success Criteria:**
   - 80% adoption rate among pilot reps
   - 50% reduction in content creation time
   - 90%+ brand consistency score

3. **Timeline:**
   - Week 1: Upload brand materials
   - Week 2: Generate guidelines + train reps
   - Weeks 3-6: Pilot and measure
   - Week 7: Expand to full team

---

## Demo Checklist

**Before Demo:**
- [ ] All fixtures in place
- [ ] Plugin installed and tested
- [ ] Sample outputs verified
- [ ] Performance acceptable
- [ ] Backup plan if live demo fails

**During Demo:**
- [ ] Explain the problem first
- [ ] Show before/after clearly
- [ ] Let the tool surprise them (don't over-explain upfront)
- [ ] Highlight explanations, not just outputs
- [ ] Address objections proactively

**After Demo:**
- [ ] Share test results document
- [ ] Provide trial access if possible
- [ ] Schedule follow-up
- [ ] Send pilot proposal

---

## Troubleshooting

**If document conversion fails:**
- Check file paths are correct
- Verify documents have actual content
- Try with single document first
- Fall back to expected output example

**If guideline generation is slow:**
- Explain it's analyzing all transcripts
- Show progress if possible
- Use pre-generated output if taking too long

**If content generation seems off-brand:**
- Check which guidelines are loaded
- Verify guidelines were generated correctly
- Show the explanation—often it's on-brand but unexpected
- Use this to demonstrate refinement loop

---

## Demo Resources

**Files to Have Ready:**
- This demo script
- Test suite documentation
- Expected outputs for comparison
- Sample customer case studies
- ROI calculator

**Backup Materials:**
- Screenshots of outputs (if live demo fails)
- Video recording of successful demo
- Written testimonials from beta users

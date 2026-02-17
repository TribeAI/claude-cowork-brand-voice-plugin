# Sample Content Requests for Brand Voice Enforcement Testing

## Request 1: Cold Email
**User Input:** "Draft a cold email to a VP of Sales at a Series B SaaS company"

**Expected Elements in Output:**
- Professional but warm tone
- Research-based opener
- Specific challenge relevant to Series B companies
- Proof point with metrics
- Low-friction CTA
- Under 100 words

---

## Request 2: LinkedIn Post
**User Input:** "Write a LinkedIn post announcing our new AI forecasting feature"

**Expected Elements in Output:**
- Conversational, authentic tone
- Under 150 words
- Lead with customer benefit, not feature announcement
- Non-salesy approach
- Natural call-to-action

---

## Request 3: Pitch Deck Outline
**User Input:** "Create a 10-slide pitch deck for an enterprise prospect"

**Expected Elements in Output:**
- Bold, confident language
- Data-driven approach
- Problem-Solution-Proof structure
- Enterprise-appropriate formality
- ROI focus throughout
- Specific metrics and proof points

---

## Request 4: Follow-Up Email
**User Input:** "Write a follow-up email after a demo where the prospect seemed interested but hasn't responded in a week"

**Expected Elements in Output:**
- Helpful, non-pushy tone
- Reference to demo content
- Offer specific value/resources
- Address potential concerns
- Clear next step options

---

## Request 5: Proposal Executive Summary
**User Input:** "Draft an executive summary for a proposal to implement TribeAI for a 50-person sales team"

**Expected Elements in Output:**
- Consultative, partnership tone
- Lead with outcomes, not features
- ROI framework
- Clear implementation timeline
- Risk mitigation (pilot, guarantee)
- Collaborative language ("together", "we")

---

## Request 6: Objection Response (Price)
**User Input:** "How should I respond to a prospect who says our pricing is too high?"

**Expected Elements in Output:**
- Confident but empathetic
- ROI framework using their numbers
- Conservative projections
- De-risking options (pilot, guarantee)
- Specific math showing value
- Not defensive or apologetic

---

## Request 7: Customer Success Email
**User Input:** "Write a welcome email to a new customer who just signed"

**Expected Elements in Output:**
- Warm, organized, reassuring tone
- Clear timeline and next steps
- Team contacts provided
- Best practice tip included
- Partnership language
- Sets expectations clearly

---

## Request 8: Multi-Audience Test
**User Input:** "Write two emails about the same topic: one to a junior SDR and one to a CEO"

**Expected Elements in Output:**
- Same core brand voice in both
- SDR email: More detailed, warmer, helpful
- CEO email: Concise, high-level, time-respectful
- Both avoid jargon
- Explanation of adaptation choices

---

## Request 9: Conflict Test
**User Input:** "Write a super casual, fun email for cold outreach"

**Expected Behavior:**
- Detect conflict with "professional but warm" guideline
- Present options to user
- Recommend staying on-brand with reasoning
- Explain tradeoff if going casual
- Respect user's final choice

---

## Request 10: No Guidelines Test
**User Input:** "Draft an email using our brand voice"

**Expected Behavior (if no guidelines loaded):**
- Detect no guidelines available
- Explain situation clearly
- Offer options: convert docs, generate from calls, create template
- Do NOT generate content without guidelines

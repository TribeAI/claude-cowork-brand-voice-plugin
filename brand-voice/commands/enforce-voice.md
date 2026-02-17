---
description: Apply brand guidelines to content creation
argument-hint: "<content request>"
---

Load the user's brand guidelines and apply them to the content request provided in $ARGUMENTS.

Find brand guidelines using this sequence (stop as soon as found):
1. `.claude/brand-voice.local.md` — per-project local config
2. Session context — check if guidelines were generated earlier in this conversation
3. Notion search — look for a page titled exactly "Brand Voice Guidelines"
4. Google Drive search — look for a file named exactly "Brand Voice Guidelines"
5. If not found, ask the user to run `/brand-voice:discover-brand`, `/brand-voice:generate-guidelines`, or paste guidelines directly

Once guidelines are loaded, follow the brand-voice-enforcement skill instructions to:
1. Analyze the content request (type, audience, key messages, requirements)
2. Apply voice constants ("We Are / We Are Not") and flex tone for context (formality, energy, technical depth)
3. Generate content applying voice, tone, messaging, and terminology guidelines
4. Validate output against brand do's and don'ts
5. Present the content with a brief explanation of brand choices made
6. Note any open questions from guidelines that affect this content
7. Offer to refine based on feedback

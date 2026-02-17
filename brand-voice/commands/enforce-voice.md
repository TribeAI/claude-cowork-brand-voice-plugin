---
description: Apply brand guidelines to content creation
argument-hint: "<content request>"
---

Load the user's brand guidelines and apply them to the content request provided in $ARGUMENTS.

If no brand guidelines exist, inform the user and suggest:
1. `/brand-voice:discover-brand` to find brand materials across platforms
2. `/brand-voice:generate-guidelines` to generate from documents or transcripts

Follow the brand-voice-enforcement skill instructions to:
1. Load brand guidelines from `.claude/brand-voice.local.md`, connected Notion workspace, or session context
2. Analyze the content request (type, audience, key messages, requirements)
3. Apply voice constants ("We Are / We Are Not") and flex tone for context (formality, energy, technical depth)
4. Generate content applying voice, tone, messaging, and terminology guidelines
5. Validate output against brand do's and don'ts
6. Present the content with a brief explanation of brand choices made
7. Note any open questions from guidelines that affect this content
8. Offer to refine based on feedback

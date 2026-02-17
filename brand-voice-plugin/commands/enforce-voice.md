---
description: Apply brand guidelines to content creation
argument-hint: "<content request>"
---

Load the user's brand guidelines and apply them to the content request provided in $ARGUMENTS.

Find brand guidelines using this sequence:
1. Check if guidelines are already in the conversation context (generated earlier in this session)
2. Search Notion for a page titled "Brand Voice Guidelines"
3. Search Google Drive for a file named "Brand Voice Guidelines"
4. If not found, ask the user to paste a link, run `/brand:generate-guidelines`, or paste guidelines directly

Once guidelines are loaded, follow the brand-voice-enforcement skill instructions to:
1. Analyze the content request (type, audience, key messages, requirements)
2. Generate content applying voice, tone, messaging, and terminology guidelines
3. Validate output against brand do's and don'ts
4. Present the content with a brief explanation of brand choices made
5. Offer to refine based on feedback

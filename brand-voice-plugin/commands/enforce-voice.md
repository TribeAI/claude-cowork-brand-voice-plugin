---
description: Apply brand guidelines to content creation
argument-hint: "<content request>"
---

Load the user's brand guidelines and apply them to the content request provided in $ARGUMENTS.

If no brand guidelines exist, inform the user and suggest:
1. `/brand:convert-docs` to convert existing brand documents
2. `/brand:generate-guidelines` to generate from sales calls

Follow the brand-voice-enforcement skill instructions to:
1. Load brand guidelines from `/mnt/user-data/outputs/brand-guidelines/`, Notion, or Google Drive
2. Analyze the content request (type, audience, key messages, requirements)
3. Generate content applying voice, tone, messaging, and terminology guidelines
4. Validate output against brand do's and don'ts
5. Present the content with a brief explanation of brand choices made
6. Offer to refine based on feedback

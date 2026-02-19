---
description: Apply brand guidelines to content creation
argument-hint: "<content request>"
---

**Before doing anything else**, check whether the user has a working folder selected for this session. If there is no working folder, warn the user: "Heads up — you don't have a working folder selected. I can still apply brand voice from guidelines in this conversation, but I won't be able to load saved guidelines from a previous session. To use saved guidelines, select a working folder and re-run this command."

Load the user's brand guidelines and apply them to the content request provided in $ARGUMENTS.

Find brand guidelines using this sequence (stop as soon as found):
1. Session context — check if guidelines were generated earlier in this conversation
2. Local guidelines file — look for `brand-voice-guidelines.md` inside a `.claude/` directory. Do NOT assume relative paths resolve to the user's project; the agent may be running from a plugin cache directory. If the user's project path is known, check `<project-root>/.claude/brand-voice-guidelines.md`. Otherwise ask the user for the path.
3. If not found, ask the user to run `/brand-voice:discover-brand`, `/brand-voice:generate-guidelines`, or paste guidelines directly

Once guidelines are loaded, follow the brand-voice-enforcement skill instructions to:
1. Analyze the content request (type, audience, key messages, requirements)
2. Apply voice constants ("We Are / We Are Not") and flex tone for context (formality, energy, technical depth)
3. Generate content applying voice, tone, messaging, and terminology guidelines
4. Validate output against brand do's and don'ts
5. Present the content with a brief explanation of brand choices made
6. Note any open questions from guidelines that affect this content
7. Offer to refine based on feedback

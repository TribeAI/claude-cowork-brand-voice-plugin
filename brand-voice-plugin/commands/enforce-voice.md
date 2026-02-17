# /brand:enforce-voice Command

## Command
`/brand:enforce-voice`

## Description
Explicitly invoke the Brand Voice Enforcement skill to apply existing brand guidelines to content creation.

## Usage
```
/brand:enforce-voice [content request]
```

## Examples

### Example 1: Cold Email
```
/brand:enforce-voice
Draft a cold email to a VP of Sales at a Series B SaaS company
```

### Example 2: Pitch Deck
```
/brand:enforce-voice
Create a 10-slide pitch deck for an enterprise prospect
```

### Example 3: LinkedIn Post
```
/brand:enforce-voice
Write a LinkedIn post announcing our new AI feature
```

### Example 4: Proposal
```
/brand:enforce-voice
Write a proposal for implementing our AI platform at a Fortune 500 company
```

## What Happens
1. Loads existing brand guidelines from configured locations
2. Analyzes the content request and determines appropriate tone
3. Generates content following brand voice, messaging, and style guidelines
4. Provides explanation of brand choices made
5. Offers refinement options

## Requirements
- Brand guidelines must exist (either from document conversion or guideline generation)
- If no guidelines exist, will prompt user to create them first

## Related Commands
- `/brand:convert-docs` - Convert brand documents to guidelines
- `/brand:generate-guidelines` - Generate guidelines from conversations

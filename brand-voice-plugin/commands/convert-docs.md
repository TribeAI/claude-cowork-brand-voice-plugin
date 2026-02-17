# /brand:convert-docs Command

## Command
`/brand:convert-docs`

## Description
Convert scattered brand documents (PDFs, PowerPoints, Google Docs) into a unified, LLM-ready brand guidelines document.

## Usage
```
/brand:convert-docs [document paths or folder]
```

## Examples

### Example 1: Convert Specific Files
```
/brand:convert-docs
Convert the style guide, pitch deck, and email templates into brand guidelines
```

### Example 2: Convert From Folder
```
/brand:convert-docs
Process all brand documents in my "Brand 2024" Google Drive folder
```

### Example 3: Convert Uploaded Files
```
/brand:convert-docs
I just uploaded 3 brand documents. Please convert them to guidelines.
```

### Example 4: Update Existing Guidelines
```
/brand:convert-docs
Add this new positioning document to our existing brand guidelines
```

## What Happens
1. Discovers and ingests brand documents from specified locations
2. Extracts brand elements (voice attributes, tone, messaging, terminology, examples)
3. Organizes content into structured Markdown format
4. Handles conflicts and deduplication across multiple documents
5. Assigns confidence scores to each section
6. Saves output to `/mnt/user-data/outputs/brand-guidelines/`
7. Optionally syncs to Notion or Google Drive
8. Notifies when complete and ready for use

## Supported Formats
- PDF, PowerPoint, Word Documents
- Google Docs, Google Slides
- Markdown, plain text
- Images with text (OCR)

## Output
Structured brand guidelines document including:
- Core voice attributes
- Tone guidelines by content type
- Messaging framework
- Terminology (preferred/prohibited)
- Content examples
- Source attribution and confidence scores

## Related Commands
- `/brand:enforce-voice` - Use generated guidelines for content creation
- `/brand:generate-guidelines` - Generate guidelines from conversations instead

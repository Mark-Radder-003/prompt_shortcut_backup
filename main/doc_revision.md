# Document Revision Prompt Template

## Purpose
AI-friendly template for systematic document comparison and revision generation.

## Standard Prompt Format

### Basic Revision Request
```
@_prompt/doc_revision.md

Compare these two documents:
@doc/{DOCUMENT_NAME}_v{OLD_VERSION}_{TIMESTAMP}.md
@doc/{DOCUMENT_NAME}_v{CURRENT_VERSION}_{TIMESTAMP}.md

Important: **The latest version contains my modification feedback**

Please analyze differences and generate the next improved version.
```

## Template Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `{DOCUMENT_NAME}` | Document type abbreviation | `sdd`, `api`, `req`, `test` |
| `{OLD_VERSION}` | Previous version number | `1`, `2`, `3` |
| `{CURRENT_VERSION}` | Current version number | `2`, `3`, `4` |
| `{TIMESTAMP}` | Creation timestamp | `202507161545` |


## AI Processing Instructions

### Step 1: Document Analysis
1. Read both document versions completely
2. Identify all content and structural differences
3. Extract user modification intentions
4. Note improvements, corrections, and new requirements

### Step 2: Comparison Analysis
- Content additions and deletions
- Structural reorganizations  
- Technical accuracy improvements
- Clarity and readability enhancements
- User feedback integration points
- New constraints or requirements

### Step 3: Next Version Generation
- Incorporate all user modifications
- Improve document quality and completeness
- Enhance clarity and organization
- Maintain consistent formatting
- Address identified gaps
- Follow project documentation standards

## Rules and Output Requirements

**File Management:**
- **Output Location**: Save to `doc/` folder in project root
- **Naming Convention**: `{TYPE}_v{NEXT_VERSION}_{NEW_TIMESTAMP}.md`
- **Version Increment**: Automatically increment version number
- **Timestamp**: Generate new timestamp for created version

**Quality Standards:**
- Address all user feedback points
- Improve readability and structure
- Maintain technical accuracy
- Ensure project consistency
- Add missing information from comparison

## Quick Reference Templates

### Minimal Usage
```
@_prompt/doc_revision.md

@doc/{document}_v{old}.md
@doc/{document}_v{current}.md

Latest has my feedback. Generate next version.
```

### Standard Usage
```
@_prompt/doc_revision.md

Compare:
@doc/{document}_v{old}_{timestamp}.md
@doc/{document}_v{current}_{timestamp}.md

The latest version contains my modification feedback.
Generate improved next version.
```

### Detailed Usage
```
@_prompt/doc_revision.md

Task: Document revision with focus on [specific areas]

Documents:
- Previous: @doc/{document}_v{old}_{timestamp}.md  
- Current: @doc/{document}_v{current}_{timestamp}.md

Focus: Latest version includes user modifications and feedback
Output: Generate enhanced next version incorporating all improvements
```
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a prompt template repository containing reusable templates and guides for interacting with LLMs, specifically optimized for Claude Code and other AI coding assistants. The templates focus on document generation, revision workflows, and git worktree setup for AI-integrated development.

## Key Files and Their Purpose

### Core Templates
- **doc_naming.md**: Template for generating consistently named documentation files with timestamps
- **doc_revision.md**: Workflow template for iterative document improvement using AI comparison and revision
- **readme_multilanguage_template.md**: Template for creating multi-language README files with language switchers
- **git_worktree_setup_guide.md**: Comprehensive guide for setting up git worktrees optimized for AI assistants (v4.0)

### Archive Templates
- **archive/claude_code_prompt_tmp.md**: Comprehensive LLM prompt engineering guide based on Anthropic's best practices
- **archive/doc_naming_cn.md**: Chinese translation of the doc_naming template
- **archive/reference_summary_template.md**: Template for creating technical reference summaries from web sources

## Common Commands

### Document Generation
When generating documents using the naming template:
```bash
# Get current timestamp for document naming
date +"%Y%m%d%H%M%S"
```

### Git Submodule Management
To add or manage the prompt alias submodule:
```bash
# Add submodule
git submodule add https://github.com/Mark-Radder-003/prompt_shortcut_backup.git _prompt_alias

# Commit submodule setup
git add .gitmodules _prompt_alias
git commit -m "Add prompt alias as submodule"

# Update submodule
git submodule update --remote --merge
```

## Document Generation Workflow

1. **Document Naming Convention**: `{TYPE}_v{VERSION}_{TIMESTAMP}.md`
   - Types: `sdd` (System Design), `api`, `req` (Requirements), `test`, `deploy`
   - Save to `doc/` folder within the project
   - Always use bash to get current timestamp

2. **Document Revision Process**:
   - Compare two versions (old and current) where current contains user feedback
   - Generate next version incorporating all improvements
   - Maintain version incrementing and new timestamps

3. **Multi-language README Creation**:
   - Add language switcher at the top of all README files
   - Create language-specific files (e.g., `README_ja.md` for Japanese)
   - Preserve original formatting and structure

## Critical Guidelines for Git Worktree Operations

**MANDATORY**: When working with git worktrees, **ALWAYS use filesystem MCP server for ALL file operations**. 
- **NEVER use bash commands** like `cd`, `ls`, `mkdir`, `cp`, `mv`, `rm` for file operations
- **ALWAYS use absolute paths** with filesystem MCP functions
- This is critical for proper path resolution and avoiding errors

Example:
- ❌ WRONG: `cd /path/to/worktree`
- ✅ CORRECT: `mcp__filesystem__list_directory(path="/path/to/worktree")`

## Template Usage Patterns

### Using Templates with @ Reference
Templates are designed to be referenced using the `@` syntax:
```
@_prompt/doc_naming.md
TYPE = 'api'
VERSION = '1'
```

### Template Variables
Common variables used across templates:
- `{TYPE}`: Document type abbreviation
- `{VERSION}`: Version number
- `{TIMESTAMP}`: Creation timestamp (YYYYMMDDHHSS)
- `{PROJECT_NAME}`: Project identifier
- `{TOPIC}`: Subject matter for reference summaries

## Important Notes

1. **File Operations**: Always prefer filesystem MCP server operations over bash commands when working with files
2. **Timestamps**: Use `date +"%Y%m%d%H%M%S"` to generate timestamps for document naming
3. **Document Storage**: Generated documents should be saved to `doc/` folder within projects
4. **Version Control**: The repository uses git worktree structure - always start Claude Code from worktree directories, not bare repo
5. **Path References**: Use absolute paths for cross-worktree references to avoid resolution issues
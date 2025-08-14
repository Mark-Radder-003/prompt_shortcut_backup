# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## ⚠️ Important Guidelines for Dynamic Content

**CRITICAL: Always Read Files Fresh**
- This is a dynamic prompt management repository - all template files change frequently
- **Never memorize or cache template content details** across sessions
- **Always use Read tool** to examine current template structure before use
- Template variables, formats, and content may be completely different between sessions
- Treat all template descriptions as potentially outdated - verify current state

## Repository Overview

This repository is a **dynamic prompt management system** containing evolving templates and documentation generation tools for AI-assisted development workflows. It serves as a centralized, ever-changing template library linked across multiple projects via symbolic links.

**Key Characteristics:**
- **Highly Dynamic**: Template content, variables, and formats change frequently
- **No Permanence**: Files are experimental and subject to complete restructuring
- **Fresh Reading Required**: Always examine current file state rather than relying on documentation
- **Template Evolution**: Expect different structures, variables, and workflows between sessions

## Architecture & Structure

### Core Concept
- **Single Source of Truth**: Templates are maintained centrally and shared across projects via symbolic links
- **Template-Driven Workflow**: Standardized prompt templates for consistent AI interactions
- **Multi-language Support**: Documentation available in English and Japanese

### Directory Organization
```
├── main/                    # Primary template directory (keep at one level depth as specified)
│   └── [various .md files] # Template files (content and filenames change frequently)
├── _archive/               # Archived templates and reference materials  
│   └── [various .md files] # Historical templates (may be outdated)
├── README.md              # English documentation
└── README_ja.md           # Japanese documentation
```

## Template Usage Approach

### Working with Unknown Templates
- **⚠️ Always discover templates fresh** - Use `ls` or `Glob` to see what template files currently exist
- **⚠️ Read each file directly** before use - Template content, structure, and purpose may be completely different
- **No assumptions** - Don't assume what any template does based on filename or previous sessions  
- **Fresh discovery** - Approach each template file as if encountering it for the first time

### Generic Usage Pattern
1. **Discover**: Use `ls main/` to see what template files currently exist
2. **Read**: Use Read tool to examine the specific template file content
3. **Understand**: Analyze current structure, variables, and requirements
4. **Use**: Reference with `@_prompt/filename.md` syntax based on current file state

### Symbolic Link Strategy

**Primary Workflow**:
```bash
# From target project directory
ln -s ~/Documents/001_git_projects/_prompt/main _prompt_alias

# Usage in prompts  
@_prompt_alias/[current_filename].md
```

**Benefits**:
- Single point of maintenance across all projects
- Automatic template updates propagate to all linked projects
- Consistent versioning and no duplication
- Guaranteed consistency across development environments

## Working with Dynamic Templates

### Fresh Reading Protocol
1. **Always Read First**: Use Read tool on template file before any usage
2. **Verify Current Structure**: Examine current variable placeholders and format requirements  
3. **Don't Assume Consistency**: Template structure may be completely different from previous sessions
4. **Validate Before Use**: Confirm current template parameters match your intended usage

### Dynamic Template Usage Pattern
1. Create symbolic link to `main/` directory in target project
2. **Read template file** to understand current structure and variables
3. Reference templates using `@_prompt/[actual_filename].md` syntax
4. Provide variables as **currently defined in the template** (not from memory)
5. Follow current template specifications for output location and format

### Adaptive Workflow Cycle
1. **Read current template** to understand latest workflow
2. Execute current template requirements
3. Expect template evolution - re-read on subsequent uses
4. Adapt to new template structures as they evolve

## Best Practices

### Dynamic Content Guidelines
- **Never Cache Template Details**: Always read template files fresh each session
- **Expect Evolution**: Template structure, variables, and formats change frequently
- **Validate Current State**: Check template content before use, not after
- **No Memory Dependencies**: Don't rely on template descriptions from previous sessions
- **Fresh Approach**: Treat each template interaction as discovering it for the first time

### When Working with This Repository
- **Preserve Structure**: Keep `main/` folder at one level depth as specified
- **Read Before Use**: Always examine template files directly before referencing
- **Dynamic Adaptation**: Adjust to current template structure rather than expected structure  
- **Leverage Symbolic Links**: Avoid copying templates, use links for consistency
- **Bilingual Support**: Consider both English and Japanese documentation needs

### Template Development Awareness
- Templates are experimental and subject to complete restructuring
- Variable names, formats, and requirements may change without notice
- Usage patterns and workflows evolve between sessions
- Documentation may lag behind actual template content

## Files to Ignore

When scanning this repository, avoid analyzing the following file types and directories (as defined in `.gitignore`):

### Sensitive & Security Files
- GCP credentials and service account keys (`*.json`, `credentials.json`, etc.)
- Environment variables (`.env`, `.env.*` except examples)
- Configuration files (`config.ini`, `config.yaml`, `settings.json`, etc.)

### Build & Development Artifacts  
- Python artifacts (`__pycache__/`, `*.py[cod]`, `build/`, `dist/`, etc.)
- Virtual environments (`venv/`, `env/`, `.venv/`)
- IDE files (`.vscode/`, `.idea/`, `*.swp`)
- Log files (`*.log`, `logs/`)

### Data & Database Files
- Data files (`*.csv`, `*.xlsx`, `*.parquet`, `data/`, `datasets/`)
- Database files (`*.db`, `*.sqlite`)
- Jupyter checkpoints (`.ipynb_checkpoints`)

### Infrastructure & Cloud
- Terraform state files (`*.tfstate`, `.terraform/`)
- Docker override files (`docker-compose.override.yml`)
- Cloud storage cache (`gs_cache/`)

### System Files
- macOS system files (`.DS_Store`, `.Spotlight-V100`)
- Temporary files (`tmp/`, `temp/`, `.tmp/`)

## Template Evolution Awareness

### Understanding Template Volatility
- **Complete Restructuring**: Templates may be entirely rewritten between sessions
- **Variable Changes**: Parameter names, types, and requirements evolve continuously  
- **Workflow Evolution**: Processing steps and output specifications change frequently
- **Format Flexibility**: Document formats and naming conventions are experimental

### Session-to-Session Expectations
- **No Consistency Guarantee**: Template content may be completely different
- **Fresh Discovery Required**: Approach each template as if encountering it for the first time
- **Documentation Lag**: This CLAUDE.md may not reflect current template reality
- **Adaptive Mindset**: Be prepared to learn new template structures each session

### Working with Uncertainty
- **Embrace Change**: Template evolution is a feature, not a bug
- **Verify Everything**: Don't assume any template characteristic remains constant
- **Stay Flexible**: Adapt workflows to current template requirements
- **Document Nothing**: Avoid creating documentation that will quickly become obsolete

## Integration Notes

This repository integrates with Claude Code workflows by providing:
- **Dynamic prompt templates** for evolving AI interactions (content changes frequently)
- **Experimental workflows** for document generation and revision (subject to change)
- **Multi-project template sharing** via symbolic links (structure may evolve)
- **Bilingual documentation support** (formats and requirements may change)

The templates work with Claude Code's file referencing system using the `@path/file.md` syntax, but **always read the referenced files directly** rather than relying on cached descriptions.
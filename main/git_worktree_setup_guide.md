# Git Worktree + Claude Code Integration Guide

> ## 🚨 CRITICAL DIRECTIVE FOR AI ASSISTANTS 🚨
> **MANDATORY: When performing ANY file operations related to git worktrees:**
> - **ALWAYS use `filesystem` MCP server for ALL file operations**
> - **NEVER use bash commands like `cd`, `ls`, `mkdir`, `cp`, `mv`, `rm`**
> - **ALWAYS use absolute paths with filesystem MCP functions**
> 
> **This is NON-NEGOTIABLE. Using bash commands WILL cause path resolution failures.**
> 
> Example:
> - ❌ WRONG: `cd /path/to/worktree`
> - ✅ CORRECT: `mcp__filesystem__list_directory(path="/path/to/worktree")`

## Context & Purpose
This guide provides a comprehensive setup for git worktree structure optimized for parallel development with Claude Code and other AI coding assistants. It addresses common path resolution issues and ensures seamless integration.

### **SuperClaude Framework Integration**
This guide is integrated into the SuperClaude framework as a **global reference** accessible via:
- **Quick Reference**: `@GIT_WORKTREE.md` - Essential patterns and commands
- **Complete Guide**: `@main/git_worktree_setup_guide.md` - Full documentation
- **Memory Integration**: Knowledge stored in Claude Code memory for automatic recall
- **Auto-Activation**: Triggered by keywords: "worktree", "git worktree", "multiple branches"

### **Framework Components**
- **Personas**: DevOps persona for worktree management, Security persona for path validation
- **MCP Coordination**: Filesystem MCP (mandatory), Sequential MCP for complex git operations
- **Wave Integration**: Multi-worktree analysis for complex projects
- **Command Integration**: Works with `/build`, `/analyze`, `/troubleshoot` commands

### What This Document Provides
- ✅ **Reference documentation** for git worktree setup commands
- ✅ **Filesystem MCP operations** for AI assistants to use
- ✅ **Configuration file templates** (JSON, Markdown) for AI context
- ✅ **Best practices** for worktree management
- ✅ **Troubleshooting guidance** for common issues

### What This Document Does NOT Provide
- ❌ **Executable scripts** (.sh files) - This is documentation only
- ❌ **Automated setup** - Commands must be run manually or via AI with filesystem MCP
- ❌ **Shell scripts to save** - All code blocks are reference documentation

## ⚠️ Critical Success Factors
1. **Always start Claude Code from the worktree directory, NOT the bare repo root**
2. **Use absolute paths when referencing files across worktrees**
3. **Configure git properly for worktree-specific settings**
4. **Validate setup after each worktree creation**
5. **🚨 CRITICAL: Use filesystem MCP server for ALL file operations - NEVER use bash commands like cd, mkdir, mv**

## Required Structure
```
project-root/                         # Bare repository (NO working files here!)
├── .git/                            # Git management (bare repo)
├── main/                            # Main branch worktree
│   ├── .git                        # File pointing to ../git/worktrees/main
│   ├── src/                        # Your actual project files
│   ├── docs/                       # Documentation
│   └── README.md                   # Project readme
└── feature/                         # Feature worktrees directory
    ├── feature-01/                  # Feature worktree 1
    │   ├── .git                    # File pointing to ../../.git/worktrees/feature-01
    │   └── [project files]         # Complete project structure
    ├── feature-02/                  # Feature worktree 2
    │   ├── .git                    # File pointing to ../../.git/worktrees/feature-02
    │   └── [project files]         # Complete project structure
    └── feature-03/                  # Feature worktree 3
        ├── .git                    # File pointing to ../../.git/worktrees/feature-03
        └── [project files]         # Complete project structure
```

## Complete Setup Process

### 1. Initial Repository Setup (Human One-Time Action)

**⚠️ These are git commands that humans must run initially. AI cannot create git repositories.**

```bash
# Create project directory
mkdir my-project && cd my-project

# Initialize as bare repository
git init --bare
# OR convert existing repo to bare
git config --bool core.bare true

# Verify bare status
git config core.bare  # Should output: true
```

### 2. Create Main Worktree (Human One-Time Action)

**⚠️ Git worktree commands must be run by humans. AI should use filesystem MCP after worktrees are created.**

```bash
# From the bare repo root
git worktree add main main

# If main branch doesn't exist yet
git worktree add -b main main HEAD

# Verify worktree creation
git worktree list
```

### 3. Configure Worktree-Specific Settings (Git Commands)

**Reference commands for git configuration:**

```bash
# Enable worktree-specific configuration
git config extensions.worktreeConfig true

# In each worktree, configure user settings if needed
# (Run from within the worktree directory)
git config --worktree user.name "Your Name"
git config --worktree user.email "your.email@example.com"
```

### 4. Create Feature Worktrees

**For Humans (git commands):**
```bash
# Add feature worktrees from bare repo root
git worktree add feature/feature-01 -b feature-01
git worktree add feature/feature-02 -b feature-02
git worktree add feature/feature-03 -b feature-03
```

**For AI (after worktrees exist):**
```python
# Create feature directory if needed
mcp__filesystem__create_directory(path="/path/to/project/feature")

# Access worktree files
mcp__filesystem__list_directory(path="/path/to/project/feature/feature-01")
```

## 🚨 CRITICAL: File Operations with Filesystem MCP Server

### ⚠️ MANDATORY: Use Filesystem MCP for ALL File Operations

**When working with git worktrees, AI assistants MUST use the filesystem MCP server for ALL file operations.**

#### ❌ NEVER Use Bash Commands for File Operations:
```bash
# DON'T DO THIS - These bash commands cause path resolution issues:
cd /path/to/worktree        # ❌ WRONG
mkdir feature               # ❌ WRONG  
mv file1 file2              # ❌ WRONG
cp source dest              # ❌ WRONG
rm file                     # ❌ WRONG
ls -la                      # ❌ WRONG
```

#### ✅ ALWAYS Use Filesystem MCP Server:
```
# CORRECT - Use filesystem MCP operations:
mcp__filesystem__list_directory         # List files
mcp__filesystem__create_directory       # Create directories
mcp__filesystem__move_file              # Move/rename files
mcp__filesystem__read_file              # Read file contents
mcp__filesystem__write_file             # Write file contents
mcp__filesystem__get_file_info          # Get file metadata
```

### Why This Is Critical
1. **Path Resolution**: Filesystem MCP maintains correct absolute paths
2. **Context Preservation**: MCP operations preserve worktree context
3. **Error Prevention**: Avoids "file not found" and wrong directory errors
4. **Consistency**: Ensures all operations use the same path resolution logic

### Common Filesystem MCP Operations for Worktrees

| Operation | Filesystem MCP Function | Example |
|-----------|------------------------|----------|
| Navigate to worktree | `list_directory` | List `/Users/username/project/main` |
| Create feature dir | `create_directory` | Create `/Users/username/project/feature` |
| Check worktree files | `list_directory` | List current worktree path |
| Read config | `read_file` | Read `.claude-config.json` |
| Write context | `write_file` | Write `.ai-context/worktree-map.md` |
| Move files | `move_file` | Move between worktrees with full paths |
| Get file info | `get_file_info` | Check if path exists and permissions |

### Example: Navigating Worktrees with Filesystem MCP

```python
# Instead of: cd /path/to/project/main
# Use:
mcp__filesystem__list_directory(path="/Users/username/project/main")

# Instead of: mkdir -p feature/feature-01  
# Use:
mcp__filesystem__create_directory(path="/Users/username/project/feature/feature-01")

# Instead of: ls -la
# Use:
mcp__filesystem__list_directory_with_sizes(path=".")
```

## SuperClaude Command Integration

### **Using with SuperClaude Commands**

**Git Worktree Analysis**:
```bash
# Analyze worktree structure and health
/analyze --focus architecture @main/git_worktree_setup_guide.md

# Deep analysis with validation
/analyze --think-hard --validate "git worktree structure"
```

**Building with Worktrees**:
```bash
# Build across multiple worktrees
/build --scope project --delegate folders

# Validate worktree setup during build
/build --validate --persona-devops
```

**Troubleshooting Worktree Issues**:
```bash
# Investigate worktree problems
/troubleshoot "git worktree path errors" --think --seq

# Security analysis of worktree permissions
/troubleshoot --persona-security --focus security
```

### **Auto-Activation Examples**
When you mention these patterns, this guide automatically activates:

| User Input | Auto-Activation | Framework Response |
|------------|-----------------|-------------------|
| "git worktree setup" | ✅ | References @GIT_WORKTREE.md + DevOps persona |
| "multiple git branches" | ✅ | Filesystem MCP enforcement + path validation |
| "parallel development" | ✅ | Wave mode for multi-worktree analysis |
| "path resolution errors" | ✅ | Security persona + troubleshooting patterns |

### **Memory Integration Usage**
The SuperClaude framework automatically recalls:
- Filesystem MCP operation patterns
- Common worktree troubleshooting solutions
- Cross-worktree file operation templates
- Validation checklists and best practices

Access stored knowledge:
```bash
# Query memory for worktree patterns
/search "git worktree filesystem MCP operations"

# Recall troubleshooting procedures
/recall "worktree path resolution errors"
```

## Claude Code Integration Best Practices

### Starting Claude Code Sessions

#### ✅ CORRECT: Start from Worktree Directory

**IMPORTANT**: When AI assistants need to access worktree files, they should use filesystem MCP, not bash navigation:

```
# For AI Assistants - Use filesystem MCP:
mcp__filesystem__list_directory(path="/path/to/project-root/main")
mcp__filesystem__read_file(path="/path/to/project-root/main/src/file.js")

# For humans starting Claude Code (one-time setup only):
# Navigate to specific worktree FIRST
# Then start Claude Code from there
claude-code /path/to/project-root/main
```

#### ❌ INCORRECT: Starting from Bare Repo
```bash
# DON'T DO THIS - Will cause path resolution issues
cd /path/to/project-root
claude-code .
```

### Path Reference Strategies

#### 1. Use Absolute Paths for Cross-Worktree References
```bash
# Good: Absolute path
/Users/username/project-root/main/src/file.js
/Users/username/project-root/feature/feature-01/src/file.js

# Bad: Relative path from wrong context
../main/src/file.js  # May fail if context is unclear
```

#### 2. Navigation Reference (For Documentation Only)

**For Humans**: Add these aliases to your `.bashrc` or `.zshrc`:
```bash
# Quick navigation aliases
alias wt-main='cd /path/to/project-root/main'
alias wt-list='git worktree list --verbose'
alias wt-feature='cd /path/to/project-root/feature'
```

**For AI Assistants**: Use filesystem MCP to navigate:
```python
# List worktrees (AI should use git command for worktree info)
# Then use filesystem MCP for file operations:
mcp__filesystem__list_directory(path="/path/to/project-root/main")
mcp__filesystem__read_file(path="/path/to/project-root/main/.claude-config.json")
```

#### 3. Create Enhanced `.claude-config.json` in Each Worktree
```json
{
  "project_name": "my-project",
  "ai_context_version": "2.0",
  "bare_repo": "/Users/username/project-root",
  "worktrees": {
    "main": {
      "path": "/Users/username/project-root/main",
      "branch": "main",
      "status": "active",
      "last_accessed": "2024-08-08T15:00:00Z"
    },
    "feature-01": {
      "path": "/Users/username/project-root/feature/feature-01",
      "branch": "feature/user-auth",
      "status": "active",
      "last_accessed": "2024-08-08T14:30:00Z"
    },
    "feature-02": {
      "path": "/Users/username/project-root/feature/feature-02",
      "branch": "feature/payment",
      "status": "locked",
      "last_accessed": "2024-08-07T10:00:00Z"
    }
  },
  "ai_instructions": "Always use absolute paths from worktrees object above. This is the source of truth for path resolution."
}
```

#### 4. Create AI Context Documentation
Create `.ai-context/worktree-map.md` in the bare repo root for AI to understand the exact folder structure:

```markdown
# Worktree Path Mapping for AI Context

## Project: [Your Project Name]
**Last Updated**: [Update timestamp when changes occur]
**Purpose**: This document helps AI assistants understand the exact local folder structure

## Active Worktrees
| Branch | Worktree Path | Status | Description |
|--------|--------------|--------|-------------|
| main | /Users/username/project-root/main | active | Main development branch |
| feature-01 | /Users/username/project-root/feature/feature-01 | active | User authentication feature |
| feature-02 | /Users/username/project-root/feature/feature-02 | locked | Payment integration |
| feature-03 | /Users/username/project-root/feature/feature-03 | prunable | Abandoned feature |

## Quick Navigation
- **Current Working Directory**: [Run `pwd` and update here]
- **Project Root (Bare)**: /Users/username/project-root
- **Active Development**: /Users/username/project-root/main
- **Feature Branches**: /Users/username/project-root/feature/

## Path Resolution Rules for AI
1. **ALWAYS use filesystem MCP server for ALL file operations**
2. Never assume relative paths - always use absolute paths from this document
3. When user references a file, check the worktree path first using filesystem MCP
4. Cross-worktree references must use full absolute paths with filesystem MCP
5. This document is the source of truth for all path resolutions
6. **NEVER use bash commands (cd, ls, mkdir, etc.) for file operations**

## Git Worktree Status
```bash
# Output of: git worktree list --verbose
/Users/username/project-root       (bare)
/Users/username/project-root/main  abc123 [main]
/Users/username/project-root/feature/feature-01  def456 [feature/user-auth]
/Users/username/project-root/feature/feature-02  ghi789 [feature/payment] locked
```
```

### Session Management Tips

1. **Clear Context When Switching Worktrees**
   
   **For AI Assistants**: Use filesystem MCP to access different worktrees:
   ```python
   # Access files from different worktree using filesystem MCP:
   mcp__filesystem__read_file(path="/path/to/project-root/feature/feature-01/src/file.js")
   ```
   
   **For Humans**: End current session and start new one from target worktree:
   ```bash
   # Human action only - start new session from target worktree
   claude-code /path/to/project-root/feature/feature-01
   ```

2. **Use Worktree-Specific Terminal Sessions**
   - Open separate terminal tabs/windows for each worktree
   - Label them clearly (e.g., "MAIN", "FEATURE-01")
   - Keep working directory consistent within each session

3. **Document Current Context**
   Create `CURRENT_WORK.md` in each worktree:
   ```markdown
   # Current Work Context
   
   **Worktree**: feature-01
   **Branch**: feature/user-authentication
   **Base Path**: /Users/username/project-root/feature/feature-01
   **Status**: Active development
   **Related Issues**: #123, #124
   ```

## Common Issues & Solutions

### Issue 1: Claude Code Can't Find Files
**Symptoms**: "File not found" errors, incorrect path suggestions

**Root Causes**:
- Started Claude Code from bare repository root
- Cached session state from different worktree
- Relative path confusion

**Solutions**:
```python
# 1. For AI: Verify worktree path using filesystem MCP
mcp__filesystem__get_file_info(path="/path/to/project-root/main")
mcp__filesystem__list_directory(path="/path/to/project-root/main")

# 2. For AI: Access files using absolute paths with filesystem MCP
mcp__filesystem__read_file(path="/path/to/project-root/main/src/file.js")

# 3. For Humans: Start fresh Claude Code session from correct worktree
# (One-time human action only)
claude-code /absolute/path/to/worktree
```

### Issue 2: Git Commands Fail or Show Wrong Status
**Symptoms**: Git status shows unexpected results, commits go to wrong branch

**Root Causes**:
- Git context pointing to bare repository
- Worktree configuration issues

**Solutions**:
```bash
# 1. Verify git worktree status
git worktree list

# 2. Check current git directory
git rev-parse --git-dir

# 3. Repair worktree if needed
git worktree repair

# 4. Ensure you're in worktree directory
cd $(git rev-parse --show-toplevel)
```

### Issue 3: Cross-Worktree File References Fail
**Symptoms**: Can't reference files from other worktrees

**Root Cause**: Using bash commands instead of filesystem MCP

**Solutions for AI Assistants**:
```python
# 1. Use absolute paths with filesystem MCP
mcp__filesystem__read_file(path="/path/to/project-root/main/config.json")

# 2. List files in other worktrees
mcp__filesystem__list_directory(path="/path/to/project-root/feature/feature-01")

# 3. Copy files between worktrees
source_content = mcp__filesystem__read_file(path="/path/to/project-root/main/shared/config.json")
mcp__filesystem__write_file(
    path="/path/to/project-root/feature/feature-01/config.json",
    content=source_content
)
```

**Note for Humans**: Symbolic links can be created manually if needed for persistent shared resources.

### Issue 4: Confusion About Bare Repository Location
**Symptoms**: Creating worktrees in wrong directory structure, unclear about where bare repo should be

**Root Causes**:
- Misunderstanding that project root should be the bare repository
- Attempting to create bare repo in subdirectory
- Not recognizing the flat structure requirement

**Solutions**:
```bash
# CORRECT Structure:
project-root/              # ← This IS the bare repository
├── .git/                 # Git internal files
├── main/                 # Worktree for main branch
├── worktrees/           # Optional: group feature worktrees
│   ├── feature-1/       # Feature worktree
│   └── feature-2/       # Another worktree
└── [NO working files here!]

# INCORRECT Structure:
project-root/
├── src/                  # ❌ Working files in bare repo
├── bare-repo/           # ❌ Bare repo in subdirectory
│   └── .git/
└── worktrees/
```

**Key Understanding**: The project root directory itself becomes the bare repository - it should contain ONLY .git/ and worktree directories, no working files.

### Issue 5: Unnecessary Permission Assumptions
**Symptoms**: AI assistants believing they need parent directory access to convert current directory to bare repo

**Root Causes**:
- Incorrect assumption that converting to bare requires parent access
- Misunderstanding of git config operations
- Over-complication of simple operations

**Solutions**:
```bash
# Converting current directory to bare - NO parent access needed:
cd /path/to/project
git config --bool core.bare true  # Works on current directory

# AI assistants should understand:
# - Current directory operations don't need parent access
# - Git config modifies .git/config in current directory
# - File backup/restore can use subdirectories
```

### Issue 6: Converting Existing Repository with Working Files
**Symptoms**: Existing repository has working files that need to be preserved when converting to bare

**Root Causes**:
- Repository already contains code and needs restructuring
- Need to preserve git history while changing structure
- Complex transition from regular to bare+worktree setup

**Solutions**:

**Step-by-Step Conversion Process**:
```bash
# 1. Backup existing files (AI should use filesystem MCP)
mkdir temp_backup
mv * temp_backup/ 2>/dev/null
mv .* temp_backup/ 2>/dev/null

# 2. Convert to bare repository
git config --bool core.bare true

# 3. Create main worktree
git worktree add main main

# 4. Restore files to main worktree
mv temp_backup/* main/
mv temp_backup/.* main/ 2>/dev/null
rmdir temp_backup

# 5. Create additional worktrees as needed
git worktree add worktrees/feature-1 -b feature-1
```

**For AI Assistants using Filesystem MCP**:
```python
# 1. Create backup directory
mcp__filesystem__create_directory(path="/path/to/project/temp_backup")

# 2. Move files to backup (iterate through directory listing)
files = mcp__filesystem__list_directory(path="/path/to/project")
for file in files:
    if file not in ['.git', 'temp_backup']:
        mcp__filesystem__move_file(
            source=f"/path/to/project/{file}",
            destination=f"/path/to/project/temp_backup/{file}"
        )

# 3. After worktree creation, restore files
backup_files = mcp__filesystem__list_directory(path="/path/to/project/temp_backup")
for file in backup_files:
    mcp__filesystem__move_file(
        source=f"/path/to/project/temp_backup/{file}",
        destination=f"/path/to/project/main/{file}"
    )
```

## Validation Checklist

### Manual Validation Steps (Reference Documentation)

After setting up each worktree, validate using these checks:

#### For Humans - Git Commands to Run:
```bash
# 1. List all worktrees
git worktree list --verbose

# 2. Check current branch
git branch --show-current

# 3. Verify git directory
git rev-parse --git-dir

# 4. Check worktree status
git status
```

#### For AI Assistants - Filesystem MCP Validation:
```python
# 1. Check if .git file exists (indicates worktree)
mcp__filesystem__get_file_info(path="/path/to/worktree/.git")

# 2. Read .git file to verify it points to correct location
mcp__filesystem__read_file(path="/path/to/worktree/.git")

# 3. Verify project files exist
mcp__filesystem__list_directory(path="/path/to/worktree")

# 4. Check for typical project markers
mcp__filesystem__get_file_info(path="/path/to/worktree/README.md")
mcp__filesystem__get_file_info(path="/path/to/worktree/package.json")
mcp__filesystem__get_file_info(path="/path/to/worktree/src")
```

#### Validation Checklist:
- [ ] Worktree appears in `git worktree list`
- [ ] `.git` file exists and points to correct bare repo
- [ ] Can read and write files in worktree
- [ ] Git commands work correctly from worktree
- [ ] Project files are present

## Essential Commands Reference

### Worktree Management
```bash
# List all worktrees with details
git worktree list --verbose

# Add new worktree with new branch
git worktree add <path> -b <new-branch>

# Add worktree tracking remote branch
git worktree add --track -b <branch> <path> <remote>/<branch>

# Remove worktree (clean removal)
git worktree remove <path>

# Remove worktree (force)
git worktree remove --force <path>

# Clean up stale worktree entries
git worktree prune

# Lock worktree (prevent accidental removal)
git worktree lock <path> --reason "Active development"

# Unlock worktree
git worktree unlock <path>

# Move worktree to new location
git worktree move <source> <destination>

# Repair worktree administrative files
git worktree repair
```

### Navigation Helpers

#### For AI Assistants (Using Filesystem MCP):
```python
# List main worktree contents
mcp__filesystem__list_directory(path="/path/to/project-root/main")

# List feature directory
mcp__filesystem__list_directory(path="/path/to/project-root/feature")

# Get worktree information
mcp__filesystem__get_file_info(path="/path/to/project-root/main/.git")
```

#### For Humans (Shell Aliases - One-time setup only):
```bash
# Go to main worktree
alias cdmain='cd /path/to/project-root/main'

# Go to feature directory
alias cdfeature='cd /path/to/project-root/feature'

# List and select worktree interactively (requires fzf)
function cdworktree() {
    local selected=$(git worktree list | fzf | awk '{print $1}')
    [ -n "$selected" ] && cd "$selected"
}
```

## Advanced Configuration

### Worktree-Specific Git Hooks
```bash
# Enable worktree config
git config extensions.worktreeConfig true

# Set worktree-specific hooks
cd /path/to/worktree
git config --worktree core.hooksPath .githooks

# Create worktree-specific hooks directory
mkdir .githooks
# Add your hooks here
```

### Shared Configuration Across Worktrees

**Documentation: Standard Worktree Configuration**

For each new worktree, apply these configurations:

1. **Git Configuration** (run these git commands):
```bash
git config --worktree pull.rebase true
git config --worktree push.default current
```

2. **Directory Structure** (AI should use filesystem MCP):
```python
# AI: Create standard directories using filesystem MCP
mcp__filesystem__create_directory(path="/path/to/worktree/.vscode")
mcp__filesystem__create_directory(path="/path/to/worktree/tmp")
mcp__filesystem__create_directory(path="/path/to/worktree/logs")
```

3. **Shared Settings** (store in `.ai-context/shared-settings.json`):
```json
{
  "vscode_settings": { /* your settings */ },
  "git_config": {
    "pull.rebase": true,
    "push.default": "current"
  }
}
```

## Troubleshooting Decision Tree

```
Claude Code can't find files?
├── Is AI using filesystem MCP for ALL file operations?
│   ├── No → 🚨 STOP! Switch to filesystem MCP immediately
│   └── Yes → Continue
├── Are you using absolute paths with filesystem MCP?
│   ├── No → Use absolute paths: mcp__filesystem__read_file(path="/full/path")
│   └── Yes → Continue
├── Is Claude Code session started from correct worktree?
│   ├── No → Human: Restart Claude Code from worktree directory
│   └── Yes → Continue
├── Can filesystem MCP access the worktree path?
│   ├── No → Check permissions with mcp__filesystem__get_file_info
│   └── Yes → Continue
├── Is git worktree intact?
│   ├── No → Run: git worktree repair (git command OK for worktree management)
│   └── Yes → Check .git file content with mcp__filesystem__read_file
└── Still having issues?
    └── Verify filesystem MCP is working correctly
```

## Best Practices Summary

1. **🚨 ALWAYS use filesystem MCP server for ALL file operations - NEVER bash commands**
2. **Always work from worktree directories, never from bare repo**
3. **Use absolute paths for cross-worktree references**
4. **Keep separate terminal sessions for each worktree**
5. **Document context in each worktree**
6. **Maintain AI context documentation (`.ai-context/worktree-map.md`)**
7. **Update `.claude-config.json` when worktree structure changes**
8. **Validate setup after creating new worktrees**
9. **Use helper scripts for navigation and setup**
10. **Configure worktree-specific settings when needed**
11. **Clean up unused worktrees regularly with `git worktree prune`**
12. **Lock important worktrees to prevent accidental deletion**
13. **Use consistent naming conventions for feature worktrees**
14. **Train AI assistants to exclusively use filesystem MCP for file access**

## Quick Start Guide

### Initial Worktree Setup Commands (Reference Documentation)

**⚠️ NOTE**: These are reference commands for humans to run manually. AI assistants should use filesystem MCP for all file operations after initial setup.

#### Step 1: Create Bare Repository (Human Action)
```bash
# Create project directory and initialize bare repo
mkdir my-project
cd my-project
git init --bare
git config extensions.worktreeConfig true
```

#### Step 2: Create Main Worktree (Human Action)
```bash
# Add main worktree
git worktree add main -b main
```

#### Step 3: Initial Commit (Human Action)
```bash
# Navigate to main worktree and create initial commit
cd main
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
cd ..
```

#### Step 4: Create Feature Directory (AI Can Do This)

**For Humans**:
```bash
mkdir feature
```

**For AI Assistants**:
```python
# Use filesystem MCP to create feature directory
mcp__filesystem__create_directory(path="/path/to/project/feature")
```

#### Step 5: Create Documentation Files (AI Should Do This)

**AI Assistants should create these documentation files using filesystem MCP**:

```python
# Create .claude-config.json
config_content = '''{
  "project_name": "my-project",
  "bare_repo": "/path/to/project",
  "worktrees": {
    "main": {
      "path": "/path/to/project/main",
      "branch": "main",
      "status": "active"
    }
  }
}'''
mcp__filesystem__write_file(
    path="/path/to/project/main/.claude-config.json",
    content=config_content
)

# Create .ai-context/worktree-map.md
mcp__filesystem__create_directory(path="/path/to/project/.ai-context")
map_content = '''# Worktree Path Mapping
## Project: my-project
| Branch | Path | Status |
|--------|------|--------|
| main | /path/to/project/main | active |
'''
mcp__filesystem__write_file(
    path="/path/to/project/.ai-context/worktree-map.md",
    content=map_content
)
```

---

## Recommendations for Enhancement

### 🎯 **High Impact Improvements**

#### 1. Quick Command Reference

| Task | Human Command | AI (Filesystem MCP) |
|------|---------------|---------------------|
| Create worktree | `git worktree add path branch` | N/A (git only) |
| List files | N/A | `mcp__filesystem__list_directory(path="...")` |
| Navigate | `cd path` | `mcp__filesystem__list_directory(path="...")` |
| Check status | `git worktree list` | Use git command + MCP for files |
| Create directory | `mkdir path` | `mcp__filesystem__create_directory(path="...")` |
| Move files | `mv source dest` | `mcp__filesystem__move_file(source="...", destination="...")` |
| Read files | `cat file` | `mcp__filesystem__read_file(path="...")` |
| Write files | `echo "content" > file` | `mcp__filesystem__write_file(path="...", content="...")` |

#### 2. Visual Workflow Overview

```
bare-repo/
├── .git/           # ← Git management
├── main/           # ← Worktree 1 (humans: cd here, AI: use full path)
└── feature/        # ← Worktree group
    ├── feature-01/ # ← Worktree 2 (AI: absolute paths only)
    └── feature-02/ # ← Worktree 3
```

#### 3. Real-World Integration Examples

**Scenario: Starting work on main branch**
```python
# AI Assistant workflow:
1. mcp__filesystem__list_directory(path="/Users/dev/project/main")
2. mcp__filesystem__read_file(path="/Users/dev/project/main/.claude-config.json")
3. Begin work with full context
```

**Scenario: Cross-worktree file sharing**
```python
# Copy config from main to feature branch
content = mcp__filesystem__read_file(path="/Users/dev/project/main/config.json")
mcp__filesystem__write_file(
    path="/Users/dev/project/feature/feature-01/config.json", 
    content=content
)
```

### 📊 **Medium Impact Enhancements**

#### 4. Troubleshooting Matrix

| Issue | Symptoms | Root Cause | Solution |
|-------|----------|------------|----------|
| Path errors | "File not found" | Using bash commands | Switch to filesystem MCP |
| Git confusion | Wrong branch status | Working from bare repo | Start from worktree |
| Access denied | Permission errors | Incorrect path resolution | Use absolute paths |
| Context loss | AI loses track of files | Relative path confusion | Always use absolute paths |
| Performance slow | Repeated file operations | No caching strategy | Batch MCP operations |

#### 5. Performance Optimization Guide

**Filesystem MCP Performance Tips:**
- **Batch operations** when possible - Use `read_multiple_files` for multiple reads
- **Cache directory listings** for repeated access within session
- **Use absolute paths** to avoid resolution overhead
- **Validate paths** before complex operations using `get_file_info`
- **Optimize file operations** - Read once, process multiple times

### 🔧 **Structure Improvements**

#### 6. Documentation Hierarchy

```markdown
# Git Worktree + Claude Code Guide

## Quick Start (5 minutes)
- Essential commands and setup
## Core Concepts (Understanding)
- What worktrees are and why they matter
## Setup Process (Step-by-step)
- Complete implementation guide
## Claude Code Integration (AI-specific)
- Filesystem MCP requirements and examples
## Troubleshooting (Problem resolution)
- Common issues and solutions
## Reference (Commands & patterns)
- Quick lookup tables and examples
```

#### 7. Persona-Specific Sections

- **For Developers**: Human setup commands, git workflows, terminal shortcuts
- **For AI Assistants**: Filesystem MCP operations, absolute path requirements, validation patterns
- **For Teams**: Shared worktree standards, naming conventions, collaboration patterns

## **SuperClaude Framework Cross-References**

**Related Components**:
- **@RULES.md**: Git worktree detection rules and filesystem MCP enforcement
- **@MCP.md**: Filesystem MCP server integration patterns and fallback strategies  
- **@PERSONAS.md**: DevOps and Security persona activation for worktree operations
- **@ORCHESTRATOR.md**: Auto-routing and validation for git worktree operations
- **@COMMANDS.md**: Integration with /build, /analyze, /troubleshoot commands

**Integration Patterns**:
- **Wave Mode**: Multi-worktree analysis for enterprise-scale projects
- **Task Delegation**: Parallel analysis across worktree directories
- **Quality Gates**: Validation cycles for worktree setup and operations
- **Memory Persistence**: Long-term knowledge retention across sessions

**Access Methods**:
```bash
# Framework entry point
@CLAUDE.md

# Quick reference
@GIT_WORKTREE.md  

# Complete documentation
@main/git_worktree_setup_guide.md

# Related framework components
@MCP.md @PERSONAS.md @ORCHESTRATOR.md
```

---

## Version History
- v6.0: **SUPERCLAUD FRAMEWORK INTEGRATION** - Integrated into SuperClaude framework as global reference, added command integration, auto-activation triggers, memory entities, cross-references
- v5.0: **ENHANCED REFERENCE** - Added quick reference tables, visual diagrams, real-world examples, troubleshooting matrix
- v4.0: **DOCUMENTATION-ONLY** - Removed all .sh scripts, now pure documentation with filesystem MCP operations
- v3.0: **CRITICAL UPDATE** - Mandated filesystem MCP server for ALL file operations, prohibited bash commands
- v2.1: Added AI Context documentation and enhanced `.claude-config.json` for better path resolution
- v2.0: Added comprehensive Claude Code integration guide and troubleshooting
- v1.0: Initial git worktree setup documentation
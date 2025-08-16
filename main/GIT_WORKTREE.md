# GIT_WORKTREE.md - SuperClaude Git Worktree Reference

Essential git worktree patterns and filesystem MCP operations for Claude Code integration.

## Core Directive

**🚨 MANDATORY: For ALL git worktree operations:**
- **ALWAYS use `filesystem` MCP server for ALL file operations**
- **NEVER use bash commands like `cd`, `ls`, `mkdir`, `cp`, `mv`, `rm`**
- **ALWAYS use absolute paths with filesystem MCP functions**

## Quick Reference

### Command Matrix
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

### Structure Pattern
```
bare-repo/
├── .git/           # ← Git management
├── main/           # ← Main worktree (humans: cd here, AI: absolute paths)
└── feature/        # ← Feature worktrees
    ├── feature-01/ # ← Feature branch 1
    └── feature-02/ # ← Feature branch 2
```

### Essential MCP Operations
```python
# Worktree discovery
mcp__filesystem__list_directory(path="/absolute/path/to/bare-repo")

# Context loading
mcp__filesystem__read_file(path="/absolute/path/to/main/.claude-config.json")

# Cross-worktree operations
content = mcp__filesystem__read_file(path="/path/to/main/file.js")
mcp__filesystem__write_file(path="/path/to/feature/feature-01/file.js", content=content)

# Validation
mcp__filesystem__get_file_info(path="/path/to/worktree/.git")
```

### Auto-Activation Triggers
- Keywords: "worktree", "git worktree", "multiple branches"
- Directory patterns: `project/main/`, `project/feature/`
- File patterns: `.git` files (not directories)
- Path errors involving git repositories

### Integration with SuperClaude
- **Wave Mode**: Multi-worktree analysis across complex projects
- **MCP Coordination**: Filesystem MCP mandatory, Sequential for complex git operations
- **Persona Integration**: DevOps persona for worktree management, Security for path validation
- **Command Integration**: Works with `/build`, `/analyze`, `/troubleshoot`
- **Memory Entities**: Knowledge stored for automatic recall across sessions

### Usage Examples
```bash
# Analyze worktree structure
/analyze --focus architecture git_worktree_setup_guide.md

# Build across worktrees with validation  
/build --scope project --validate --persona-devops

# Troubleshoot path issues
/troubleshoot "git worktree path errors" --think --seq
```

## Complete Reference
For comprehensive documentation: `git_worktree_setup_guide.md` (v6.0 - SuperClaude Framework Integration)
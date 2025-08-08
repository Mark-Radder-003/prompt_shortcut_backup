# AI Prompt: Git Worktree Setup Configuration

## Context
User wants to set up git worktree structure for parallel development with clean organization.

## Required Structure
```
ci-xxxx/                              # Root directory (bare git / detached HEAD)
├── .git/                             # Git management area
├── main/                             # Main worktree (main branch)
└── feature/                          # Feature worktrees directory
    ├── feature-01/                   # Feature worktree 1
    ├── feature-02/                   # Feature worktree 2
    └── feature-03/                   # Feature worktree 3
```

## Key Requirements
- Root must be bare git (detached HEAD) - no project files
- Main worktree contains all project files and documentation
- Each feature worktree is independent working directory
- All worktrees share same git history
- Parallel development without branch conflicts

## Setup Process
1. **Convert root to bare git**: `git checkout --detach` (makes root "null git")
2. **Create main worktree**: `git worktree add main main`
3. **Create feature worktrees**: `git worktree add feature/[name] feature/[name]`

## Essential Commands
- `git worktree list` - Check all worktrees
- `git worktree add [path] [branch]` - Create new worktree
- `git worktree remove [path]` - Remove worktree
- `git worktree prune` - Clean up invalid worktrees

## AI Instructions
When user requests git worktree setup:
1. Use this exact structure pattern
2. Ensure root stays clean (detached HEAD)
3. Place all project files in main/ worktree
4. Create feature/ directory for parallel development
5. Verify structure matches the pattern above

## Common Issues to Avoid
- Don't put project files in root directory
- Don't manually create worktree folders
- Always use `git worktree add` command
- Keep feature branches independent
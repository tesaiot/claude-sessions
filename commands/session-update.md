Update the current development session by:

1. Check if `.claude/sessions/.current-session` exists to find the active session
2. If no active session, inform user to start one with `/project:session-start`
3. Get current branch status: `git branch --show-current` and `git rev-list --left-right --count origin/develop...HEAD`
4. If session exists, append to the session file with:
   - Current timestamp
   - The update: $ARGUMENTS (or if no arguments, summarize recent activities from git status)
   - Add branch status section showing commits ahead/behind
   - Git status summary from `git status --porcelain`
   - If branch is behind base branch, add warning
   - Todo list status
   - Any issues encountered
   - Solutions implemented

Format the update like:
```
### Update - [TIMESTAMP]

**Summary**: $ARGUMENTS or [auto-generated summary]

**Branch Status**:
- Current: [branch name] ([X] commits ahead, [Y] behind [base branch])
[Add warning if behind: ⚠️ Branch is behind develop by Y commits]

**Git Changes**:
- Modified: [list files]
- Added: [list files]
- Deleted: [list files]

**Todo Progress**: [X completed, Y in progress, Z pending]

**Details**: [any additional context]
```

Keep updates concise but comprehensive for future reference.
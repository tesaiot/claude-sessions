Start a new development session by:

1. First check the current git branch using `git branch --show-current`
2. If on main/master branch, warn the user: "⚠️ You're on main branch! It's recommended to work on develop or a feature branch. Continue anyway?"
3. If on develop branch, ask: "What type of work will you be doing? 1) Feature 2) Bugfix 3) Improvement 4) Hotfix 5) Small changes on develop"
4. Create a session file in `.claude/sessions/` with the format `YYYY-MM-DD-HHMM-$ARGUMENTS.md` (or just `YYYY-MM-DD-HHMM.md` if no name provided)

The session file should begin with:
```
# Development Session - [DATE TIME] - [NAME IF PROVIDED]

## Branch Information
- Current Branch: [result from git branch --show-current]
- Base Branch: [develop or main based on branch type]
- Type: [feature/bugfix/improvement/hotfix/develop]

## Goals
- [ ] [ask user for goals if not clear]

## Progress
### [TIMESTAMP] Session started
Started working on branch: [branch name]
```

5. After creating the file, create or update `.claude/sessions/.current-session` to track the active session filename
6. Confirm the session has started and remind the user they can:
   - Update it with `/project:session-update`
   - End it with `/project:session-end`
   - Check branch status with `/project:session-branch-status`
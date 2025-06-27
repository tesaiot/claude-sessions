Start a new bugfix development session by:

1. Check current branch is develop: `git branch --show-current`
   - If not on develop, checkout develop first: `git checkout develop`
   - Pull latest: `git pull origin develop`

2. Parse arguments to extract issue number and description
   - Format expected: "123 description" or just "description"
   - If has issue number: branch name = `bugfix/123-description`
   - If no issue number: branch name = `bugfix/description`

3. Create bugfix branch: `git checkout -b [branch name]`

4. Create session file in `.claude/sessions/` with appropriate name

The session file should begin with:
```
# Bugfix Session - [DATE TIME] - [ISSUE#] [DESCRIPTION]

## Branch Information
- Branch: bugfix/[branch name]
- Base Branch: develop
- Type: Bug Fix
- Issue: #[issue number if provided]

## Bug Details
### Description
[Ask user to describe the bug]

### Steps to Reproduce
1. [Ask for reproduction steps]

### Expected Behavior
[Ask what should happen]

### Actual Behavior
[Ask what actually happens]

## Root Cause Analysis
[To be filled during investigation]

## Progress
### [TIMESTAMP] Bugfix branch created
Created bugfix/[branch name] from develop (latest)
Started investigation of issue #[issue]
```

5. Update `.claude/sessions/.current-session` with session filename

6. Confirm: "🐛 Bugfix branch created and session started!"

7. Remind user to:
   - Reproduce the issue first
   - Document findings in session
   - Add tests to prevent regression
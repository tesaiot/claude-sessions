Start a new hotfix session by:

1. ⚠️ IMPORTANT: Check current branch should be main/master: `git branch --show-current`
   - If not on main/master, checkout main first: `git checkout main`
   - Pull latest: `git pull origin main`

2. Parse arguments for version and description
   - Format expected: "1.2.1 description" or just "description"
   - If has version: branch name = `hotfix/1.2.1-description`
   - If no version: ask for version number

3. Create hotfix branch: `git checkout -b hotfix/[version]-$ARGUMENTS`

4. Create session file in `.claude/sessions/` with format `YYYY-MM-DD-HHMM-hotfix-[version]-$ARGUMENTS.md`

The session file should begin with:
```
# Hotfix Session - [DATE TIME] - v[VERSION] - $ARGUMENTS

## Branch Information
- Branch: hotfix/[version]-$ARGUMENTS
- Base Branch: main
- Type: Production Hotfix
- Severity: [Ask: Critical/High/Medium]

## Issue Details
### Production Issue
[Ask user to describe the production issue]

### Impact
- Affected Users: [Ask for impact assessment]
- Severity: [Critical/High/Medium]
- Started: [When did issue start]

### Root Cause
[To be determined during investigation]

## Fix Strategy
[Ask for proposed fix approach]

## Testing Plan
- [ ] Local testing
- [ ] Staging verification
- [ ] Production smoke test

## Progress
### [TIMESTAMP] Hotfix branch created
Created hotfix/[version]-$ARGUMENTS from main (latest)
🚨 CRITICAL: This will be deployed to PRODUCTION
```

5. Update `.claude/sessions/.current-session` with session filename

6. Confirm with warning: "🚨 HOTFIX branch created from MAIN! This will go to PRODUCTION!"

7. Remind user:
   - This fix will be deployed to production
   - Must be merged to BOTH main AND develop
   - Keep changes minimal and focused
   - Test thoroughly before merging
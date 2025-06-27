Start a new feature development session by:

1. Check current branch is develop: `git branch --show-current`
   - If not on develop, checkout develop first: `git checkout develop`
   - Pull latest: `git pull origin develop`

2. Create feature branch: `git checkout -b feature/$ARGUMENTS`
   - If no arguments provided, ask for feature name

3. Create session file in `.claude/sessions/` with format `YYYY-MM-DD-HHMM-feature-$ARGUMENTS.md`

The session file should begin with:
```
# Feature Development Session - [DATE TIME] - $ARGUMENTS

## Branch Information
- Branch: feature/$ARGUMENTS
- Base Branch: develop
- Type: Feature Development
- Jira/Issue: [Ask if applicable]

## Feature Requirements
- [ ] [Ask user for main requirements]

## Acceptance Criteria
- [ ] [Ask user for acceptance criteria]

## Technical Approach
[Ask for brief technical approach]

## Progress
### [TIMESTAMP] Feature branch created
Created feature/$ARGUMENTS from develop (latest)
```

4. Update `.claude/sessions/.current-session` with session filename

5. Confirm: "✅ Feature branch 'feature/$ARGUMENTS' created and session started!"

6. Remind user:
   - Commit frequently with descriptive messages
   - Keep branch updated with develop
   - Update session with `/project:session-update`
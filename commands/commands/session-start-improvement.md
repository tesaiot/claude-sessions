Start a new improvement/refactoring session by:

1. Check current branch is develop: `git branch --show-current`
   - If not on develop, checkout develop first: `git checkout develop`
   - Pull latest: `git pull origin develop`

2. Create improvement branch: `git checkout -b improvement/$ARGUMENTS`
   - If no arguments provided, ask for improvement name

3. Create session file in `.claude/sessions/` with format `YYYY-MM-DD-HHMM-improvement-$ARGUMENTS.md`

The session file should begin with:
```
# Improvement Session - [DATE TIME] - $ARGUMENTS

## Branch Information
- Branch: improvement/$ARGUMENTS
- Base Branch: develop
- Type: Improvement/Refactoring

## Improvement Objectives
- [ ] [Ask user for main objectives]

## Current State Analysis
### Performance Metrics (if applicable)
- Current: [baseline measurements]
- Target: [improvement goals]

### Code Quality Issues
- [Ask what needs refactoring]

### Technical Debt
- [Ask what technical debt is being addressed]

## Success Criteria
- [ ] Performance improved by X% (if applicable)
- [ ] Code coverage maintained or increased
- [ ] No breaking changes
- [ ] All tests still passing

## Progress
### [TIMESTAMP] Improvement branch created
Created improvement/$ARGUMENTS from develop (latest)
```

4. Update `.claude/sessions/.current-session` with session filename

5. Confirm: "🔧 Improvement branch 'improvement/$ARGUMENTS' created and session started!"

6. Remind user:
   - Measure before and after metrics
   - Keep changes backwards compatible
   - Update documentation for any API changes
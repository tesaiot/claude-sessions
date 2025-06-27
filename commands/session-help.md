Show help for the session management system:

## Session Management Commands

The session system helps document development work across git branches.

### Available Commands:

**Basic Commands:**
- `/project:session-start [name]` - Start a new session (branch-aware)
- `/project:session-update [notes]` - Add notes with branch status  
- `/project:session-end` - End session with merge readiness check
- `/project:session-list` - List sessions grouped by branch type
- `/project:session-current` - Show current session and branch info
- `/project:session-help` - Show this help

**Branch-Specific Commands (coming soon):**
- `/project:session-start-feature [name]` - Create feature branch & session
- `/project:session-start-bugfix [issue] [name]` - Create bugfix branch & session
- `/project:session-start-improvement [name]` - Create improvement branch & session
- `/project:session-start-hotfix [version] [name]` - Create hotfix branch & session

### Git Flow Support:

- Default branch: develop
- Feature/Bugfix/Improvement: branch from develop → merge to develop
- Hotfix: branch from main → merge to main AND develop
- Small changes: can work directly on develop

### Best Practices:

- Use appropriate branch types for different work
- Keep branch synced with base branch
- Update session regularly
- End session before creating PR
- Review branch checklist before merging

### Example Workflow:

```
# On develop branch
/project:session-start feature-auth
# Choose option 1 for feature
/project:session-update Added login form
/project:session-update Fixed validation bug
/project:session-end
# Create PR to develop
```
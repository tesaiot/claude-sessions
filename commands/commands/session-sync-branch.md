Sync current branch with base branch by:

1. Check current session and branch:
   - Read `.claude/sessions/.current-session`
   - Get current branch: `git branch --show-current`
   - Determine base branch from branch type

2. Save any uncommitted changes:
   - Check for changes: `git status --porcelain`
   - If changes exist, stash them: `git stash push -m "Auto-stash before sync"`

3. Fetch latest from remote:
   - `git fetch origin [base-branch]`

4. Attempt to merge base branch:
   - For feature/bugfix/improvement: `git merge origin/develop`
   - For hotfix: `git merge origin/main`

5. Handle merge results:
   - If successful: Report number of commits merged
   - If conflicts: 
     * List conflicted files
     * Provide instructions to resolve
     * DO NOT auto-resolve

6. If stashed changes exist:
   - Apply stash: `git stash pop`
   - Report any conflicts from stash

7. Update session file with sync record:
```
### [TIMESTAMP] Branch synchronized
Synced with [base-branch]: [X] new commits merged
[List any conflicts if present]
```

8. Show summary:
```
🔄 Branch Sync Complete

✅ Synced with: develop
📥 Commits merged: 3
📝 Your changes: Restored from stash

Current status:
- Branch is now up to date with develop
- No conflicts detected
- Ready to continue development

Next steps:
- Review merged changes
- Run tests to ensure compatibility
- Continue with your feature development
```

9. If conflicts exist, provide detailed resolution guide
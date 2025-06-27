Show comprehensive branch status for current session by:

1. Check if `.claude/sessions/.current-session` exists
   - If no session active, inform user to start one

2. Get current branch information:
   - Current branch: `git branch --show-current`
   - Branch type from name (feature/bugfix/improvement/hotfix)
   - Base branch (develop for most, main for hotfix)

3. Check sync status:
   - Commits ahead: `git rev-list --count origin/[base]..HEAD`
   - Commits behind: `git rev-list --count HEAD..origin/[base]`
   - Last fetch: `stat -c %y .git/FETCH_HEAD`

4. Check for conflicts:
   - Try merge with no-commit: `git merge --no-commit --no-ff origin/[base]`
   - Abort merge: `git merge --abort`
   - List any conflicts found

5. Show local changes:
   - Staged files: `git diff --cached --name-status`
   - Modified files: `git diff --name-status`
   - Untracked files: `git ls-files --others --exclude-standard`

6. Display formatted output:
```
🌿 Branch Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📍 Current Branch: feature/user-auth
   Type: Feature Branch
   Base: develop
   Created: 2 days ago

📊 Sync Status:
   ✅ Ahead of develop: 5 commits
   ⚠️  Behind develop: 2 commits
   Last sync: 2025-01-18 14:30

🔄 Recent Commits (this branch):
   - abc123: Add login validation (2 hours ago)
   - def456: Implement JWT tokens (5 hours ago)
   - ghi789: Create auth middleware (1 day ago)

📝 Local Changes:
   Staged: 1 file
   - M: src/auth/login.ts
   
   Modified: 3 files
   - M: src/auth/middleware.ts
   - M: tests/auth.test.ts
   - M: README.md
   
   Untracked: 2 files
   - src/auth/types.ts
   - docs/auth-flow.md

⚠️  Action Required:
   - Sync with develop (2 commits behind)
   - Stage or commit local changes
   - No conflicts detected ✅

💡 Suggested Commands:
   - git pull origin develop (to sync)
   - git add . (to stage all)
   - git commit -m "message" (to commit)
```

7. Provide specific recommendations based on status
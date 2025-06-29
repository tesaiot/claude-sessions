Prepare and merge current branch to develop branch by:

1. Check current branch and session status:
   - Get current branch: `git branch --show-current`
   - Verify not on main/master or develop
   - Check `.claude/sessions/.current-session` for active session
   - Get branch status: `git rev-list --left-right --count origin/develop...HEAD`

2. Display pre-merge checklist:
```
🔀 MERGE TO DEVELOP PREPARATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📍 Current Branch: [branch name]
🎯 Target Branch: develop
📊 Status: [X] commits ahead, [Y] behind develop
📁 Session: [active session file]

⚡ PRE-MERGE CHECKLIST:
```

3. Execute comprehensive pre-merge tasks:
```
☐ Update Session Documentation
  - Run: /project:session-update Final updates before merge
  - Document all completed features
  - List any known issues
  - Update TODO items status

☐ Code Quality Checks
  - Run all tests: npm test / pytest / cargo test
  - Lint check: npm run lint / pylint / cargo clippy
  - Type check: tsc --noEmit / mypy
  - No console.log or debug statements

☐ File Cleanup
  - Remove all temp files from /tmp/
  - Delete any test files (*_test, *_fixed, *_v2)
  - Clean up commented code
  - Verify no hardcoded values

☐ Documentation Updates
  - README.md reflects new features
  - API documentation updated
  - CHANGELOG.md entry added
  - Comments for complex code

☐ Git Status Check
  - All changes committed
  - No untracked files (except intended)
  - Working directory clean
  - .gitignore updated if needed

☐ Branch Sync Status
  - Fetch latest: git fetch origin develop
  - Check if behind develop
  - Resolve any conflicts locally first
```

4. Sync with develop if behind:
```bash
# If branch is behind develop
git fetch origin develop
git merge origin/develop
# Resolve conflicts if any
# Test after merge
```

5. Final commit preparation:
```bash
# Stage any remaining changes
git add .
git status

# Final commit with descriptive message
git commit -m "[Branch Type]: [Description] - Ready for merge to develop"
```

6. Execute merge process:
```bash
# Push current branch with latest changes
git push origin [current-branch]

# Switch to develop
git checkout develop
git pull origin develop

# Merge feature branch
git merge --no-ff [current-branch] -m "Merge [branch-type]/[name] into develop"

# Push merged develop
git push origin develop
```

7. Post-merge cleanup:
```
☐ Session Finalization
  - Run: /project:session-end
  - Archive session with merge status

☐ Branch Cleanup (Optional)
  - Delete local: git branch -d [branch-name]
  - Delete remote: git push origin --delete [branch-name]
  - Or keep for reference

☐ Verification
  - Check develop branch on GitHub
  - Verify CI/CD pipelines pass
  - Confirm no merge conflicts
```

8. Generate merge summary:
```
✅ MERGE TO DEVELOP COMPLETED

📋 Merge Summary:
- Source: [branch-name]
- Target: develop
- Commits merged: [X]
- Session: [session-file]

🎯 Next Steps:
- Monitor CI/CD on develop branch
- Create new branch for next feature
- Update project board/tickets

💡 Commands:
- Start new feature: /project:session-start-feature [name]
- Check develop status: git log --oneline -10
```

9. Update tracking files:
   - Mark branch as merged in any tracking systems
   - Update project documentation
   - Notify team if needed
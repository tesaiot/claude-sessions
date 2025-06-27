Prepare current session for code review by:

1. Check current session exists and get branch info
   - Must be on feature/bugfix/improvement branch
   - Cannot be on main/develop

2. Run pre-review checks:
   ```
   ✓ All changes committed (no uncommitted files)
   ✓ Branch up to date with base branch
   ✓ No merge conflicts
   ✓ Tests passing (if test command available)
   ✓ No linting errors (if linter available)
   ```

3. Generate PR information from session:
   - Extract accomplishments from session
   - List all changed files
   - Summarize approach taken
   - Note any breaking changes

4. Create PR description:
```markdown
## Summary
[Auto-generated from session accomplishments]

## Type of Change
- [ ] 🐛 Bug fix (non-breaking change)
- [ ] ✨ New feature (non-breaking change)
- [ ] 💥 Breaking change
- [ ] 🔧 Improvement/Refactoring

## Changes Made
[List key changes from session]

## Testing
[How the changes were tested]

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Tests added/updated
- [ ] All tests passing

## Related Issues
[Any issue numbers from session]

## Session Reference
Session file: [session filename]
```

5. Suggest reviewers based on changed files:
   - Look at git blame for changed files
   - Suggest top contributors as reviewers

6. Update session with review preparation:
```
### [TIMESTAMP] Ready for Review
- All changes committed
- Branch synced with [base]
- PR description prepared
- Suggested reviewers: [list]
```

7. Show next steps:
```
✅ Ready for Code Review!

Branch: feature/user-auth
Target: develop
Changes: 15 files

Suggested Reviewers:
- @johndoe (auth module owner)
- @janedoe (recent contributor)

Next Steps:
1. Create PR on GitHub/GitLab/Bitbucket
2. Copy the generated PR description
3. Assign suggested reviewers
4. Link any related issues

💡 PR Description copied to clipboard (if possible)
```
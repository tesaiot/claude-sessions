End the current development session by:

1. Check `.claude/sessions/.current-session` for the active session
2. If no active session, inform user there's nothing to end
3. Get final branch information: current branch, commits ahead/behind, branch type
4. If session exists, append a comprehensive summary including:
   - Session duration
   - Git summary:
     * Total files changed (added/modified/deleted)
     * List all changed files with change type
     * Number of commits made (if any)
     * Final git status
   - Todo summary:
     * Total tasks completed/remaining
     * List all completed tasks
     * List any incomplete tasks with status
   - Key accomplishments
   - All features implemented
   - Problems encountered and solutions
   - Breaking changes or important findings
   - Dependencies added/removed
   - Configuration changes
   - Deployment steps taken
   - Lessons learned
   - What wasn't completed
   - Tips for future developers
   
   ADD NEW SECTION:
   ### Branch & Merge Readiness
   - Branch Type: [detected from branch name]
   - Current Branch: [branch name]
   - Merge Target: [develop for feature/bugfix/improvement, main for hotfix]
   - Branch Status: [X commits ahead, Y behind]
   - Ready for PR: [Yes if no conflicts and not behind]
   
   ### Pre-Merge Checklist
   - [ ] All tests passing
   - [ ] No conflicts with base branch
   - [ ] Code reviewed locally
   - [ ] Documentation updated

5. Empty the `.claude/sessions/.current-session` file (don't remove it, just clear its contents)
6. If on feature/bugfix/improvement branch, remind: "Ready to create PR to develop branch"
7. If on hotfix branch, remind: "Remember to merge to both main AND develop"

The summary should be thorough enough that another developer (or AI) can understand everything that happened without reading the entire session.
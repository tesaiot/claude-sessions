Show the current session status by:

1. Check if `.claude/sessions/.current-session` exists
2. If no active session, inform user and suggest starting one
3. If active session exists:
   - Show session name and filename
   - Calculate and show duration since start
   - Get and show current git branch with `git branch --show-current`
   - Get branch status with `git rev-list --left-right --count origin/develop...HEAD`
   - Show branch type (feature/bugfix/improvement/hotfix/develop)
   - Show last few updates from the session file
   - Show current goals/tasks status
   - Remind user of available commands

Format output as:
```
📍 Current Session: [name]
📁 File: [filename]
⏱️ Duration: [time since start]

🌿 Branch: [current branch]
   Type: [Feature/Bugfix/Improvement/Hotfix/Develop]
   Status: [X] commits ahead, [Y] behind [base]

📝 Recent Updates:
[last 3 updates]

🎯 Current Goals:
[goals with checkboxes]

💡 Commands: session-update, session-end
```

Keep the output concise and informative.
List all development sessions by:

1. Check if `.claude/sessions/` directory exists
2. List all `.md` files (excluding hidden files and `.current-session`)
3. For each session file:
   - Read the file to extract branch information
   - Group by branch type (feature/bugfix/improvement/hotfix/develop)
   - Show filename, title, date/time, branch name
   - Mark if merged (check if branch still exists)
4. If `.claude/sessions/.current-session` exists, mark which session is active

Present in grouped format:
```
🚀 Feature Sessions
- [date]-[name].md (ACTIVE) - feature/[name]
- [date]-[name].md ✅ Merged - feature/[name]

🐛 Bugfix Sessions
- [date]-[name].md ✅ Merged - bugfix/[name]

🔧 Improvement Sessions
- [date]-[name].md 🔄 In Progress - improvement/[name]

🚨 Hotfix Sessions
- [date]-[name].md ✅ Released - hotfix/[name]

📝 Develop Branch Sessions
- [date]-[name].md ✅ Done
```

Sort by most recent first within each group.
---
name: wrap
description: Close out a work session by drafting updates to STATUS.md — fills in Last Session, Next, and any Notes based on git history and session context.
allowed-tools: Read, Edit, Bash
---

Session notes saved this session:
!`cat ~/.claude/session-notes/${CLAUDE_SESSION_ID}.md 2>/dev/null || echo "(none)"`

Current STATUS.md:
!`cat STATUS.md 2>/dev/null || echo "(no STATUS.md found in current directory)"`

Recent git log:
!`git log --oneline -20 2>/dev/null || echo "(not a git repo or no commits)"`

Uncommitted changes:
!`git diff HEAD --stat 2>/dev/null || echo "(none)"`

---

The user wants to wrap up their work session. Using the context above — session notes, the current STATUS.md, git log, and this conversation — draft updates to STATUS.md.

**What to update:**
- **Status**: only change if it genuinely shifted (e.g., hit a blocker → Blocked, wrapped up → Done)
- **Updated**: today's date
- **Last Session**: concrete bullets on what was done. Reference GitHub issue numbers if visible in commit messages or conversation. Write for someone coming back cold in two weeks.
- **Next**: the single most actionable next step — specific enough to act on immediately. An issue number + short description is ideal.
- **Notes**: only add lines that are worth preserving long-term (decisions, gotchas, key context). Don't repeat what's already there.

**How to respond:**
1. Show the proposed changes as a diff or clearly labeled new content for each section.
2. Ask the user if they want to apply it, skip any section, or adjust anything.
3. Once confirmed, use the Edit tool to write the changes to STATUS.md.

Be concise. Don't pad Last Session with obvious things. One sharp bullet beats three vague ones.

After writing STATUS.md, remind the user to run `./scripts/sync.sh` from their `_projects` directory to update the dashboard.

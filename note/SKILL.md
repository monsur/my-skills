---
name: note
description: Jot down a note, insight, or aha moment during this session to be included in the recap later. Usage: /note <your insight or observation>
disable-model-invocation: true
allowed-tools: Bash
---

The user wants to save a note for later recap: "$ARGUMENTS"

Use the Bash tool to append this note to the session notes file. Run exactly this command:

```
mkdir -p ~/.claude/session-notes && echo "- $(date '+%H:%M') $ARGUMENTS" >> ~/.claude/session-notes/${CLAUDE_SESSION_ID}.md
```

After saving, briefly confirm: tell the user the note was saved, and echo the note text back so they can verify it was captured correctly. Keep the confirmation to one short line.

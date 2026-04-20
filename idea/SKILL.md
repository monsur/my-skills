---
name: idea
description: Capture an idea to the ideas file in the _projects repo. Usage: /idea <your idea>
disable-model-invocation: true
allowed-tools: Bash
---

The user wants to save an idea: "$ARGUMENTS"

Use the Bash tool to append this idea to the ideas file. Run exactly this command:

```
mkdir -p ~/Documents/Projects/_projects && echo "- $(date '+%Y-%m-%d') $ARGUMENTS" >> ~/Documents/Projects/_projects/ideas.md
```

After saving, briefly confirm: tell the user the idea was saved, and echo the idea text back so they can verify it was captured correctly. Keep the confirmation to one short line.

---
name: idea
description: Capture an idea to IDEAS.md in the monsur/_projects GitHub repo. Usage: /idea <your idea>
allowed-tools: Bash
---

The user wants to capture this idea: "$ARGUMENTS"

**Step 1: Verify we're in the _projects repo**

Run:
```bash
git remote get-url origin 2>/dev/null
```

If the output doesn't contain `monsur/_projects`, stop and tell the user: "❌ /idea only works from the _projects repo. Navigate there first."

**Step 2: Derive a title and format the entry**

From `$ARGUMENTS`, derive a concise Title Case name (e.g. "A tool to sync Readwise highlights" → "Readwise Highlight Sync"). Use the full argument text as the description paragraph.

**Step 3: Append to IDEAS.md and push**

Compute today's date, substitute `{Title}`, `{YYYY-MM-DD}`, and `{Description}` with the values from Step 2, then run:

```bash
cat >> IDEAS.md << 'IDEA_END'

## {Title}
*Captured: {YYYY-MM-DD}*

{Description}

---
IDEA_END
git add IDEAS.md && git commit -m "idea: {Title}" && git push
```

After saving, confirm in one short line: echo the title back so the user can verify it was captured.

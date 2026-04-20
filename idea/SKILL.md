---
name: idea
description: Capture an idea to IDEAS.md in the monsur/_projects GitHub repo. Usage: /idea <your idea>
allowed-tools: Bash
---

The user wants to capture this idea: "$ARGUMENTS"

**Step 1: Check gh is ready**

Run:
```bash
command -v gh &>/dev/null && gh auth status &>/dev/null
```

If that fails, tell the user which part is missing and give setup instructions:
- **`gh` not installed:** `brew install gh` (macOS) or https://cli.github.com
- **Not authenticated:** Run `gh auth login` and follow the prompts

**Step 2: Derive a title and format the entry**

From `$ARGUMENTS`, derive a concise Title Case name (e.g. "A tool to sync Readwise highlights" → "Readwise Highlight Sync"). Use the full argument text as the description paragraph.

Format the new section exactly like this (note the blank line before the `---`):

```
## {Title}
*Captured: YYYY-MM-DD*

{Full description from $ARGUMENTS}

---
```

**Step 3: Append to IDEAS.md**

Fetch the current file, append the new section, and push it back:

```bash
RESPONSE=$(gh api repos/monsur/_projects/contents/IDEAS.md)
SHA=$(echo "$RESPONSE" | jq -r '.sha')
CURRENT=$(echo "$RESPONSE" | jq -r '.content' | base64 -d)
NEW_CONTENT="${CURRENT}
## {Title}
*Captured: $(date '+%Y-%m-%d')*

{Description}

---"
gh api repos/monsur/_projects/contents/IDEAS.md \
  --method PUT \
  --field message="idea: {Title}" \
  --field "content=$(echo -n "$NEW_CONTENT" | base64 | tr -d '\n')" \
  --field sha="$SHA"
```

Replace `{Title}` and `{Description}` with the values you derived in Step 2.

After saving, confirm in one short line: echo the title back so the user can verify it was captured.

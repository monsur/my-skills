---
name: idea
description: Capture an idea to IDEAS.md in the monsur/_projects GitHub repo. Usage: /idea <your idea>
allowed-tools: Bash
---

The user wants to capture this idea: "$ARGUMENTS"

First, check if `gh` is installed and authenticated:

```bash
command -v gh &>/dev/null && gh auth status &>/dev/null
```

If that fails, tell the user which part is missing and give them the relevant setup instructions:

- **`gh` not installed:** Install via `brew install gh` (macOS) or https://cli.github.com
- **Not authenticated:** Run `gh auth login` and follow the prompts to authenticate with GitHub

If `gh` is ready, append the idea to `IDEAS.md` in `monsur/_projects` by running these commands:

```bash
IDEA="$ARGUMENTS"
RESPONSE=$(gh api repos/monsur/_projects/contents/IDEAS.md)
SHA=$(echo "$RESPONSE" | jq -r '.sha')
CURRENT=$(echo "$RESPONSE" | jq -r '.content' | base64 -d)
NEW_CONTENT="${CURRENT}"$'\n'"- $(date '+%Y-%m-%d'): ${IDEA}"
gh api repos/monsur/_projects/contents/IDEAS.md \
  --method PUT \
  --field message="idea: ${IDEA}" \
  --field "content=$(echo -n "$NEW_CONTENT" | base64 | tr -d '\n')" \
  --field sha="$SHA"
```

After saving, confirm in one short line: echo the idea back so the user can verify it was captured.

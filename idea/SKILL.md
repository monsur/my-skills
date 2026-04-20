---
name: idea
description: Capture an idea to ideas.md in the monsur/_projects GitHub repo. Usage: /idea <your idea>
allowed-tools: mcp__github__get_file_contents, mcp__github__create_or_update_file
---

The user wants to capture this idea: "$ARGUMENTS"

Append it to `ideas.md` in the `monsur/_projects` GitHub repo on the `main` branch. Follow these steps:

1. Use `mcp__github__get_file_contents` to fetch `ideas.md` from owner=`monsur`, repo=`_projects`, and note its `sha` and current `content` (base64-decoded).
2. Append a new line to the content: `- YYYY-MM-DD $ARGUMENTS` (use today's date).
3. Use `mcp__github__create_or_update_file` to write the updated content back, providing the `sha` from step 1, with commit message: `idea: $ARGUMENTS`

After saving, confirm in one short line: echo the idea back so the user can verify it was captured.

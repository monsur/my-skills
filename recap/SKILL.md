---
name: recap
description: Generate a Bluesky thread recap of this session. Combines saved notes from /note with the full session context to produce a thread ready for Threadweaver.
disable-model-invocation: true
allowed-tools: Bash
---

Saved notes from this session:
!`cat ~/.claude/session-notes/${CLAUDE_SESSION_ID}.md 2>/dev/null || echo "(no notes saved — working from session context only)"`

Generate a Bluesky thread recap of this session. Follow these guidelines:

**Content:**
- Draw from both the saved notes above AND the full conversation context of this session
- Capture key insights, aha moments, interesting decisions, and things worth remembering
- Prioritize the notes the user explicitly saved — those are what they found most valuable
- Be specific and concrete, not generic

**Format:**
- Write in an engaging, first-person or conversational tone suitable for Bluesky
- Each post must be 300 characters or fewer (Bluesky's limit)
- Separate each post with a blank line and a line of dashes: `---`
- Number each post: start with `[1/N]` at the beginning of each post (estimate N upfront)
- Open with a strong hook post that sets up the thread topic
- Close with a final post that ties it together or invites engagement

**Output:**
Output the thread as plain text only — no markdown headers, no code blocks, no extra commentary. Just the posts separated by `---`, ready to paste into Threadweaver (https://github.com/monsur/threadweaver).

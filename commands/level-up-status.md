---
name: level-up-status
description: Show your Level-Up learning progress dashboard
---

Run `/level-up --status` logic:

Read `${CLAUDE_PLUGIN_ROOT}/data/progress.json` and `${CLAUDE_PLUGIN_ROOT}/data/curriculum.json`.

Present a visual progress dashboard showing:
- Each tier with completion count
- Each lesson with status (completed/pending/skipped)
- Completion dates for finished lessons
- Current streak and total stats
- What's next

Use checkmarks, empty boxes, and tildes for visual clarity. Keep it scannable.

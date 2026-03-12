---
id: T1-03
title: Session-Start Context Hook
tier: 1
concept: hooks
estimatedMinutes: 7
dependsOn: [T1-02]
artifact: SessionStart hook that surfaces today's context
---

## Why This Matters for Your Work

You context-switch between projects and tasks throughout the day. A `SessionStart` hook runs a quick check when you open Claude Code and surfaces: what day it is, what files you recently touched, and whether there's an unfinished task or handoff doc from your last session. It's like a 3-second briefing before every session.

## What You'll Build

A `SessionStart` hook that:
- Lists recent files modified in the last 24 hours (so you know what's "hot")
- Surfaces any NEXT-STEPS.md or handoff doc if one exists
- Optionally checks day-of-week for recurring workflow reminders

## Do This Now

1. **Review the hook you created in T1-02.** Same mechanism, different event. Instead of `PostToolUse`, this fires on `SessionStart` — once, right when you open Claude Code.

2. **Create the hook.** I'll add a `SessionStart` entry to your settings. The script will be lightweight — it must finish fast so it doesn't delay your session. Tell me to proceed.

3. **Test it.** Run `/clear` to restart. You should see a brief context summary appear automatically.

## You'll Know It Worked When

Start a new session and without typing anything, you see a brief status line: what files are hot and any outstanding handoff notes.

## What Just Happened

`SessionStart` hooks run once when Claude Code initializes. They're ideal for loading context, checking environment state, or setting up preconditions. Combined with `PostToolUse` hooks (from the previous lesson), you now have two of the most useful hook types. The others — `PreToolUse` (block dangerous actions), `Stop` (cleanup on exit), `Notification` (alerts) — follow the same pattern.

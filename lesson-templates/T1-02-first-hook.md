---
id: T1-02
title: Your First Hook
tier: 1
concept: hooks
estimatedMinutes: 10
dependsOn: []
artifact: A PostToolUse hook that validates file output
---

## Why This Matters for Your Work

You probably have files that Claude writes regularly — reports, configs, documents. Right now, if something goes wrong with the output (broken formatting, missing sections, invalid syntax), you find out when you look at it. A hook catches this automatically — every time, without you remembering to check.

The key insight: **CLAUDE.md says "please do X." Hooks guarantee X happens.** CLAUDE.md is a suggestion. Hooks are code.

## What You'll Build

A `PostToolUse` hook on the `Write` tool that runs a validation check whenever Claude writes a file. We'll tailor the validation to your most common output format (markdown, JSON, code — we'll figure out which one matters most for you).

## Do This Now

1. **Identify your most-written file type.** What does Claude write for you most often? Reports? Configs? Code? We'll build the hook for that.

2. **Understand the hook lifecycle.** Hooks fire at specific events: `PreToolUse` (before a tool runs), `PostToolUse` (after), `SessionStart`, `Stop`, and others. We want `PostToolUse` on `Write` — it fires after any file write.

3. **Create the hook.** I'll add a hook configuration to your project's settings. The hook will be a small bash script or prompt-based check that validates the written file. Tell me to proceed.

4. **Test it.** We'll write a deliberately malformed file and verify the hook catches it. Then clean up.

## You'll Know It Worked When

Write a file with an intentional error. The hook fires and flags the issue before the session moves on.

## What Just Happened

Hooks are Claude Code's quality gates. Unlike instructions in CLAUDE.md (which Claude follows probabilistically), hooks execute deterministically as shell commands or matcher-based prompts. They're perfect for anything that MUST happen: validation, linting, security checks, audit logging. You now have the pattern — you can add hooks for any tool at any lifecycle point.

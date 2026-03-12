---
id: T3-04
title: Custom Keybindings
tier: 3
concept: efficiency
estimatedMinutes: 5
dependsOn: []
artifact: ~/.claude/keybindings.json with your shortcuts
---

## Why This Matters for Your Work

You invoke commands multiple times per day. Each time, you type the full command name. Custom keybindings let you trigger these with a key chord — saving a few seconds per invocation that compounds across hundreds of daily interactions.

## What You'll Build

A `keybindings.json` file with shortcuts for your 4-5 most-used commands.

## Do This Now

1. **Identify your top commands.** I'll look at your command directory and suggest the most frequently useful ones.

2. **I'll create the keybindings file** at `~/.claude/keybindings.json` with ergonomic key combos. Tell me which commands you want mapped.

3. **Test each binding.** Press the shortcut, verify the command fires.

## You'll Know It Worked When

You press a two-key shortcut and your most-used command fires instantly. No typing, no autocomplete, no `/`.

## What Just Happened

Keybindings in Claude Code work like IDE shortcuts — they map key combinations to actions. The file lives at `~/.claude/keybindings.json` and supports standard modifier keys (Ctrl, Alt, Shift, Meta). Chord bindings (two-step combos like `Ctrl+K, Ctrl+M`) are also supported for when you run out of simple combos.

---
id: T3-03
title: Headless Batch Processing
tier: 3
concept: automation
estimatedMinutes: 10
dependsOn: []
artifact: Shell script using claude -p for batch operations
---

## Why This Matters for Your Work

You have files that need similar processing — transcripts to summarize, reports to generate, data to transform. Right now, each one is a separate interactive session. `claude -p` (print mode) runs Claude non-interactively — you give it a prompt, it executes and returns the result. Chain multiple calls in a shell script and you can batch-process 10 files while you do other work.

## What You'll Build

A shell script that takes a directory of files and runs a Claude prompt on each one, writing the results back.

## Do This Now

1. **Understand the syntax.** `claude -p "your prompt here"` runs Claude once, non-interactively, and prints the result. You can pipe files into it: `cat file.md | claude -p "Summarize this"`.

2. **Identify a batch task.** What files do you have multiple of that need the same processing? I'll help you pick the right one.

3. **I'll create a batch script** that finds matching files, runs the prompt on each, and writes the output. Tell me the directory and file pattern.

4. **Test on 2-3 files.** We'll run the script on a small batch to verify output quality.

## You'll Know It Worked When

You point the script at a folder with multiple files, go do other work, and come back to processed results.

## What Just Happened

`claude -p` is Claude Code's non-interactive mode. It unlocks batch processing, CI/CD integration, and scripted workflows. Key flags: `-p` for single prompt, `--output-format json` for structured output, `--max-turns` to limit agent loops, `--allowedTools` to restrict what Claude can do. Combined with shell scripting, this turns Claude from an interactive assistant into a batch processing engine.

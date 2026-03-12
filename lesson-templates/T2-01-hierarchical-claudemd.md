---
id: T2-01
title: Hierarchical CLAUDE.md
tier: 2
concept: project-context
estimatedMinutes: 10
dependsOn: [T1-01]
artifact: Sub-folder CLAUDE.md files for key directories
---

## Why This Matters for Your Work

Your root CLAUDE.md gives Claude the big picture. But when you're deep in a specific subdirectory, Claude doesn't need to know about unrelated projects. Sub-folder CLAUDE.md files add **scoped context** — Claude gets the root file PLUS the nearest sub-folder file, giving it exactly the right level of detail for where you're working.

## What You'll Build

CLAUDE.md files for your 2-3 main work areas, each with directory-specific context: key files, conventions, domain terminology, and tools relevant to that subdirectory.

## Do This Now

1. **Identify your top directories.** Which 2-3 subdirectories do you work in most? I'll scan your project structure to suggest candidates.

2. **I'll draft CLAUDE.md files for each.** Keep them short — 30-50 lines each. These are supplements to the root, not replacements.

3. **Verify.** Navigate into a subdirectory and ask Claude a domain-specific question. It should know the local conventions without you explaining them.

## You'll Know It Worked When

In a fresh session from a subdirectory, Claude knows the local context (file conventions, domain terms, key files) in addition to the project-wide context from the root CLAUDE.md.

## What Just Happened

Claude Code loads CLAUDE.md from the working directory AND every parent directory up to `/`. This means context is additive and hierarchical — general info at the root, specific info deeper down. This is the same pattern used by large engineering teams: root CLAUDE.md for repo-wide conventions, sub-folder files for module-specific patterns. Context that scales with directory depth.

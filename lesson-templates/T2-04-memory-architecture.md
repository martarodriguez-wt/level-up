---
id: T2-04
title: Memory Architecture
tier: 2
concept: memory
estimatedMinutes: 10
dependsOn: []
artifact: Structured memory system with clear categories and naming
---

## Why This Matters for Your Work

Claude Code's auto-memory system works, but memory files tend to grow organically — session notes mixed with decisions, flat indexes, inconsistent naming. As your memory grows, finding the right context becomes harder. A structured architecture means Claude (and future you) can find any piece of context in one lookup instead of scanning everything.

## What You'll Build

A refactored memory directory with:
- Clear naming conventions (type prefix: `user_`, `project_`, `feedback_`, `reference_`)
- Each memory file focused on exactly one topic
- MEMORY.md as a categorized index (not just a list)
- Archived/outdated memories moved to an `archive/` subdirectory

## Do This Now

1. **I'll read your current memory directory** and catalog every file: what it contains, whether it's current, and what type it is (user, feedback, project, reference).

2. **I'll propose a restructure.** New naming, new organization, what to split, what to archive.

3. **You approve the plan.** I'll execute the renames and MEMORY.md rewrite.

4. **Verify.** Ask Claude in a fresh session: "What do you know about [specific project]?" It should find the right memory instantly.

## You'll Know It Worked When

MEMORY.md reads like a table of contents, not a dump. Each memory file has clear frontmatter (name, description, type) and covers exactly one topic.

## What Just Happened

Memory architecture is information architecture. The same principles that make a good product taxonomy make a good memory system: mutually exclusive categories, descriptive naming, and a navigable index. As your memory grows (and it will), this structure prevents the "can't find anything" problem that kills knowledge bases.

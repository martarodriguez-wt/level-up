---
id: T1-01
title: Root CLAUDE.md
tier: 1
concept: project-context
estimatedMinutes: 8
dependsOn: []
artifact: CLAUDE.md at your project root
---

## Why This Matters for Your Work

Every time you start a session, Claude discovers your setup from scratch. It doesn't know your role, your project structure, your conventions, or what tools you have configured. A root CLAUDE.md fixes this — it's auto-loaded at session start and gives Claude your full context in the first second.

This is typically the single biggest efficiency gap for Claude Code users. Everything else in the curriculum builds on this.

## What You'll Build

A `CLAUDE.md` at your project root that:
- Declares your role and what you work on
- Maps your project directories and what's in each
- Lists your key commands, skills, and agents by use case
- States your writing/coding conventions
- Notes the tools you have configured (MCPs, plugins, etc.)

## Do This Now

1. **Audit your setup.** I'll scan your directory structure, agents, commands, and skills to draft the CLAUDE.md. Tell me to proceed.

2. **Review and edit.** I'll show you the draft. You approve or adjust. Target: under 80 lines (concise enough that Claude reads it all, complete enough that it never asks "what project is this?").

3. **Verify.** Run `/clear` and start a fresh session. Ask Claude: "What projects do I have and what are my key tools?" It should answer correctly without you providing any context.

## You'll Know It Worked When

A fresh session — with zero context from you — correctly identifies your projects, tools, and conventions. No more "Can you tell me about your setup?"

## What Just Happened

CLAUDE.md is Claude Code's project memory. It loads automatically at session start from the working directory and every parent directory up to `/`. By placing one at your root working directory, you've given every session a baseline understanding of who you are and what you're working on. Sub-folder CLAUDE.md files (a later lesson) add directory-specific context on top of this.

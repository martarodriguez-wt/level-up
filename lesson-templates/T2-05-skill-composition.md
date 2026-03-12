---
id: T2-05
title: Skill Composition — Chain Your Automations
tier: 2
concept: skills
estimatedMinutes: 10
dependsOn: []
artifact: A command or skill that chains multiple automations
---

## Why This Matters for Your Work

If you have multiple commands or skills that do related things, running the full pipeline means invoking them separately and mentally tracking which step you're on. Skill composition chains them: one trigger, full pipeline, proper handoff between stages.

## What You'll Build

An updated workflow where:
- One command can invoke another command or skill as a downstream step
- Each stage's output feeds the next stage's input
- The full pipeline is traceable (you can see which stage produced what)

## Do This Now

1. **Identify related automations.** Which of your commands/skills do you often run in sequence? I'll read your command and skill files to find candidates.

2. **Map the data flow.** What does step 1 produce that step 2 needs? What's currently duplicated between them?

3. **Propose the composition.** This might mean: one command calls another, a skill gains a sub-mode, or a new orchestrator wraps both.

4. **Implement and test.** We'll run the composed pipeline and verify each stage passes data correctly.

## You'll Know It Worked When

One command triggers the full pipeline. You can see the handoff between stages, and the final output reflects data from all upstream stages.

## What Just Happened

Skill composition is the difference between a collection of scripts and an automation system. When commands can invoke skills (or vice versa), you get pipelines — and pipelines are where the real productivity gains live. The pattern: break work into single-responsibility stages, then compose them with clear interfaces.

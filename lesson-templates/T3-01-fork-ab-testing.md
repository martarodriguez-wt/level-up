---
id: T3-01
title: /fork for A/B Prompt Testing
tier: 3
concept: context-management
estimatedMinutes: 6
dependsOn: []
artifact: Side-by-side comparison of two approaches
---

## Why This Matters for Your Work

When framing a document or choosing between approaches, you often face "should I go with X or Y?" choices. Right now, you pick one and iterate. With `/fork`, you branch the conversation — same context, two different directions — and compare results side by side. It's A/B testing for prompts.

## What You'll Build

A forked session where you test two different approaches to the same problem. We'll use a real example from your work.

## Do This Now

1. **Pick a framing question.** Any real decision where you're torn between two approaches — document structure, analysis angle, communication tone.

2. **Build context.** Share the relevant background in this session.

3. **Fork.** Type `/fork`. This creates a branch with your full conversation context preserved.

4. **Run both approaches.** In this session, go with option A. In the forked session, go with option B. Compare the outputs.

5. **You can also fork from the CLI:** `claude -c --fork-session` when resuming a past session.

## You'll Know It Worked When

You have two complete outputs from the same starting context, each exploring a different angle. You can pick the better one — or merge the best of both.

## What Just Happened

`/fork` preserves the full conversation context and branches it. This is fundamentally different from starting a new session (which loses context) or continuing in the same session (which pollutes context with the first attempt). Use it whenever you want to explore alternatives without commitment: different structures, competing framings, alternative tones.

---
id: T3-05
title: Multi-Perspective Parallel Review
tier: 3
concept: parallel-agents
estimatedMinutes: 8
dependsOn: []
artifact: A command that launches multiple agent reviews in parallel
---

## Why This Matters for Your Work

If you have multiple agents for different perspectives, running them sequentially — ask one, wait, ask the next, wait — takes N times as long as it should. Claude Code can spawn parallel agents. One command launches multiple reviews simultaneously and synthesizes the results. A 15-minute review loop becomes 2-3 minutes.

## What You'll Build

A `/review-360` command that:
1. Takes a file path as input
2. Launches 3 of your agents in parallel (we'll pick the most useful combination)
3. Collects all perspectives
4. Synthesizes: what they agree on, where they disagree, and what gaps each uniquely identified

## Do This Now

1. **I'll create the command** in your commands directory. It will use the Agent tool to launch your existing agents in parallel.

2. **Pick a test document.** Any document you'd normally want multiple perspectives on.

3. **Run it.** `/review-360 path/to/document.md` — watch the agents work simultaneously.

4. **Review the synthesis.** The command produces a unified output with agreement areas, disagreement areas, and unique insights from each lens.

## You'll Know It Worked When

You get distinct, non-overlapping reviews in under 3 minutes, plus a synthesis that highlights the most important feedback across all perspectives.

## What Just Happened

Parallel agents are Claude Code's multiplier. Each agent runs in its own context, with its own tools and persona, simultaneously. The key is the Agent tool's ability to launch multiple agents in a single message. This pattern scales: 3 agents for a quick review, 10 agents for processing 10 files, or 5 agents researching 5 different approaches. The constraint is that agents can't see each other's work in real-time — the synthesis step bridges that gap.

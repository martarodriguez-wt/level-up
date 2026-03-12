---
name: level-up-refresh
description: Discover new Claude Code tips and features from the community and Anthropic changelogs. Adds new lessons to your Tier 4 Frontier curriculum.
---

Run `/level-up --refresh` logic:

Read `${CLAUDE_PLUGIN_ROOT}/data/discoveries.json` for last refresh date and sources.

Execute web research against all sources listed in discoveries.json. Filter results for relevance to the user's role (from `${CLAUDE_PLUGIN_ROOT}/data/progress.json` profile). Add new discoveries. Create Tier 4 lesson templates for high-relevance finds in `${CLAUDE_PLUGIN_ROOT}/lesson-templates/`. Update curriculum.json and discovery timestamps.

Report: what you found, what's new since last refresh, and how many new lessons were added.

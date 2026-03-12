# Level-Up — Claude Code Learning Assistant

A dynamic, personalized learning system for Claude Code. Assesses your actual setup, finds the highest-impact improvement, and teaches it through your real work.

## How It Works

Level-Up doesn't follow a fixed curriculum. It:

1. **Assesses your setup** — reads your agents, commands, skills, hooks, CLAUDE.md files, MCP servers, keybindings, memory, and settings. Not just "do you have it?" but "how well is it configured?"
2. **Scores maturity** — each concept gets a level from 0 (absent) to 3 (optimized), based on quality rubrics
3. **Finds the best next lesson** — anti-patterns first, then foundations, then deepening. Respects concept dependencies.
4. **Generates the lesson dynamically** — using YOUR actual files as the teaching vehicle. No pre-written tutorials.
5. **Stays current** — refresh the knowledge base from Anthropic docs to learn about new features

## Install

```
/plugin marketplace add martarodriguez-wt/level-up
```

## Usage

| Command | What It Does |
|---------|-------------|
| `/level-up` | Assess and teach the next highest-impact improvement |
| `/level-up --status` | Dashboard of all concepts with maturity levels |
| `/level-up --assess` | Full audit of your Claude Code setup |
| `/level-up --topic hooks` | Deep-dive into a specific concept |
| `/level-up --refresh` | Update knowledge base from latest docs |

On first run, Level-Up asks about your role and runs a full assessment. After that, each `/level-up` does a quick re-check before selecting the best lesson.

## What It Teaches

16 concepts organized by dependency, not difficulty:

| Concept | What It Covers |
|---------|---------------|
| project-context | CLAUDE.md files — root, hierarchical, rules |
| hooks | PreToolUse, PostToolUse, SessionStart, Stop, and more |
| agents | Custom subagents with personas, tools, models |
| commands | Reusable prompt templates via /command |
| skills | Rich auto-triggering capabilities with supporting files |
| mcp-servers | External tool integrations via MCP |
| keybindings | Custom keyboard shortcuts |
| memory | Auto-memory, MEMORY.md, topic files |
| context-management | /fork, /compact, /clear, handoff docs |
| parallel-execution | Multi-agent workflows, git worktrees |
| headless-automation | claude -p for batch processing and CI/CD |
| model-configuration | Model selection, effort levels, thinking |
| permissions-security | Allow/deny rules, sandboxing |
| plugins | Installing, curating, and creating plugins |
| voice-input | Dictation for faster prompt input |
| scheduled-tasks | /loop, cron, recurring automation |

## Maturity Model

Every concept is scored on a 4-level scale:

| Level | Meaning | Coach Action |
|-------|---------|-------------|
| 0 — Absent | Don't have it | Introduce through real task |
| 1 — Present | Have it, but minimal | Teach fundamentals and best practices |
| 2 — Functional | Works, but misses best practices | Diagnose anti-patterns, improve |
| 3 — Optimized | Well-configured | Skip (or revisit quarterly) |

The coach prioritizes: **anti-patterns > absent foundations > deepening**. A badly configured feature is more urgent than a missing one.

## Architecture

```
level-up/
├── .claude-plugin/plugin.json    # Plugin manifest
├── agents/coach.md               # Coaching persona + assessment protocol
├── commands/level-up.md          # Entry point + all modes
├── data/
│   ├── knowledge.md              # Concept graph + maturity rubrics (refreshable)
│   └── progress.json             # User profile + concept levels (auto-populated)
├── README.md
└── LICENSE
```

**6 files. No pre-written lessons.** The coach generates every lesson dynamically from the knowledge graph + your actual setup.

## Contributing

To add a concept:
1. Add a section to `data/knowledge.md` following the existing format (dependencies, detection, maturity levels 0-3, anti-patterns, best practices, level transitions)
2. Submit a PR

To update rubrics or best practices: edit the relevant section in `data/knowledge.md`.

## License

MIT

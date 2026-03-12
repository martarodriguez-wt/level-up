# Level-Up — Claude Code Learning Assistant

A progressive, personalized learning system for Claude Code. Teaches through your real work, not tutorials.

## What It Does

Level-Up is a Claude Code plugin that acts as your personal coach. It:

- **Assesses your setup** on first run — scans your agents, commands, skills, hooks, MCPs, and CLAUDE.md files
- **Builds a personalized curriculum** — skips what you already know, focuses on gaps that matter
- **Teaches through real tasks** — every lesson produces an artifact you actually use (a hook, a CLAUDE.md, a command)
- **Tracks progress** — completion, streaks, skips
- **Stays current** — discovers new Claude Code features and community tips via web research

## Install

```bash
claude plugin add martarodriguez-wt/level-up
```

Or clone and install locally:

```bash
git clone https://github.com/martarodriguez-wt/level-up.git
claude plugin add ./level-up
```

## Usage

| Command | What It Does |
|---------|-------------|
| `/level-up` | Next lesson |
| `/level-up --status` | Progress dashboard |
| `/level-up --skip` | Skip current lesson |
| `/level-up --topic hooks` | Jump to a specific topic |
| `/level-up --refresh` | Discover new tips from the web |
| `/level-up --redo T1-01` | Redo a completed lesson |

You can also invoke the coach agent directly for ad-hoc questions about your setup.

## Curriculum

### Tier 1: Fill the Gaps
Common setup gaps that hurt your daily workflow.

| Lesson | Concept | Time |
|--------|---------|------|
| Root CLAUDE.md | Project context | 8 min |
| Your First Hook | Hooks | 10 min |
| Session-Start Context Hook | Hooks | 7 min |

### Tier 2: Deepen What You Have
Make your existing tools more powerful.

| Lesson | Concept | Time |
|--------|---------|------|
| Hierarchical CLAUDE.md | Project context | 10 min |
| Mermaid in Strategy Docs | Visual tools | 8 min |
| Agent Audit | Agents | 12 min |
| Memory Architecture | Memory | 10 min |
| Skill Composition | Skills | 10 min |

### Tier 3: New Capabilities
Things you probably haven't tried yet.

| Lesson | Concept | Time |
|--------|---------|------|
| /fork for A/B Prompt Testing | Context management | 6 min |
| Voice Input | Input methods | 10 min |
| Headless Batch Processing | Automation | 10 min |
| Custom Keybindings | Efficiency | 5 min |
| Multi-Perspective Parallel Review | Parallel agents | 8 min |

### Tier 4: Frontier
Auto-populated by `/level-up --refresh` — new features from Anthropic changelogs and community sources.

## How It Works

**First run:** The coach agent scans your `.claude/` directory, asks about your role, and personalizes the curriculum. Lessons you've already mastered are auto-completed.

**Each lesson:**
1. Explains **why** this matters for your specific workflow
2. Describes what you'll **build** (a real artifact, not an exercise)
3. Walks you through the steps using your actual files
4. Verifies it worked
5. Explains the underlying concept so you can apply it elsewhere

**Progress** is tracked in `data/progress.json`. The curriculum adapts as you complete lessons and as new features are discovered.

## Topics

Available topics for `--topic` flag:
- `project-context` — CLAUDE.md files and project memory
- `hooks` — Quality gates and automation triggers
- `visual-tools` — Mermaid diagrams and visual documentation
- `agents` — Agent design, audit, and optimization
- `memory` — Memory architecture and knowledge management
- `skills` — Skill creation and composition
- `context-management` — /fork, /compact, handoff docs
- `input-methods` — Voice input, dictation
- `automation` — Headless mode, batch processing, scheduled tasks
- `efficiency` — Keybindings, shortcuts, workflow optimization
- `parallel-agents` — Multi-agent parallel execution

## Plugin Structure

```
level-up/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── agents/
│   └── coach.md             # Coaching persona
├── commands/
│   ├── level-up.md          # Main entry point
│   ├── level-up-status.md   # Progress dashboard
│   └── level-up-refresh.md  # Discovery engine
├── data/
│   ├── curriculum.json      # Lesson plan (13 lessons, 4 tiers)
│   ├── progress.json        # User progress (auto-populated)
│   └── discoveries.json     # Web research findings
├── lesson-templates/        # One template per lesson (13 files)
│   ├── T1-01-root-claudemd.md
│   ├── T1-02-first-hook.md
│   └── ...
├── README.md
└── LICENSE
```

## Contributing

To add a lesson:
1. Create a template in `lesson-templates/` following the existing format
2. Add the lesson to `data/curriculum.json` in the appropriate tier
3. Submit a PR

## License

MIT

# Claude Code Knowledge Graph

> This file is the source of truth for what Claude Code can do and what "good" looks like.
> Refresh with `/level-up --refresh` to pull new features from official docs.
> Last refreshed: 2026-03-12

## How to Read This File

Each concept has:
- **Dependencies** — what must be at level 1+ before this concept is teachable
- **Detection** — how to assess what the user currently has
- **Maturity levels** — what absent / basic / functional / optimized looks like
- **Anti-patterns** — common mistakes to diagnose
- **Best practices** — what to teach at each level transition

---

## project-context

**What:** CLAUDE.md files that give Claude project context at session start.

**Dependencies:** none

**Detection:**
- Check for CLAUDE.md or .claude/CLAUDE.md at project root
- Check for ~/.claude/CLAUDE.md (user-level)
- Check for .claude/rules/*.md files
- Count lines, check for section headers, conventions, gotchas

**Maturity:**
- **0 Absent:** No CLAUDE.md exists anywhere in the project
- **1 Present:** CLAUDE.md exists but is under 20 lines or unstructured (wall of text, no headers)
- **2 Functional:** CLAUDE.md has clear sections (role, stack, conventions, commands), 30-150 lines, but no sub-folder files or rules
- **3 Optimized:** Root CLAUDE.md + .claude/rules/ with path-specific rules, or hierarchical CLAUDE.md in subdirectories. Under 200 lines each. User-level ~/.claude/CLAUDE.md for cross-project preferences.

**Anti-patterns:**
- Over 300 lines (Claude skims or ignores the tail)
- Generic instructions ("write clean code") instead of specific conventions ("2-space indentation, no semicolons")
- Duplicating information available in package.json or README
- No structure — a paragraph instead of sections

**Level transitions:**
- 0→1: Create a CLAUDE.md with role, tech stack, key commands, and 3 conventions
- 1→2: Add sections for gotchas, file structure, and tool configuration. Make instructions specific and verifiable.
- 2→3: Add .claude/rules/ for path-specific context (e.g., frontend vs backend). Add ~/.claude/CLAUDE.md for personal preferences. Use @imports for shared context.

---

## hooks

**What:** Deterministic scripts or prompts that fire at lifecycle events (PreToolUse, PostToolUse, SessionStart, Stop, etc.). Unlike CLAUDE.md which is a suggestion, hooks guarantee execution.

**Dependencies:** none

**Detection:**
- Check .claude/settings.json and ~/.claude/settings.json for "hooks" key
- Check .claude/agents/*.md frontmatter for hooks
- Check .claude/skills/*/SKILL.md frontmatter for hooks
- List hook event types in use

**Maturity:**
- **0 Absent:** No hooks configured anywhere
- **1 Present:** 1-2 hooks, usually PostToolUse or SessionStart, command type only
- **2 Functional:** 3-5 hooks covering 2-3 event types, mix of command and prompt types, basic matchers
- **3 Optimized:** 5+ hooks across 4+ event types (including PreToolUse for safety, Stop for verification), mix of command/prompt/agent types, specific matchers, proper error handling with exit codes

**Anti-patterns:**
- Hooks without matchers (fires on every tool use — noisy and slow)
- No error handling (silent failures)
- Echo statements in shell profiles breaking hook JSON parsing
- Hooks that are too slow (blocking the session for >5 seconds)

**Level transitions:**
- 0→1: Create a PostToolUse hook on Write that validates output formatting. Explain the hook lifecycle and why hooks differ from CLAUDE.md instructions.
- 1→2: Add a PreToolUse hook that catches dangerous Bash commands. Add a SessionStart hook for context loading. Introduce prompt-type hooks.
- 2→3: Add Stop hooks for task verification. Use agent-type hooks for complex validation. Add matchers to limit scope. Implement JSON output for structured control.

---

## agents

**What:** Specialized AI personas with their own system prompts, tool restrictions, and models. Run in isolated contexts.

**Dependencies:** none

**Detection:**
- List files in .claude/agents/ and ~/.claude/agents/
- For each agent file, read: description, tools, model, and system prompt quality
- Check for overlapping mandates between agents
- Check if tools are restricted or defaulting to inherit-all

**Maturity:**
- **0 Absent:** No custom agents
- **1 Present:** 1-3 agents with generic descriptions and no tool restrictions
- **2 Functional:** 3-7 agents with specific descriptions, explicit tool lists, and clear mandates. But some overlap or generic prompts remain.
- **3 Optimized:** Non-overlapping agents with narrow mandates, domain-specific knowledge, explicit "do NOT cover" instructions, distinct communication styles, appropriate model choices (haiku for read-only, opus for reasoning), and tool restrictions matching their role.

**Anti-patterns:**
- Multiple agents that produce the same feedback on the same input
- Generic descriptions ("You are a helpful assistant who reviews code")
- All agents inheriting all tools (no restriction)
- No model specification (expensive models for simple read tasks)
- Agents without "do NOT cover" boundaries

**Level transitions:**
- 0→1: Create 2-3 agents for your most common review perspectives. Give each a clear role.
- 1→2: Restrict tools per agent (read-only agents get Read/Grep/Glob only). Add domain-specific knowledge to prompts. Set model per agent.
- 2→3: Audit by running the same document through all agents and comparing outputs. Merge overlapping agents. Add "do NOT cover" instructions. Add memory for agents that learn. Set permissionMode per agent.

---

## commands

**What:** Reusable prompt templates invoked via /command-name. Markdown files with YAML frontmatter.

**Dependencies:** none

**Detection:**
- List files in .claude/commands/ and ~/.claude/commands/
- Check frontmatter: does each command have name and description?
- Check if commands use $ARGUMENTS for parameterization
- Check for hardcoded paths vs portable references

**Maturity:**
- **0 Absent:** No custom commands
- **1 Present:** 1-3 commands with basic prompts, no frontmatter or minimal frontmatter
- **2 Functional:** 3-7 commands with proper frontmatter (name, description), parameterized with $ARGUMENTS, clear instructions
- **3 Optimized:** Commands with full frontmatter, composable (one command can reference another), well-documented descriptions for auto-discovery, argument hints, and appropriate tool restrictions

**Anti-patterns:**
- Commands without descriptions (invisible to auto-discovery)
- Hardcoded file paths instead of $ARGUMENTS
- Monolithic commands that try to do everything
- No parameterization (copy-paste the same command with different inputs)

**Level transitions:**
- 0→1: Identify a workflow you repeat weekly. Turn it into a command.
- 1→2: Add proper frontmatter. Parameterize with $ARGUMENTS. Write clear descriptions.
- 2→3: Compose commands (command A triggers command B). Add argument-hint for autocomplete. Consider converting complex commands to skills.

---

## skills

**What:** Rich, auto-triggering capabilities with supporting files. More powerful than commands — they have directories, reference docs, scripts, and progressive disclosure.

**Dependencies:** commands (level 1+) — understanding commands helps understand how skills differ

**Detection:**
- List directories in .claude/skills/ and ~/.claude/skills/
- For each skill, check SKILL.md: frontmatter quality, line count, supporting files
- Check if description triggers correctly (specific keywords vs vague)
- Check for progressive disclosure (brief overview → detailed steps → reference docs)

**Maturity:**
- **0 Absent:** No custom skills
- **1 Present:** 1-2 skills with basic SKILL.md, no supporting files
- **2 Functional:** Skills with proper frontmatter, supporting reference files, clear trigger descriptions
- **3 Optimized:** Skills with progressive disclosure (SKILL.md overview + references/ for details), scripts/ for automation, explicit allowed-tools, well-tuned trigger descriptions that auto-invoke reliably, and composition with other skills

**Anti-patterns:**
- SKILL.md over 1000 lines with no supporting files (monolith)
- Vague description that triggers on unrelated prompts (false positives)
- Missing trigger keywords in description (never auto-invokes)
- No supporting files when the skill has complex reference material

**Level transitions:**
- 0→1: Convert your most complex command into a skill. Add a SKILL.md with proper frontmatter.
- 1→2: Add supporting files (references/, templates/). Tune the description for auto-triggering. Add argument hints.
- 2→3: Implement progressive disclosure. Add scripts for automation. Compose with other skills or commands. Restrict allowed-tools.

---

## mcp-servers

**What:** External tool integrations (APIs, databases, services) accessible to Claude via Model Context Protocol.

**Dependencies:** none

**Detection:**
- Check .mcp.json (project scope) and ~/.claude.json (user scope)
- List configured servers and their types (http, stdio, sse)
- Check authentication method (hardcoded vs env vars vs OAuth)
- Check if servers are documented

**Maturity:**
- **0 Absent:** No MCP servers configured
- **1 Present:** 1-2 servers, possibly with hardcoded credentials
- **2 Functional:** 2-5 servers with env var authentication, project-scoped for team servers, user-scoped for personal tools
- **3 Optimized:** Servers with OAuth auth, proper scoping, documented in CLAUDE.md, tool search enabled for many servers, output token limits configured

**Anti-patterns:**
- Hardcoded API keys in .mcp.json (committed to git)
- All servers at user scope (team members can't use them)
- No documentation of available MCP tools in CLAUDE.md
- Too many servers without tool search (Claude can't find the right tool)

**Level transitions:**
- 0→1: Add one MCP server for a service you use daily. Use env vars for auth.
- 1→2: Scope servers appropriately (project vs user). Document available tools in CLAUDE.md.
- 2→3: Add OAuth for secure servers. Enable tool search. Configure output token limits. Add server descriptions.

---

## keybindings

**What:** Custom keyboard shortcuts mapped to Claude Code actions.

**Dependencies:** none

**Detection:**
- Check ~/.claude/keybindings.json exists and has bindings
- Count bindings, check which contexts are covered

**Maturity:**
- **0 Absent:** No keybindings.json or empty file
- **1 Present:** 1-5 bindings in 1 context
- **2 Functional:** 5-15 bindings across 3+ contexts, avoiding terminal conflicts
- **3 Optimized:** Full workflow coverage with chords, documented, compatible with vim mode if used

**Anti-patterns:**
- Rebinding Ctrl+C or Ctrl+D (breaks terminal)
- Conflicts with tmux/screen prefix keys
- Too many bindings to remember (over 30)

**Level transitions:**
- 0→1: Create keybindings.json with 3-5 shortcuts for your most-used actions.
- 1→2: Add bindings for multiple contexts (Chat, Global, Confirmation). Use chords for less common actions.
- 2→3: Full workflow coverage. Document bindings in CLAUDE.md.

---

## memory

**What:** Persistent auto-memory system that stores learnings, project context, and user preferences across sessions.

**Dependencies:** project-context (level 1+) — CLAUDE.md and memory work together

**Detection:**
- Check if auto-memory is enabled (not disabled in settings)
- Read MEMORY.md: line count, structure, categorization
- List topic files in memory directory
- Check if memories are focused (one topic each) vs sprawling

**Maturity:**
- **0 Absent:** Auto-memory disabled or MEMORY.md doesn't exist
- **1 Present:** Auto-memory enabled, MEMORY.md exists but is unstructured or sparse
- **2 Functional:** MEMORY.md is a categorized index under 200 lines, 3-5 topic files with clear frontmatter (name, description, type)
- **3 Optimized:** Well-organized memory with type prefixes (user_, project_, feedback_, reference_), archived outdated memories, regular curation, MEMORY.md reads like a table of contents

**Anti-patterns:**
- MEMORY.md over 200 lines (truncated, tail is lost)
- Memory files mixing multiple topics
- No frontmatter on memory files (Claude can't judge relevance)
- Stale memories that are no longer accurate
- Duplicating information that's in CLAUDE.md

**Level transitions:**
- 0→1: Enable auto-memory. Let it accumulate for a week.
- 1→2: Curate MEMORY.md into categories. Split large memories into focused topic files. Add frontmatter.
- 2→3: Implement naming conventions. Archive outdated memories. Schedule monthly curation. Ensure MEMORY.md stays under 200 lines.

---

## context-management

**What:** Techniques for managing conversation context: /fork, /compact, /clear, /rename, handoff documents.

**Dependencies:** none

**Detection:**
- Check session history for fork/compact/rename usage (indirect — ask user or check patterns)
- Look for NEXT-STEPS.md or handoff documents in project
- Check if user has a pattern of one-task-per-session

**Maturity:**
- **0 Absent:** User doesn't manage context (long, polluted sessions)
- **1 Present:** Uses /clear between tasks
- **2 Functional:** Uses /clear + /compact for long sessions + /rename for important sessions
- **3 Optimized:** Uses /fork for A/B testing, handoff docs for context transfer, /compact with custom instructions, systematic session naming for searchability

**Anti-patterns:**
- One endless session for multiple unrelated tasks (context pollution)
- Never using /clear (stale context degrades output quality)
- Losing important session context because sessions aren't named

**Level transitions:**
- 0→1: Adopt one-task-per-session discipline. Use /clear when switching tasks.
- 1→2: Use /compact for long sessions. Name important sessions with /rename. Resume sessions instead of re-explaining.
- 2→3: Use /fork to explore alternatives. Create handoff documents before /clear for complex ongoing work. Use /compact with custom summary instructions.

---

## parallel-execution

**What:** Running multiple agents, sessions, or worktrees simultaneously for throughput.

**Dependencies:** agents (level 1+)

**Detection:**
- Check if user has commands that spawn multiple agents
- Check for git worktrees (git worktree list)
- Look for patterns of parallel work in session history

**Maturity:**
- **0 Absent:** All work is sequential
- **1 Present:** Occasionally asks Claude to "do these in parallel"
- **2 Functional:** Has commands that launch parallel agents for specific workflows (e.g., multi-perspective review)
- **3 Optimized:** Systematic use of parallel agents for batch processing, git worktrees for parallel branch work, combined with proper synthesis of parallel results

**Anti-patterns:**
- Spawning too many parallel agents (diminishing returns past 5-7)
- No synthesis step (parallel results without comparison)
- Using parallel agents for dependent tasks (where order matters)

**Level transitions:**
- 0→1: Try asking Claude to research 3 options in parallel.
- 1→2: Create a command that launches multiple agents for a common workflow (e.g., multi-perspective document review).
- 2→3: Use git worktrees for parallel branch work. Implement batch processing scripts. Always include a synthesis step.

---

## headless-automation

**What:** Non-interactive Claude Code via `claude -p` for CI/CD, batch processing, and scripted workflows.

**Dependencies:** commands (level 1+)

**Detection:**
- Check for shell scripts that invoke `claude -p`
- Check CI/CD configs (.github/workflows/, .gitlab-ci.yml) for claude invocations
- Check for cron jobs or scheduled tasks using claude

**Maturity:**
- **0 Absent:** Only uses Claude interactively
- **1 Present:** Has used `claude -p` once or twice manually
- **2 Functional:** Has shell scripts using `claude -p` for batch tasks, with proper output handling
- **3 Optimized:** Full CI/CD integration, scheduled batch jobs, JSON output parsing, error handling, and retry logic

**Level transitions:**
- 0→1: Run `claude -p "summarize this file" < file.md` to see how headless mode works.
- 1→2: Create a batch script that processes multiple files with `claude -p`.
- 2→3: Integrate into CI/CD. Use `--output-format json` for structured output. Add error handling.

---

## model-configuration

**What:** Choosing the right model per task, configuring effort levels, and managing thinking budgets.

**Dependencies:** none

**Detection:**
- Check settings for model configuration
- Check agent files for per-agent model settings
- Check if user switches models contextually

**Maturity:**
- **0 Absent:** Uses default model for everything
- **1 Present:** Aware of model choices but uses one model
- **2 Functional:** Uses different models for different tasks (haiku for reads, opus for reasoning). Knows about effort levels.
- **3 Optimized:** Per-agent model configuration. Uses thinking mode for complex tasks. Fast mode for iteration. Effort level tuning per task type.

**Level transitions:**
- 0→1: Learn the model lineup (haiku/sonnet/opus) and when each is appropriate.
- 1→2: Set model per agent (haiku for Explore, opus for planning). Use Shift+Tab to cycle modes.
- 2→3: Configure effort levels. Use "ultrathink" for complex reasoning. Monitor costs with /cost.

---

## permissions-security

**What:** Permission rules, sandboxing, and security configuration.

**Dependencies:** none

**Detection:**
- Check settings for permissions configuration (allow/deny rules)
- Check sandbox configuration
- Check permission mode

**Maturity:**
- **0 Absent:** Default permissions, no customization
- **1 Present:** Basic permission mode set (e.g., acceptEdits)
- **2 Functional:** Specific allow/deny rules for tools and paths. Permission mode varies by context.
- **3 Optimized:** Fine-grained rules with wildcards, sandbox enabled with filesystem and network restrictions, hooks for conditional permission control.

**Level transitions:**
- 0→1: Review default permissions. Set explicit allow rules for your common tools.
- 1→2: Add deny rules for dangerous operations. Use plan mode for exploration.
- 2→3: Enable sandboxing. Add network restrictions. Use PreToolUse hooks for conditional validation.

---

## plugins

**What:** Packaged extensions that bundle skills, agents, hooks, and MCP servers for sharing.

**Dependencies:** skills (level 1+), agents (level 1+)

**Detection:**
- Check settings.json for enabledPlugins
- List installed plugins
- Check if user has created any plugins

**Maturity:**
- **0 Absent:** No plugins installed or only defaults
- **1 Present:** 1-5 plugins installed from marketplace
- **2 Functional:** 5-10 plugins curated for workflow. Understands which plugins do what.
- **3 Optimized:** Has created and published own plugins. Curates plugin set. Uses plugin hooks and MCP servers.

**Level transitions:**
- 0→1: Browse available plugins with /plugin. Install 2-3 relevant to your workflow.
- 1→2: Curate your plugin set. Disable unused plugins. Understand each plugin's capabilities.
- 2→3: Package your own skills/agents as a plugin. Publish for others. Use plugin settings for configuration.

---

## voice-input

**What:** Dictation for faster prompt input.

**Dependencies:** none

**Detection:**
- Check for dictation tools installed (SuperWhisper, MacWhisper)
- Check system dictation settings (macOS: System Settings → Keyboard → Dictation)

**Maturity:**
- **0 Absent:** Types everything
- **1 Present:** Knows dictation exists, uses system dictation occasionally
- **2 Functional:** Regular dictation use for complex prompts. Has a tool configured.
- **3 Optimized:** Custom vocabulary in dictation tool. Seamless workflow integration.

**Level transitions:**
- 0→1: Enable macOS built-in dictation (free, zero setup). Test with a complex prompt.
- 1→2: Use regularly for context-heavy prompts. Consider SuperWhisper for better accuracy.
- 2→3: Add custom vocabulary for your domain terms. Integrate into daily workflow.

---

## scheduled-tasks

**What:** Recurring or timed tasks via /loop, cron, or desktop scheduled tasks.

**Dependencies:** headless-automation (level 1+)

**Detection:**
- Check for /loop usage in session
- Check ~/.claude/scheduled-tasks/ for configured tasks
- Check crontab for claude invocations

**Maturity:**
- **0 Absent:** No scheduled tasks
- **1 Present:** Has used /loop once or has 1 scheduled task
- **2 Functional:** 2-3 scheduled tasks for monitoring or reporting. Proper intervals.
- **3 Optimized:** Comprehensive scheduled automation with notification hooks, error handling, and dashboard monitoring.

**Level transitions:**
- 0→1: Use /loop to monitor something for an afternoon (build status, deployment).
- 1→2: Create a recurring scheduled task for a weekly workflow.
- 2→3: Add notification hooks. Implement error handling. Monitor task health.

---

## output-styles

**What:** Communication style presets that change how Claude responds.

**Dependencies:** none

**Detection:**
- Check settings for outputStyle
- Check for custom styles in .claude/output-styles/

**Maturity:**
- **0 Absent:** Default style only
- **1 Present:** Has switched style once or twice
- **2 Functional:** Uses appropriate style per context (concise for quick tasks, explanatory for learning)
- **3 Optimized:** Custom output styles for different audiences (technical, executive, user-facing). Team convention documented.

**Level transitions:**
- 0→1: Try switching to "concise" for a session. Notice the difference.
- 1→2: Use different styles for different work modes.
- 2→3: Create custom styles for your team's communication needs.

---

## plan-mode

**What:** Read-only exploration mode where Claude researches and plans before making changes.

**Dependencies:** none

**Detection:**
- Check if user has used /plan or --permission-mode plan
- Look for plan files in ~/.claude/plans/

**Maturity:**
- **0 Absent:** Never uses plan mode
- **1 Present:** Has used /plan once or twice
- **2 Functional:** Consistently uses plan mode before multi-file changes. Reviews plans before approving.
- **3 Optimized:** Plan mode as default for exploration. Iterates on plans. Uses /rewind to refine. Combines with /fork for alternative plans.

**Level transitions:**
- 0→1: Use /plan before your next multi-file task. See how it changes the workflow.
- 1→2: Make it a habit: plan before any change touching 3+ files.
- 2→3: Use plan mode as default for unfamiliar code. Combine with /fork to compare approaches.

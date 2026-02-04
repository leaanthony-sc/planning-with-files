# Planning with Files

> **Work like Manus** — the AI agent company Meta acquired for **$2 billion**.

## Thank You

To everyone who starred, forked, and shared this skill — thank you. This project blew up in less than 24 hours, and the support from the community has been incredible.

If this skill helps you work smarter, that's all I wanted.

---

A Claude Code plugin that transforms your workflow to use persistent markdown files for planning, progress tracking, and knowledge storage — the exact pattern that made Manus worth billions.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://code.claude.com/docs/en/plugins)
[![Version](https://img.shields.io/badge/version-2.13.0-brightgreen)](https://github.com/leaanthony-sc/planning-with-files/releases)

## Quick Install

```bash
# Install the plugin
claude plugins install OthmanAdi/planning-with-files
```

That's it! Now use one of these commands in Claude Code:

| Command | Autocomplete | Description |
|---------|--------------|-------------|
| `/planning-with-files:plan` | Type `/plan` | Shorter command (v2.11.0+) |
| `/planning-with-files:start` | Type `/planning` | Original command |

**Alternative:** If you want `/planning-with-files` (without prefix), copy skills to your local folder:

```bash
# Optional: Copy skills for /planning-with-files command
cp -r ~/.claude/plugins/cache/planning-with-files/planning-with-files/*/skills/planning-with-files ~/.claude/skills/
```

**Windows (PowerShell):**
```powershell
# Install the plugin
claude plugins install OthmanAdi/planning-with-files

# Optional: Copy skills for /planning-with-files command
Copy-Item -Recurse -Path "$env:USERPROFILE\.claude\plugins\cache\planning-with-files\planning-with-files\*\skills\planning-with-files" -Destination "$env:USERPROFILE\.claude\skills\"
```

See [docs/installation.md](docs/installation.md) for installation instructions.

## Documentation

| Document | Description |
|----------|-------------|
| [Installation Guide](docs/installation.md) | How to install the plugin |
| [Quick Start](docs/quickstart.md) | 5-step guide to using the pattern |
| [Workflow Diagram](docs/workflow.md) | Visual diagram of how files and hooks interact |
| [Troubleshooting](docs/troubleshooting.md) | Common issues and solutions |

See [CHANGELOG.md](CHANGELOG.md) for version history.

## Why This Skill?

On December 29, 2025, [Meta acquired Manus for $2 billion](https://techcrunch.com/2025/12/29/meta-just-bought-manus-an-ai-startup-everyone-has-been-talking-about/). In just 8 months, Manus went from launch to $100M+ revenue. Their secret? **Context engineering**.

> "Markdown is my 'working memory' on disk. Since I process information iteratively and my active context has limits, Markdown files serve as scratch pads for notes, checkpoints for progress, building blocks for final deliverables."
> — Manus AI

## The Problem

Claude Code (and most AI agents) suffer from:

- **Volatile memory** — TodoWrite tool disappears on context reset
- **Goal drift** — After 50+ tool calls, original goals get forgotten
- **Hidden errors** — Failures aren't tracked, so the same mistakes repeat
- **Context stuffing** — Everything crammed into context instead of stored

## The Solution: 3-File Pattern

For every complex task, create THREE files:

```
task_plan.md      → Track phases and progress
findings.md       → Store research and findings
progress.md       → Session log and test results
```

### The Core Principle

```
Context Window = RAM (volatile, limited)
Filesystem = Disk (persistent, unlimited)

→ Anything important gets written to disk.
```

## Usage

Once installed, Claude will automatically:

1. **Create `task_plan.md`** before starting complex tasks
2. **Re-read plan** before major decisions (via PreToolUse hook)
3. **Remind you** to update status after file writes (via PostToolUse hook)
4. **Store findings** in `findings.md` instead of stuffing context
5. **Log errors** for future reference
6. **Verify completion** before stopping (via Stop hook)

Or invoke manually:
- `/planning-with-files:plan` - Type `/plan` to find in autocomplete (v2.11.0+)
- `/planning-with-files:start` - Type `/planning` to find in autocomplete
- `/planning-with-files` - Only if you copied skills to `~/.claude/skills/`

See [docs/quickstart.md](docs/quickstart.md) for the full 5-step guide.

## Session Recovery (NEW in v2.2.0)

When your context window fills up and you run `/clear`, this skill automatically recovers unsynced work from your previous session.

### Optimal Workflow

For the best experience, we recommend:

1. **Disable auto-compact** in Claude Code settings (use full context window)
2. **Start a fresh session** in your project
3. **Run `/planning-with-files`** when ready to work on a complex task
4. **Work until context fills up** (Claude will warn you)
5. **Run `/clear`** to start fresh
6. **Run `/planning-with-files`** again — it will automatically recover where you left off

### How Recovery Works

When you invoke `/planning-with-files`, the skill:

1. Checks for previous session data (stored in `~/.claude/projects/`)
2. Finds the last time planning files were updated
3. Extracts conversation that happened after (potentially lost context)
4. Shows a catchup report so you can sync planning files

This means even if context filled up before you could update your planning files, the skill will recover that context in your next session.

### Disabling Auto-Compact

To use the full context window without automatic compaction:

```bash
# In your Claude Code settings or .claude/settings.json
{
  "autoCompact": false
}
```

This lets you maximize context usage before manually clearing with `/clear`.

## Key Rules

1. **Create Plan First** — Never start without `task_plan.md`
2. **The 2-Action Rule** — Save findings after every 2 view/browser operations
3. **Log ALL Errors** — They help avoid repetition
4. **Never Repeat Failures** — Track attempts, mutate approach

## File Structure

```
planning-with-files/
├── commands/                # Plugin commands
│   ├── plan.md              # /planning-with-files:plan command
│   └── start.md             # /planning-with-files:start command
├── templates/               # Templates for planning files
├── scripts/                 # Helper scripts
├── docs/                    # Documentation
│   ├── installation.md
│   ├── quickstart.md
│   ├── workflow.md
│   └── troubleshooting.md
├── skills/                  # Claude Code skill
│   └── planning-with-files/
│       ├── SKILL.md
│       ├── examples.md
│       ├── reference.md
│       ├── templates/
│       └── scripts/
├── .claude-plugin/          # Plugin manifest
├── CHANGELOG.md
├── LICENSE
└── README.md
```

## The Manus Principles

| Principle | Implementation |
|-----------|----------------|
| Filesystem as memory | Store in files, not context |
| Attention manipulation | Re-read plan before decisions (hooks) |
| Error persistence | Log failures in plan file |
| Goal tracking | Checkboxes show progress |
| Completion verification | Stop hook checks all phases |

## When to Use

**Use this pattern for:**
- Multi-step tasks (3+ steps)
- Research tasks
- Building/creating projects
- Tasks spanning many tool calls

**Skip for:**
- Simple questions
- Single-file edits
- Quick lookups


## Acknowledgments

- **Manus AI** — For pioneering context engineering patterns
- **Anthropic** — For Claude Code, Agent Skills, and the Plugin system
- **Lance Martin** — For the detailed Manus architecture analysis
- Based on [Context Engineering for AI Agents](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus)

## Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License — feel free to use, modify, and distribute.

---

**Author:** [Ahmad Othman Ammar Adi](https://github.com/OthmanAdi)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=OthmanAdi/planning-with-files&type=Date)](https://star-history.com/#OthmanAdi/planning-with-files&Date)

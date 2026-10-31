---
name: learn-entire
description: Teach, configure, operate, and troubleshoot Entire (entire.com / entire.io) — the AI-native Git platform, CLI, Checkpoints, Trails, and agent session tracking. Use when working with entire, entire:// remotes, checkpoints, entire why, trails, or setting up agent hooks.
license: MIT
compatibility: Linux, macOS, or Windows with Git and Entire CLI (entire) installed.
metadata:
  author: Aawej Pathan
  version: 1.0.0
  homepage: https://entire.com
---

# Learn Entire

**Entire** (`entire.com` / `entire.io`) is an AI-native Git platform and forge founded by former GitHub CEO Thomas Dohmke. While GitHub was designed around human-written code diffs, Entire is built for **human + AI coding agent collaboration**, recording the *intent, conversation, and reasoning* behind every line of code as first-class Git metadata.

This skill equips agents and developers with the workflows, commands, and mental models to use Entire effectively.

---

## Quick Navigation (Progressive Disclosure)

When detailed reference or troubleshooting is needed, consult the companion documents:
- [Architecture & Core Concepts](references/architecture-and-concepts.md): Distributed Git clusters, `entire://` protocol, checkpoints, trails vs. PRs.
- [CLI Reference Guide](references/cli-reference.md): Complete list of commands, flags, and options for `entire`.
- [Checkpoints & Sessions](references/checkpoints-and-sessions.md): Checkpoint internals, git refs storage, token analysis, and `entire why`.
- [Trails & Multi-Agent Review](references/trails-and-code-review.md): Intent-driven code reviews, evaluations, and multi-repo changes.
- [Agent Integrations](references/agent-integrations.md): Hooking up Antigravity, Claude Code, Cursor, Codex, Pi, and OpenCode.
- [Troubleshooting & Diagnostics](references/troubleshooting.md): Fixing stuck sessions, hook drift, and running `entire doctor`.
- [Step-by-step Workflow Walkthrough](examples/basic-workflow.md): End-to-end recipe from repo init to trail creation.

---

## Core Mental Model

| Dimension | GitHub | Entire |
| :--- | :--- | :--- |
| **Primary Unit of Work** | Commit & Pull Request | Commit + Checkpoint & Trail |
| **Ground Truth** | Code only | Code + Agent Intent (Prompts, Sessions, Tools) |
| **Blame (`git blame`)** | Who wrote the line & commit date | **`entire why`**: What prompt & agent session created the line |
| **Code Review** | Line-by-line manual human diff inspection | **Trails**: Multi-agent automated evaluations + human gatekeeping |
| **Search** | Keyword grep on code | **`entire search`**: Hybrid semantic + keyword search over code & prompts |
| **Protocol** | `https://` or `git@github.com:...` | `entire://<cluster-endpoint>/et/<org>/<repo>` or GitHub Mirrors |

---

## Operational Workflows

### 1. Enabling Entire in a Repository
Before Entire can capture sessions, hook integration must be enabled:
```bash
# Enable in current repo with interactive agent picker
entire enable

# Or enable non-interactively for a specific agent (e.g. antigravity or claude-code)
entire enable --agent antigravity -y
```
**Completion Criterion:**
- `.entire/settings.json` is created.
- Agent hook config is added to `.agents/hooks.json` (or `.claude/settings.json`).
- Git hooks (`prepare-commit-msg`, `post-commit`, `pre-push`) exist in `.git/hooks/`.
- `entire status` shows `● Enabled`.

### 2. Inspecting Intent with `entire why`
Whenever someone asks *"Why does this code exist?"* or *"Who wrote this logic?"*:
```bash
# Trace a specific file and line back to the exact prompt and agent session
entire why <path/to/file>:<line>

# Output machine-readable JSON
entire why <path/to/file>:<line> --json
```

### 3. Checkpoint Management
Every commit created while an agent session is active receives an `Entire-Checkpoint` trailer.
- **List checkpoints:** `entire checkpoint list`
- **Inspect session & transcript:** `entire checkpoint explain <checkpoint-id|commit-sha>`
- **Analyze token consumption:** `entire checkpoint tokens <checkpoint-id>`
- **Semantic search:** `entire search "retry backoff logic" --compact`

### 4. Working with Trails (The Modern PR)
Trails capture cross-branch and cross-repo intent with evaluation-driven reviews:
```bash
# Create a trail from the current branch
entire trail create --title "feat: implement caching layer"

# View trail status and web link
entire trail show <trail-id>

# Run or review agent evaluation findings
entire trail finding list <trail-id>

# Resume an agent session directly on the trail's branch
entire trail resume <trail-id>
```

### 5. Repository Health & Diagnostics
If hooks fail to trigger or sessions become disconnected:
```bash
# Run automated diagnostics
entire doctor

# Auto-fix stuck sessions and hook drift
entire doctor --force
```

---

## Best Practices for AI Agents

1. **Keep Context Clean:** Before running heavy search queries, use `entire search --compact` or `entire search --json` to get trimmed token-efficient output.
2. **Preserve Git Trailers:** Never strip the `Entire-Checkpoint: <id>` trailer from commit messages during rebases or squashes.
3. **Trace Before Modifying:** When refactoring unfamiliar code in an Entire repository, run `entire why <file>:<line>` first to understand the original intent before deleting or changing logic.

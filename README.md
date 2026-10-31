# learn-entire Agent Skill

An open agent skill following the [Agent Skills standard](https://agentskills.io) to teach, operate, and troubleshoot **Entire** (`entire.com` / `entire.io`) — the AI-native Git platform and forge for human + AI agent collaboration.

## Installation via skills.sh (Recommended)

You can install this skill into any project or globally across all supported AI coding agents (Antigravity, Claude Code, Cursor, Codex, Cline, etc.) using the [`skills.sh`](https://skills.sh) CLI:

```bash
# Install to your current project
npx skills add atpaawej/learn-entire

# Or install globally across all agents
npx skills add atpaawej/learn-entire -g
```

To preview available skills before installing:
```bash
npx skills add atpaawej/learn-entire --list
```

---

## Directory Structure
```text
learn-entire/
├── SKILL.md                          # Main skill file with frontmatter and instructions
├── LICENSE                           # MIT License
├── README.md                         # This file
├── references/
│   ├── architecture-and-concepts.md  # Deep dive into clusters, protocols, and intent
│   ├── cli-reference.md              # Complete CLI commands and flags reference
│   ├── checkpoints-and-sessions.md   # Checkpoint storage, hooks, and why-pipeline
│   ├── trails-and-code-review.md     # Multi-agent review, findings, and trails vs PRs
│   ├── agent-integrations.md         # Antigravity, Claude Code, Cursor, Codex hooks
│   └── troubleshooting.md            # Diagnosing stuck sessions and entire doctor
└── examples/
    ├── basic-workflow.md             # End-to-end recipe from git init to trail
    └── sample-settings.json          # Example .entire/settings.json configuration
```

## Manual Installation (Alternative)
```bash
# Clone directly into your personal agent skills
git clone https://github.com/atpaawej/learn-entire.git ~/.gemini/config/skills/learn-entire

# Or in a project repository
mkdir -p .agents/skills
git clone https://github.com/atpaawej/learn-entire.git .agents/skills/learn-entire
```

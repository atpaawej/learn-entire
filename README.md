# learn-entire Agent Skill

An open agent skill following the [Agent Skills standard](https://agentskills.io) to teach, operate, and troubleshoot **Entire** (`entire.com` / `entire.io`) — the AI-native Git platform and forge for human + AI agent collaboration.

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

## How to Install / Use in Agents

### In Antigravity / Claude Code / Agent Platforms
Copy the `learn-entire` directory into your project's `.agents/skills/` or your global skills directory:
```bash
cp -r learn-entire ~/.gemini/config/skills/
# or in a project repository
mkdir -p .agents/skills
cp -r learn-entire .agents/skills/
```

Whenever the agent is asked about Entire, `entire://` remotes, checkpoints, `entire why`, trails, or debugging session hooks, the agent automatically activates this skill.

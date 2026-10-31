# Agent Integrations Guide

Entire bridges with coding agents by attaching hooks to their prompt and tool execution lifecycles.

---

## Supported Agents

Entire natively supports major AI coding environments:
- **Google Antigravity (`antigravity`)**
- **Anthropic Claude Code (`claude-code`)**
- **Cursor (`cursor`)**
- **OpenAI Codex (`codex`)**
- **Pi (`pi`)**
- **OpenCode (`opencode`)**

---

## 1. How Agent Hooks Work

When an agent is configured, Entire installs hook manifests:

### For Antigravity (`.agents/hooks.json`)
Registers hook handlers for prompt lifecycle events:
- `onPromptStart`: Creates a session entry in `.entire/tmp/pre-prompt-<session-id>.json`.
- `onToolCall`: Logs tool names, arguments, and file modifications.
- `onPromptEnd`: Updates session token counts and interaction status.

### For Claude Code (`.claude/settings.json`)
Injects pre-command and post-command matchers into the Claude Code configuration so every Claude CLI turn records checkpoint telemetry.

---

## 2. Managing Agents with the CLI

### Listing Agents
```bash
$ entire agent list
Installed agents:
  ● Antigravity   (active in this worktree)
  ● Claude Code

Available agents:
  ○ Codex
  ○ Cursor
  ○ Pi
  ○ OpenCode
```

### Adding an Agent
To install hooks for a new agent without re-running full setup:
```bash
entire agent add cursor
```

### Removing an Agent
```bash
entire agent remove codex
```

### Force Re-installing Hooks
If an agent updates its internal configuration format and hooks stop firing:
```bash
entire agent add <agent-name> --force
```

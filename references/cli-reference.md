# Entire CLI Reference Guide

The Entire CLI (`entire`) is the primary interface for managing agent hooks, inspecting checkpoints, running semantic searches, and reviewing trails.

---

## Setup & Environment

### `entire enable`
Initializes Entire tracking in the current repository.
```bash
entire enable [flags]
```
**Flags:**
- `--agent <string>`: Specify agent hooks to install (`antigravity`, `claude-code`, `codex`, `cursor`, `pi`, `opencode`).
- `-y, --yes`: Accept all defaults non-interactively.
- `--checkpoint-backend <refs|branch>`: Storage strategy (defaults to `refs`).
- `--local`: Write settings to `.entire/settings.local.json` instead of `.entire/settings.json`.
- `--force`: Reinstall hooks, replacing existing Entire hooks.

### `entire status`
Displays the active tracking state, configured agents, checkpoint remote, and currently active sessions in the worktree.
```bash
entire status
```

### `entire agent`
Manages AI agent integrations.
```bash
entire agent list            # Show installed and supported agents
entire agent add <agent>     # Install hooks for an agent
entire agent remove <agent>  # Remove agent hooks
```

---

## Sessions & Checkpoints

### `entire why`
Explains the intent behind a file or specific line.
```bash
entire why <file>:<line>
entire why <file> --line 42 --json
```

### `entire checkpoint`
Operations on checkpoints tied to Git commits.
```bash
entire checkpoint list                       # List checkpoints on the current branch
entire checkpoint explain <id|sha>          # Show intent, transcript, and touched files
entire checkpoint explain --generate <id>    # Generate an AI summary for the checkpoint
entire checkpoint tokens <id>               # Show input/output/cache tokens
entire checkpoint search "<query>"           # Search within checkpoints
entire checkpoint delete <id>               # Delete a checkpoint
```

### `entire session`
Inspects and manages live agent sessions.
```bash
entire session list                          # List all active/recent sessions
entire session current                       # Show session in current directory
entire session info <session-id>             # Detailed session transcript and metadata
entire session tokens <session-id>           # Token stats for session
entire session resume <branch>               # Switch branch and restore session state
entire session stop                          # Stop active sessions
```

### `entire search`
Hybrid semantic and keyword search across code, commits, prompts, and checkpoints.
```bash
entire search "<query>"                      # Interactive search table
entire search "<query>" --json --compact     # Agent-friendly trimmed output
entire search --code "<symbol>"              # Cross-repository code search
entire search "auth timeout author:alice"    # Filtered search
```

---

## Trails (Agent-Native Code Review)

### `entire trail`
Manages project trails across repositories and branches.
```bash
entire trail list --project <org/project>    # List open trails
entire trail create --title "<title>"        # Open a new trail from current branch
entire trail show <trail-id>                 # Display trail status, URL, and discussions
entire trail watch <trail-id>                # Stream real-time trail updates
entire trail finding list <trail-id>         # Inspect evaluation findings
entire trail comment <trail-id> -m "looks good" # Add discussion comment
entire trail approve <trail-id>              # Approve trail
entire trail merge <trail-id>                # Merge changes into base branch
```

---

## Summaries & Diagnostics

### `entire dispatch`
Generates a consolidated dispatch summarizing recent agent work across repos.
```bash
entire dispatch                              # Generate cloud dispatch
entire dispatch --local --all-branches       # Local summary using installed agent
```

### `entire recap`
Interactive or static view of recent checkpoint activity and contributor breakdown.
```bash
entire recap --day                           # Today's activity
entire recap --week --static                 # Last 7 days in plain text
```

### `entire doctor`
Scans for stuck sessions, hook drift, or broken metadata refs.
```bash
entire doctor                                # Interactive diagnosis
entire doctor --force                        # Auto-fix all identified issues
```

# Troubleshooting & Diagnostics

## 1. Running Automated Diagnostics (`entire doctor`)

The first step when encountering issues with Entire is running `entire doctor`.

```bash
entire doctor
```

To automatically repair issues without interactive prompts:
```bash
entire doctor --force
```

### Common Issues Detected by `entire doctor`

| Check | Cause | Resolution |
| :--- | :--- | :--- |
| **Stuck Sessions** | A session remained active for > 1 hour with no activity, or an agent process terminated abruptly before condensing data. | Run `entire doctor --force` to condense fixable data and discard orphaned states. |
| **Hook Drift** | An agent CLI upgraded its hook schema, causing old Entire hooks in `.agents/` or `.claude/` to stop receiving events. | Run `entire agent add <agent> --force`. |
| **Log Directory Unwritable** | `.entire/logs/` has incorrect file permissions, silently failing telemetry logging. | Check directory ownership: `chmod -R u+rwX .entire/logs`. |
| **Disconnected Metadata Branches** | Older Entire versions created split branches without a common ancestor. | `entire doctor` automatically cherry-picks local checkpoints onto the remote tip. |

---

## 2. Keychain & Sandbox Permissions

When running commands that interact with the Entire cloud forge (e.g., `entire trail` or `entire search`), the CLI reads authentication tokens from the operating system keyring (e.g., macOS Keychain, Linux secret-service).

> **Warning:** If running inside a sandboxed terminal or container without keyring access, you may see errors like:
> `Keyring is not accessible` or `Network access denied`.
> 
> **Fix:** Run the command in an unsandboxed terminal. Do **not** run `entire login` in a loop inside a restricted sandbox.

---

## 3. Commit Created Without `Entire-Checkpoint` Trailer

If you committed code but do not see `Entire-Checkpoint: <ID>` in `git log`:
1. Check if Entire is enabled:
   ```bash
   entire status
   ```
2. Verify that `.git/hooks/prepare-commit-msg` exists and is executable:
   ```bash
   chmod +x .git/hooks/prepare-commit-msg
   ```
3. Ensure an agent was active during the turn. Commits made purely by hand without any agent session in progress may not carry checkpoint data unless session adoption was initiated.

---

## 4. Resetting or Cleaning Session Data

To clean up stale session logs or temp files safely:
```bash
# Preview what would be cleaned
entire clean --dry-run

# Clean orphaned session data
entire clean
```

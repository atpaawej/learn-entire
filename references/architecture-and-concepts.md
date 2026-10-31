# Entire Architecture & Core Concepts

## 1. What is Entire?
Entire is an AI-first Git platform founded by Thomas Dohmke (former CEO of GitHub). It addresses the fundamental shift in software engineering: while Git was created to coordinate distributed human text edits, modern software development increasingly involves AI coding agents creating, revising, and refactoring large volumes of code autonomously.

Entire combines:
1. **A high-throughput distributed Git forge:** Multi-region Git clusters that scale to millions of concurrent agent commits without rate-limiting.
2. **Intent & Provenance Layer (Checkpoints):** Cryptographically binds prompts, session transcripts, tool calls, and model tokens directly to Git commits.
3. **Multi-Agent Review System (Trails):** Replaces legacy human line-by-line Pull Requests with evaluation-driven trails capable of spanning multiple repositories and branches.

---

## 2. The Entire Remote Protocol (`entire://`)
Repositories hosted natively on Entire use the custom `entire://` protocol:

```text
entire://<cluster-endpoint>/et/<project-or-user>/<repo-name>
```

Example:
```text
origin entire://aws-ap-south-1.entire.io/et/atpaawej/hello-world
```

### Git Mirrors
Entire also supports bidirectional mirroring with GitHub and GitLab. When mirrored:
- Your team can keep their public code on GitHub (`gh/<org>/<repo>`).
- Fast agents clone and push to the nearest regional Entire cluster.
- Checkpoints and trails remain synchronized across both environments.

---

## 3. The Core Hierarchy

### Sessions
A **Session** represents a single continuous interaction between a human and a specific AI agent (e.g. Antigravity, Claude Code, Cursor). A session has a unique ID (such as a UUID) and logs:
- User prompts and timestamps.
- Agent internal reasoning and messages.
- Tool invocations (file reads, edits, bash commands).
- Token usage (input, output, cache hit rates).

### Checkpoints
A **Checkpoint** is a point-in-time snapshot of an agent session tied to a specific Git commit SHA. Checkpoints are stored in dedicated Git refs (`refs/entire/checkpoints/*`) or metadata branches.
- Commits are linked to checkpoints using the Git commit message trailer:
  ```text
  Entire-Checkpoint: 01M69CNHH9D2092QYTZJ9FMEQ0
  ```
- Because checkpoints live inside Git itself, cloning or fetching preserves the complete provenance history without external database dependencies.

### Trails
A **Trail** is the Entire alternative to a Pull Request.
- **Project-Scoped:** A trail can coordinate changes across multiple repositories and multiple branches simultaneously.
- **Evaluation-Driven:** Instead of waiting for a human to manually read diffs, specialized evaluation agents run against the trail, generating structured findings, test validations, and security assessments.
- **Session Continuity:** Any developer or agent can run `entire trail resume <id>` to instantly load the branch with the full preceding agent conversational context intact.

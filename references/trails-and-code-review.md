# Trails & The Evolution of Code Review

## Why Pull Requests Break Down with Coding Agents

The standard GitHub Pull Request (PR) was designed around human constraints:
1. **Limited Diff Volume:** Humans can comfortably review 200–400 lines of code. When coding agents generate 2,000+ lines in minutes, manual diff inspection becomes a bottleneck and leads to rubber-stamping.
2. **Loss of Context:** A PR diff shows *what* changed, but lacks the rationale for *why* specific trade-offs were made.
3. **Single-Repository Scope:** Modern systems often require coordinating changes across frontend, backend, schemas, and infrastructure. Managing multiple correlated PRs on GitHub requires complex orchestration.

---

## What is an Entire Trail?

A **Trail** is an intent-first, evaluation-driven code review unit designed for the agent era.

### 1. Multi-Repo and Cross-Branch Scope
A single project trail can encapsulate changes across multiple repositories and branches. For example, a trail titled `feat: add payment gateway` can bundle:
- `gh/acme/backend` on branch `feature/payment`
- `gh/acme/frontend` on branch `feature/payment-ui`
- `gh/acme/contracts` on branch `schema/v2`

### 2. Evaluation Findings (`entire trail finding`)
Instead of human reviewers scanning every line for syntax or style errors:
- **Evaluation Agents** run automated suites (security audits, architecture rule checks, performance benchmarks, regression tests).
- Issues are recorded as structured **Findings** attached to the trail.
- Coding agents can be prompted to address and clear findings iteratively before human review.

```bash
# View active findings on a trail
entire trail finding list <trail-id>
```

### 3. Contextual Session Handoff (`entire trail resume`)
On GitHub, if a colleague's PR needs adjustments, you must either leave comments or checkout their branch and guess how to prompt an agent from scratch.

On Entire:
```bash
entire trail resume <trail-id>
```
This command checks out the branch and **loads the active agent session**, allowing your local agent to continue where the original session left off with complete memory of previous prompts and rationale.

---

## The Trail Lifecycle

1. **Create Trail:** `entire trail create --title "feat: user notifications"`
2. **Automated Evaluations:** CI/CD and evaluation agents post findings.
3. **Resolve Findings:** Coding agents update code and checkpoints automatically.
4. **Human Gatekeeping:** Developers review the intent summary, verify passed evaluations, and approve:
   ```bash
   entire trail approve <trail-id>
   ```
5. **Merge:** Changes are merged into the target branch:
   ```bash
   entire trail merge <trail-id>
   ```

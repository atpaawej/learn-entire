# End-to-End Entire Workflow Example

This guide walks through creating a repository, developing with an AI coding agent, capturing checkpoints, using `entire why`, and publishing a Trail.

---

### Step 1: Initialize Repository & Enable Entire
```bash
# Create and enter project directory
mkdir my-service && cd my-service
git init

# Enable Entire with your preferred agent
entire enable --agent antigravity -y
```

### Step 2: Develop with Your Agent
Prompt your agent to create your application files. For example:
- `src/main.py`
- `README.md`
- `pyproject.toml`

### Step 3: Commit Changes
Commit your changes through Git:
```bash
git add .
git commit -m "feat: initial service implementation"
```
Notice that Entire automatically attaches a checkpoint:
```text
Entire-Checkpoint: 01M69CNHH9D2092QYTZJ9FMEQ0
```

### Step 4: Verify with `entire why`
Test intent tracing on any generated line:
```bash
entire why src/main.py:10
```
Output:
```text
Line 10 in src/main.py
Checkpoint from Antigravity · checkpoint 01M... · session ...
Prompt: "Create a FastAPI service with a health check endpoint"
```

### Step 5: Push to Origin
```bash
git remote add origin entire://aws-ap-south-1.entire.io/et/my-org/my-service
git push -u origin main
```
Entire pushes both the standard Git commits and all checkpoint refs to the forge cluster.

### Step 6: Create a Trail for Code Review
When working on a feature branch:
```bash
git checkout -b feature/auth
# ... make changes and commit ...
git push origin feature/auth

# Open a Trail
entire trail create --title "feat: implement JWT authentication"
```
Your team and automated evaluation agents can now review findings, inspect prompts, and resume sessions directly.

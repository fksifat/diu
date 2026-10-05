# Google Antigravity CLI & OpenAI Codex CLI
## Complete Setup, Configuration, Usage, and Developer Workflow Guide

**Last reviewed:** October 2026

---

# 1. Overview

This document explains how to install, authenticate, configure, and effectively use two modern terminal-based AI coding agents:

1. **Google Antigravity CLI**
2. **OpenAI Codex CLI**

Both tools allow developers to work with AI coding agents directly from a terminal.

Instead of manually asking an AI:

```text
"How do I implement this?"
```

you can give an agent access to a project and ask it to:

```text
Inspect the repository
Understand the architecture
Plan the implementation
Modify files
Run tests
Debug failures
Review the changes
```

The key difference is that these tools are designed around **agentic software development**, rather than simple text generation.

---

# 2. What Is Antigravity CLI?

Google Antigravity CLI is the terminal-first interface for Google's Antigravity agent system.

It provides a lightweight Terminal User Interface (TUI) for:

- Reading repositories
- Editing files
- Running commands
- Debugging
- Multi-file development
- Agent orchestration
- Subagents
- MCP/skills/plugins
- Conversation history
- Workspace configuration

Google describes the CLI as a lightweight terminal surface sharing the same core agent harness as Antigravity 2.0.

The executable is:

```bash
agy
```

---

# 3. What Is Codex CLI?

Codex CLI is OpenAI's local coding agent that runs directly on your computer.

It can work with a local repository and perform software-development tasks such as:

```text
Repository analysis
Code generation
Code modification
Debugging
Testing
Refactoring
Code review
Multi-file changes
Terminal operations
```

The official Codex repository provides standalone installers as well as npm and Homebrew installation options.

The executable is:

```bash
codex
```

---

# 4. System Requirements

## 4.1 Antigravity CLI

Antigravity CLI supports:

```text
macOS
Linux
Windows
```

The current official installer automatically places the executable in a user-level directory.

For macOS/Linux:

```text
~/.local/bin/agy
```

For Windows:

```text
C:\Users\<username>\AppData\Local\agy\bin
```


---

## 4.2 Antigravity IDE Requirements

If you also want the full Antigravity desktop application:

### Linux

Current requirements include:

```text
glibc >= 2.28
glibcxx >= 3.4.25
```

Examples include:

```text
Ubuntu 20+
Debian 10+
Fedora 36+
RHEL 8+
```


---

## 4.3 Codex CLI

Codex CLI supports:

```text
macOS
Linux
Windows
```

It can be installed using:

```text
Official installer
npm
Homebrew
Standalone binaries
```


---

# 5. Installing Antigravity CLI

## 5.1 Linux

Open a terminal:

```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

The official installer installs the `agy` executable.

Restart your terminal if necessary.

Then verify:

```bash
agy
```

---

# 6. Installing Antigravity on macOS

Run:

```bash
curl -fsSL https://antigravity.google/cli/install.sh | bash
```

Then:

```bash
agy
```

The same installer is used for macOS and Linux.

---

# 7. Installing Antigravity on Windows

## PowerShell

Run:

```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

Then:

```powershell
agy
```

---

## Command Prompt

Run:

```cmd
curl -fsSL https://antigravity.google/cli/install.cmd -o install.cmd && install.cmd && del install.cmd
```

Then:

```cmd
agy
```


---

# 8. Antigravity Installation Options

The installer supports additional options.

### Skip aliases

```bash
--skip-aliases
```

This prevents the installer from changing legacy `agy`/`antigravity` aliases.

### Skip PATH modification

```bash
--skip-path
```

This prevents the installer from modifying your shell profile to add the CLI directory to PATH.


---

# 9. Verify Antigravity Installation

After installation:

```bash
agy
```

If the command starts the Antigravity TUI, installation succeeded.

You can also check the executable location:

```bash
which agy
```

Linux/macOS:

```bash
which agy
```

Windows PowerShell:

```powershell
Get-Command agy
```

---

# 10. First Antigravity Launch

Navigate to your project:

```bash
cd ~/Documents/my-project
```

Then:

```bash
agy
```

The first launch asks you to configure:

```text
Color scheme
Rendering mode
Workspace trust
```

After you trust the repository, Antigravity can index and work with the project.

---

# 11. Antigravity Workspace Trust

Workspace trust is important.

Only allow an AI agent to operate on repositories that you understand and trust.

A project may contain:

```text
Scripts
Shell commands
Package installation
Environment variables
Credentials
Deployment scripts
Database utilities
```

Never blindly execute commands suggested by an AI agent.

---

# 12. Antigravity Authentication

Antigravity supports several authentication approaches.

## Default account authentication

Start:

```bash
agy
```

If no existing session is available, Antigravity opens a browser authentication flow.

Sign in with your approved Google account.

The CLI can use the operating system's secure credential storage when available.

---

# 13. Antigravity Authentication Over SSH

If you connect to a remote Linux machine:

```bash
ssh user@server
```

and run:

```bash
agy
```

Antigravity detects the SSH environment.

Instead of opening a browser on the server, it provides an authorization URL.

Workflow:

```text
Remote server
     ↓
agy
     ↓
Authorization URL
     ↓
Open URL on local computer
     ↓
Google authentication
     ↓
Authorization code
     ↓
Paste code into SSH terminal
```


---

# 14. Using a Gemini API Key with Antigravity

Antigravity can also use a Gemini API key.

Configure:

```text
~/.gemini/antigravity-cli/settings.json
```

Set:

```json
{
  "modelProvider": "gemini"
}
```

Then:

```bash
export GEMINI_API_KEY="your-api-key"
```

Start:

```bash
agy
```

The official documentation states that `GEMINI_API_KEY` must be accompanied by:

```json
"modelProvider": "gemini"
```

Setting only the environment variable is not sufficient.

---

# 15. Persisting the Gemini API Key

For Bash:

```bash
echo 'export GEMINI_API_KEY="your-api-key"' >> ~/.bashrc
source ~/.bashrc
```

For Zsh:

```bash
echo 'export GEMINI_API_KEY="your-api-key"' >> ~/.zshrc
source ~/.zshrc
```

Never commit API keys to Git.

Do not put:

```text
GEMINI_API_KEY=...
```

inside a tracked source file.

---

# 16. Antigravity Configuration

Antigravity CLI stores its main configuration at:

```text
~/.gemini/antigravity-cli/settings.json
```

You can also access settings from inside the CLI:

```text
/config
```

or:

```text
/settings
```

The settings interface can control workspace behavior, permissions, appearance, and performance-related settings.

---

# 17. Antigravity Keybindings

Configuration file:

```text
~/.gemini/antigravity-cli/keybindings.json
```

Inside the CLI:

```text
/keybindings
```

You can customize keyboard shortcuts.

Useful defaults include:

```text
Enter       → Submit
Ctrl+C      → Cancel
Ctrl+D      → Exit
Ctrl+G      → Edit prompt
Ctrl+L      → Clear screen
Alt+Enter   → New line
```


---

# 18. Important Antigravity Commands

Antigravity provides slash commands.

Common commands include:

```text
/config
/settings
/permissions
/keybindings
/clear
/undo
/rewind
/fork
/resume
/agents
```

Useful workflow commands include:

```text
/goal
/grill-me
/schedule
/browser
/plugin
```


---

# 19. Antigravity Terminal Commands

Antigravity allows direct terminal interaction.

A command beginning with:

```text
!
```

can be used to execute terminal commands.

For example:

```text
!git status
```

or:

```text
!pytest
```

or:

```text
!docker ps
```

This is useful when you want explicit terminal control while staying inside the agent session.

---

# 20. Antigravity File References

The `@` character can trigger file-path suggestions.

For example:

```text
Review @src/main.py and fix the authentication bug.
```

This is useful for giving the agent focused context.

---

# 21. Your First Antigravity Task

Inside your repository:

```bash
cd my-project
agy
```

Start with:

```text
Analyze this repository.

Do not modify anything.

Explain:
1. Project architecture
2. Entry points
3. Main modules
4. Database structure
5. API structure
6. Testing strategy
7. Potential technical problems
```

This is a good first prompt because it establishes context before allowing modifications.

---

# 22. A Better Antigravity Coding Workflow

Use:

```text
Analyze
   ↓
Plan
   ↓
Implement
   ↓
Test
   ↓
Review
   ↓
Fix
   ↓
Verify
```

For example:

```text
First inspect the repository and understand the architecture.

Then propose an implementation plan.

Do not modify files until I approve the plan.
```

After reviewing the plan:

```text
Implement the approved plan.

After implementation:
1. Run the relevant tests.
2. Fix failures.
3. Review the diff.
4. Summarize all changes.
```

---

# 23. Antigravity Goals

For larger tasks, use:

```text
/goal
```

A goal should describe the desired outcome rather than a rigid sequence of commands.

Example:

```text
/goal
Migrate this FastAPI application from synchronous database access to async SQLAlchemy without breaking the existing API tests.
```

Goals are useful for tasks with a clear finish condition but uncertain implementation path.

---

# 24. Antigravity Subagents

Antigravity supports subagents.

Use:

```text
/agents
```

for agent management.

A larger task can be divided into independent work:

```text
Agent 1 → Analyze backend
Agent 2 → Analyze frontend
Agent 3 → Analyze tests
Agent 4 → Review database
```

This can be useful for large repositories.

Do not parallelize tasks that modify the same files unless the workflow is explicitly designed to avoid conflicts.

---

# 25. Antigravity Permissions

AI agents can potentially:

```text
Read files
Write files
Execute commands
Install dependencies
Modify Git repositories
Run tests
Interact with external systems
```

Therefore, permissions should be treated as a security boundary.

Use:

```text
/config
```

or:

```text
/permissions
```

to inspect and configure permissions.

---

# 26. Dangerous Permission Modes

Avoid unrestricted execution unless you completely understand the consequences.

Never blindly approve commands such as:

```bash
rm -rf
sudo
chmod -R
chown -R
git reset --hard
git push --force
docker system prune
```

An AI agent can misunderstand context just like a human can.

---

# 27. Installing Codex CLI

OpenAI provides multiple installation methods.

## Recommended official installer — Linux/macOS

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Then:

```bash
codex
```


---

# 28. Codex on Windows

PowerShell:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

Then:

```powershell
codex
```


---

# 29. Installing Codex with npm

If Node.js/npm is already installed:

```bash
npm install -g @openai/codex
```

Then:

```bash
codex
```

The official Codex repository currently lists npm as a supported installation method.

To update:

```bash
npm install -g @openai/codex@latest
```

---

# 30. Installing Codex with Homebrew

On macOS:

```bash
brew install --cask codex
```

To update:

```bash
brew update
brew upgrade --cask codex
```


---

# 31. Verify Codex

Run:

```bash
codex
```

For version information:

```bash
codex --version
```

For newer features, always make sure the installed version supports the feature you intend to use.

---

# 32. Codex Authentication

Start:

```bash
codex
```

Codex provides a:

```text
Sign in with ChatGPT
```

authentication option.

Follow the browser authentication flow.

OpenAI currently recommends using ChatGPT authentication when the user wants to use Codex through an eligible ChatGPT plan. API-key authentication is also supported with additional configuration.

---

# 33. Codex API-Key Authentication

API-key authentication is useful for environments where ChatGPT browser authentication is not appropriate, such as certain automated or CI workflows.

Keep the API key secret.

Example environment variable:

```bash
export OPENAI_API_KEY="your-api-key"
```

Never commit it.

Never put it into:

```text
Git repository
README
Source code
Docker image
Public logs
```

For the current authentication details, consult the official Codex authentication documentation.

---

# 34. First Codex Session

Navigate to your repository:

```bash
cd ~/Documents/my-project
```

Run:

```bash
codex
```

Then start with:

```text
Inspect this repository and explain its architecture.

Do not modify any files yet.
```

After receiving the analysis:

```text
Create a detailed implementation plan for improving the authentication system.

Do not implement it yet.
```

Then:

```text
Implement the approved plan.

Run the relevant tests and fix any failures.
```

---

# 35. Codex Prompting Strategy

Avoid vague prompts.

Bad:

```text
Fix my project.
```

Better:

```text
Inspect the FastAPI authentication module.

The login endpoint currently returns HTTP 500 when an invalid
JWT is supplied.

Find the root cause, implement the smallest safe fix,
add a regression test, and run the relevant test suite.
```

---

# 36. Give Codex a Definition of Done

A powerful technique is to specify acceptance criteria.

Example:

```text
Task:
Implement refresh-token rotation.

Requirements:
- Existing login behavior must remain unchanged.
- Refresh tokens must be rotated after use.
- Reuse of an old refresh token must be rejected.
- Add unit tests.
- Add integration tests.
- Do not change the public API response format.
- Run the complete authentication test suite.
```

This gives Codex a measurable finish line.

---

# 37. Codex Goals

Newer Codex versions support Goals.

Example:

```text
/goal Reduce API latency below 150 ms without breaking existing tests.
```

Goals are intended for tasks where the outcome is clear but the implementation path may require investigation, experimentation, debugging, or multiple steps. OpenAI's current cookbook documents Goals starting from Codex 0.128.0.

---

# 38. Codex and Git

Before giving an agent a complex Git task:

```bash
git status
```

Then:

```bash
git branch
```

and:

```bash
git log --oneline -10
```

A safe workflow is:

```text
Clean working tree
      ↓
Create feature branch
      ↓
Agent modifies code
      ↓
Run tests
      ↓
Review diff
      ↓
Commit
      ↓
Push
```

---

# 39. Git Safety

Before allowing an AI agent to modify a repository:

```bash
git status
```

After modifications:

```bash
git diff
```

Then:

```bash
git diff --stat
```

And:

```bash
git status
```

Do not blindly accept a large diff.

---

# 40. Recommended Git Workflow with AI Agents

```bash
git checkout -b feature/my-change
```

Then run your agent.

After the agent finishes:

```bash
git status
git diff
```

Run tests:

```bash
pytest
```

or:

```bash
npm test
```

or your project's appropriate test command.

Then commit:

```bash
git add .
git commit -m "feat: implement my change"
```

---

# 41. Working with Existing Projects

When starting an unfamiliar repository, ask the agent to inspect:

```text
README
package.json
pyproject.toml
requirements.txt
Dockerfile
docker-compose.yml
.env.example
src/
tests/
config/
database/
```

Do not immediately ask it to rewrite the application.

First understand:

```text
Architecture
Dependencies
Entrypoints
Configuration
Database
API
Testing
Deployment
```

---

# 42. Working with Python Projects

A good initial prompt:

```text
Analyze this Python project.

Determine:
- Python version
- Package manager
- Application entry point
- Dependency structure
- Virtual environment expectations
- Testing framework
- Linting/formatting tools
- Configuration system
- Database integration
- API framework

Do not modify files.
```

---

# 43. Working with FastAPI

For your FastAPI projects, a useful agent prompt is:

```text
Analyze this FastAPI project.

Map:
- Application entrypoint
- Routers
- Services
- Schemas
- Models
- Database layer
- Authentication
- Configuration
- Middleware
- Tests

Identify architectural problems but do not modify anything.
```

---

# 44. Working with React

Example:

```text
Analyze this React application.

Identify:
- Entry point
- Routing
- Components
- Pages
- State management
- API layer
- Authentication
- Styling system
- Build system
- Testing setup

Do not modify files.
```

---

# 45. Working with ML Projects

For an ML repository:

```text
Analyze this machine learning repository.

Identify:
- Dataset ingestion
- Data cleaning
- EDA
- Feature engineering
- Feature selection
- Preprocessing
- Train/validation/test splitting
- Model architecture
- Hyperparameter configuration
- Training loop
- Evaluation
- Model serialization
- Inference
- Experiment tracking

Check for data leakage and reproducibility problems.

Do not modify files.
```

---

# 46. Using AI Agents for ML Development

A strong ML workflow is:

```text
Agent
 ↓
Understand dataset
 ↓
Inspect pipeline
 ↓
Identify leakage
 ↓
Review preprocessing
 ↓
Review feature engineering
 ↓
Compare models
 ↓
Run experiments
 ↓
Analyze metrics
 ↓
Perform error analysis
 ↓
Improve pipeline
```

The agent should not simply optimize for the highest validation score.

---

# 47. Example ML Agent Task

```text
Analyze this classification project.

Goals:
1. Identify data leakage.
2. Review train/validation/test splitting.
3. Review preprocessing.
4. Review class imbalance handling.
5. Review feature selection.
6. Review model selection.
7. Review evaluation metrics.
8. Identify possible overfitting.

Do not modify anything.

Return:
- Critical problems
- Medium-risk problems
- Recommendations
- Proposed improvement plan
```

---

# 48. Antigravity vs Codex

Both tools are capable coding agents, but their ecosystems differ.

| Area | Antigravity CLI | Codex CLI |
|---|---|---|
| Organization | Google | OpenAI |
| Command | `agy` | `codex` |
| Primary interface | Terminal TUI | Terminal agent |
| Model ecosystem | Gemini/Google ecosystem | OpenAI/Codex ecosystem |
| Local repository work | Yes | Yes |
| Code editing | Yes | Yes |
| Terminal operations | Yes | Yes |
| Agent workflows | Yes | Yes |
| Subagents | Yes | Yes |
| MCP/skills ecosystem | Yes | Yes |
| ChatGPT authentication | No | Yes |
| Gemini API key | Yes | No |
| OpenAI API key | No | Yes |

Capabilities evolve quickly, so verify feature availability against the current official documentation before building a workflow around a specific feature.

---

# 49. When to Use Antigravity

Antigravity can be particularly attractive when:

```text
You already use Google's AI ecosystem
You work heavily with Gemini
You want Antigravity IDE + CLI
You want terminal-first agent workflows
You want subagent orchestration
You want Google-oriented tooling
```

---

# 50. When to Use Codex

Codex is particularly useful when:

```text
You prefer OpenAI models
You already use ChatGPT
You want Codex integrated into your development workflow
You want terminal-based OpenAI coding agents
You want OpenAI's coding ecosystem
```

---

# 51. Using Both on the Same Machine

You can install both.

Example:

```bash
agy
```

and:

```bash
codex
```

They are separate CLI applications.

You can use them on the same repository, but avoid having both agents simultaneously modify the same files.

---

# 52. Recommended Multi-Agent Workflow

A powerful approach is:

```text
                    Git Repository
                         │
          ┌──────────────┴──────────────┐
          │                             │
      Antigravity                    Codex
          │                             │
      Analysis                     Implementation
          │                             │
          └──────────────┬──────────────┘
                         ↓
                    Tests
                         ↓
                     Review
                         ↓
                      Git
```

Even better:

```text
main
 │
 ├── feature/antigravity-analysis
 │
 └── feature/codex-implementation
```

Do not allow two agents to independently modify the same working tree at the same time.

---

# 53. Worktrees for Multi-Agent Development

Git worktrees are useful when multiple agents need to work simultaneously.

Example:

```bash
git worktree add ../project-agent-a feature/agent-a
git worktree add ../project-agent-b feature/agent-b
```

Now:

```text
project/
project-agent-a/
project-agent-b/
```

Each agent can work independently.

This dramatically reduces accidental file conflicts.

---

# 54. Agent Rules File

For serious projects, create project-level instructions.

Example:

```text
AGENTS.md
```

or an equivalent instruction/configuration mechanism supported by your agent.

A useful rules document should contain:

```text
Project architecture
Coding standards
Testing requirements
Forbidden operations
Build commands
Lint commands
Formatting commands
Database rules
Security rules
Git rules
Deployment rules
```

---

# 55. Example AGENTS.md

```markdown
# Project Instructions

## Architecture

This project uses:

- FastAPI
- PostgreSQL
- SQLAlchemy
- Pydantic
- Pytest

## Rules

- Do not modify database migrations without explicit approval.
- Do not change public API contracts without approval.
- Never commit secrets.
- Never modify `.env`.
- Add tests for bug fixes.
- Run tests before declaring a task complete.

## Code Quality

Use:

- Ruff
- Black
- Pytest
- MyPy where applicable

## Git

Never run:

- git reset --hard
- git push --force
- git clean -fd

without explicit approval.

## Completion Requirements

Before finishing:

1. Run relevant tests.
2. Run linting.
3. Review the diff.
4. Explain changes.
5. Mention remaining risks.
```

---

# 56. Agent Prompt Template

Use this general structure:

```text
## Context

Explain the project and current problem.

## Goal

Describe the desired outcome.

## Constraints

List things the agent must not change.

## Requirements

List functional requirements.

## Acceptance Criteria

Define exactly what success means.

## Verification

Specify tests, commands, and checks.

## Deliverables

Specify what should be changed or produced.
```

---

# 57. Example Professional Prompt

```text
You are working inside an existing FastAPI application.

## Goal

Implement JWT refresh-token rotation.

## Requirements

- Preserve the existing login API.
- Add refresh-token rotation.
- Reject reused refresh tokens.
- Store refresh-token identifiers securely.
- Add unit tests.
- Add integration tests.

## Constraints

- Do not rewrite unrelated modules.
- Do not change existing API response formats.
- Do not modify environment secrets.
- Do not remove existing tests.

## Verification

Run:

pytest

Then inspect:

git diff

## Completion

Do not consider the task complete until:
- implementation is complete,
- tests pass,
- no unrelated files are modified,
- the final diff has been reviewed.
```

---

# 58. Common Mistakes

## Mistake 1 — Starting in the Wrong Directory

Bad:

```bash
cd ~
agy
```

Better:

```bash
cd ~/Documents/project
agy
```

The agent should start inside the intended repository.

---

## Mistake 2 — Giving Too Little Context

Bad:

```text
Fix authentication.
```

Better:

```text
The login endpoint returns HTTP 401 after token refresh.
Reproduce the issue, inspect the authentication flow,
identify the root cause, add a regression test, and fix it.
```

---

## Mistake 3 — Letting the Agent Change Everything

Bad:

```text
Rewrite the entire backend.
```

Better:

```text
Identify the smallest safe architectural change that solves the problem.
Do not rewrite unrelated modules.
```

---

# 59. Mistake 4 — Not Running Tests

Never trust:

```text
"Implementation complete."
```

until you verify it.

Run:

```bash
pytest
```

or the project's appropriate test suite.

---

# 60. Mistake 5 — Not Reviewing Git Diff

Always:

```bash
git diff
```

after an agent makes significant changes.

Look for:

```text
Unexpected files
Deleted code
Secrets
Debug statements
Unrelated refactors
Changed dependencies
Database changes
Configuration changes
```

---

# 61. Mistake 6 — Exposing Secrets

Never allow your agent to accidentally commit:

```text
OPENAI_API_KEY
GEMINI_API_KEY
AWS_SECRET_ACCESS_KEY
DATABASE_PASSWORD
JWT_SECRET
PRIVATE_KEY
```

Use:

```text
.env
.env.local
secret managers
environment variables
```

and ensure secrets are excluded from Git.

---

# 62. Recommended `.gitignore`

Example:

```gitignore
.env
.env.*
!.env.example

.venv/
venv/
__pycache__/

*.pyc

node_modules/

.ipynb_checkpoints/

models/*.pt
models/*.pth
models/*.safetensors

.DS_Store
```

Adapt this to the project.

---

# 63. Troubleshooting Antigravity

## `agy: command not found`

Check:

```bash
which agy
```

If nothing is returned, inspect:

```bash
ls ~/.local/bin/agy
```

If it exists but isn't on PATH:

```bash
echo $PATH
```

Add the directory to your shell PATH if necessary.

---

# 64. Antigravity Authentication Problems

If authentication fails:

1. Restart the CLI.
2. Check your network.
3. Check browser authentication.
4. Verify the configured provider.
5. Check credential/key configuration.
6. For SSH, use the provided authorization URL.
7. If using Gemini API mode, verify:

```text
modelProvider = gemini
```

and:

```text
GEMINI_API_KEY
```


---

# 65. Antigravity Logout

Inside the CLI:

```text
/logout
```

This disconnects the account and clears saved authentication profiles from the OS keyring.

---

# 66. Troubleshooting Codex

## `codex: command not found`

Check:

```bash
which codex
```

If installed through npm:

```bash
npm root -g
```

and:

```bash
npm bin -g
```

depending on your npm version/environment.

You can also reinstall:

```bash
npm install -g @openai/codex@latest
```

---

# 67. Codex Authentication Problems

Start:

```bash
codex
```

and select:

```text
Sign in with ChatGPT
```

If using an API key, verify that the key is correctly configured and available to the process.

Never print the key while troubleshooting.

---

# 68. Update Strategy

Keep the agents reasonably current.

### Antigravity

Use the official installer/update mechanism and verify the current release through Google's official download/docs pages.

### Codex

With npm:

```bash
npm install -g @openai/codex@latest
```

With Homebrew:

```bash
brew update
brew upgrade --cask codex
```

---

# 69. Security Model

Treat an AI coding agent as a developer with powerful terminal access.

The agent may potentially:

```text
Read files
Write files
Run commands
Install packages
Modify configuration
Interact with Git
Access available environment variables
```

Therefore:

```text
Least privilege
+
Workspace isolation
+
Git branches
+
Tests
+
Diff review
+
Secret protection
```

should be standard practice.

---

# 70. Production Repository Rules

For production code:

```text
Never give unrestricted permissions by default.

Always:
- Work on a branch
- Review changes
- Run tests
- Check secrets
- Review dependency changes
- Review database migrations
- Review deployment configuration
```

---

# 71. Recommended Developer Setup

For a Linux development machine:

```text
Ubuntu/Linux
    │
    ├── Git
    ├── Docker
    ├── Python
    ├── Node.js
    │
    ├── Antigravity CLI
    │       └── agy
    │
    └── Codex CLI
            └── codex
```

Recommended terminal:

```bash
cd ~/Documents/project
```

Then choose:

```bash
agy
```

or:

```bash
codex
```

---

# 72. Recommended Workflow for Your Projects

For a complex project such as an ML, FastAPI, React, or automation system:

### Phase 1 — Repository Analysis

```text
Analyze the complete repository.

Do not modify anything.

Create:
- Architecture map
- Dependency map
- Data flow
- Main execution flow
- Potential problems
- Testing strategy
```

### Phase 2 — Planning

```text
Create an implementation plan.

Separate:
- Required changes
- Optional improvements
- Risks
- Testing requirements
```

### Phase 3 — Implementation

```text
Implement only the approved changes.

Do not refactor unrelated code.
```

### Phase 4 — Verification

```text
Run:
- Unit tests
- Integration tests
- Lint
- Type checks
- Build
```

### Phase 5 — Review

```text
Review the complete Git diff.

Identify:
- Bugs
- Security problems
- Unnecessary changes
- Regression risks
```

### Phase 6 — Finalization

```text
Summarize:
- Files changed
- Features added
- Tests executed
- Remaining risks
```

---

# 73. ML-Specific Agent Workflow

For your ML projects, use:

```text
Dataset
   ↓
Data Validation
   ↓
Cleaning
   ↓
EDA
   ↓
Leakage Detection
   ↓
Train/Test Split
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Feature Selection
   ↓
Baseline
   ↓
Candidate Models
   ↓
Cross Validation
   ↓
Hyperparameter Search
   ↓
Error Analysis
   ↓
Final Model
```

Ask the agent to verify every stage instead of jumping directly to model training.

---

# 74. Best Prompt for ML Repository Analysis

```text
You are an ML engineering reviewer.

Analyze this entire repository without modifying files.

Determine:

1. Dataset ingestion
2. Data cleaning
3. Missing-value handling
4. Outlier handling
5. EDA
6. Train/validation/test splitting
7. Data leakage risks
8. Feature engineering
9. Feature selection
10. Feature scaling
11. Class imbalance handling
12. Model selection
13. Hyperparameter tuning
14. Cross-validation
15. Evaluation metrics
16. Error analysis
17. Reproducibility
18. Model serialization
19. Inference pipeline
20. Deployment readiness

For every issue:
- Explain the problem.
- Explain why it matters.
- Give the recommended solution.

Do not modify anything.
```

---

# 75. Best Prompt for Code Review

```text
Review the current implementation as a senior software engineer.

Do not modify files.

Check:

- Correctness
- Security
- Performance
- Maintainability
- Error handling
- Edge cases
- Testing
- Dependency usage
- API compatibility
- Configuration
- Logging

Classify findings as:

CRITICAL
HIGH
MEDIUM
LOW

For every finding provide:
1. Location
2. Problem
3. Why it matters
4. Recommended fix
```

---

# 76. Best Prompt for Autonomous Implementation

```text
Implement the following feature.

Before modifying anything:

1. Inspect the repository.
2. Identify relevant modules.
3. Determine existing conventions.
4. Create an implementation plan.

Then:

5. Implement the feature.
6. Add or update tests.
7. Run the relevant test suite.
8. Fix failures.
9. Run lint/type checks where available.
10. Review the final Git diff.

Constraints:

- Do not modify unrelated files.
- Do not introduce unnecessary dependencies.
- Do not remove existing functionality.
- Do not expose secrets.

At the end provide:
- Summary
- Files changed
- Tests executed
- Remaining risks
```

---

# 77. Antigravity CLI Quick Reference

```bash
# Install
curl -fsSL https://antigravity.google/cli/install.sh | bash

# Start
agy

# Check executable
which agy
```

Inside Antigravity:

```text
/config
/settings
/permissions
/keybindings
/agents
/goal
/grill-me
/schedule
/browser
/plugin
/clear
/undo
/rewind
/fork
/resume
/logout
```

Terminal command:

```text
!command
```

File reference:

```text
@path/to/file
```

---

# 78. Codex CLI Quick Reference

```bash
# Install — official installer
curl -fsSL https://chatgpt.com/codex/install.sh | sh

# Or npm
npm install -g @openai/codex

# Start
codex

# Update
npm install -g @openai/codex@latest

# Check version
codex --version
```

Windows:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

Homebrew:

```bash
brew install --cask codex
```

---

# 79. Final Recommended Workflow

For serious development, use this process:

```text
                    PROJECT
                       │
                       ▼
                 Git Branch
                       │
                       ▼
              Repository Analysis
                       │
                       ▼
                    Planning
                       │
                       ▼
              Agent Implementation
                       │
                       ▼
                 Automated Tests
                       │
                       ▼
                 Static Analysis
                       │
                       ▼
                  Git Diff Review
                       │
                       ▼
                Security Review
                       │
                       ▼
                  Human Review
                       │
                       ▼
                    Commit
                       │
                       ▼
                     Push
                       │
                       ▼
                  CI / CD
                       │
                       ▼
                   Deployment
```

The agent should accelerate the workflow, **not remove engineering discipline**.

---

# 80. Golden Rules

### Rule 1

**Always start the agent inside the correct repository.**

### Rule 2

**Understand before modifying.**

### Rule 3

**Use explicit acceptance criteria.**

### Rule 4

**Keep agents on isolated Git branches/worktrees for significant work.**

### Rule 5

**Never expose secrets.**

### Rule 6

**Never blindly approve destructive commands.**

### Rule 7

**Always run tests after implementation.**

### Rule 8

**Always review the Git diff.**

### Rule 9

**Do not let multiple agents modify the same working tree simultaneously.**

### Rule 10

**The human remains responsible for the final change.**

---

# 81. Official Documentation

## Google Antigravity

Official Antigravity documentation:

[Antigravity CLI documentation](https://antigravity.google/docs/cli-overview?utm_source=chatgpt.com)

Installation and authentication:

[Antigravity CLI installation & authentication](https://www.antigravity.google/docs/cli/install/?utm_source=chatgpt.com)

Using the CLI:

[Using Antigravity CLI](https://antigravity.google/docs/cli/using/?utm_source=chatgpt.com)

Official downloads:

[Google Antigravity downloads](https://www.antigravity.google/download?utm_source=chatgpt.com)

---

## OpenAI Codex

Official Codex documentation:

[OpenAI Codex documentation](https://developers.openai.com/codex?utm_source=chatgpt.com)

Codex CLI source repository:

[OpenAI Codex CLI on GitHub](https://github.com/openai/codex?utm_source=chatgpt.com)

Codex developer resources:

[OpenAI Codex developer resources](https://developers.openai.com/learn/codex?utm_source=chatgpt.com)

---

# 82. Final Summary

The two basic commands to remember are:

```bash
agy
```

for **Google Antigravity CLI**, and:

```bash
codex
```

for **OpenAI Codex CLI**.

The correct mental model is not:

```text
AI → Generate Code
```

but:

```text
Human defines goal
        ↓
Agent understands repository
        ↓
Agent plans
        ↓
Agent implements
        ↓
Agent tests
        ↓
Agent reviews
        ↓
Human verifies
        ↓
Git
        ↓
CI/CD
        ↓
Production
```

Use AI agents as **engineering collaborators**, while keeping Git, testing, security, review, and deployment discipline under your control.
# Getting started — Agentic First Starter Kit

## 1. Copy scaffolding into your repo

Copy these paths into your project root (or merge carefully if files already exist):

- `AGENTS.md`, `CLAUDE.md`, `REDHAT.md`
- `docs/agentic-sdlc.md`, `docs/getting-started.md`, `docs/principles.md`
- `skills/*.md` and `skills/docs-writer/` (tool-agnostic; wire into your assistant as you prefer)
- `.cursor/rules/*.mdc` (optional; Cursor-specific)
## 2. Fill in `AGENTS.md`

Replace every **[EXAMPLE]** block. Add **real** pitfalls agents hit in *your* codebase. Link your build/test commands.

## 3. Optional tooling

Several skills reference external tools. Install them if your workflow uses them; skills gracefully fall back when tools are absent.

| Tool | Purpose | Install |
|------|---------|---------|
| **[EXAMPLE]** [`mcp-atlassian`](https://github.com/sooperset/mcp-atlassian) | Jira MCP server for reading/writing issues from skills | `ghcr.io/sooperset/mcp-atlassian:latest` (container) or see repo README |
| [`gh`](https://cli.github.com/) | GitHub CLI for posting PR comments from skills | `dnf install gh` / `brew install gh` |
| [`glab`](https://gitlab.com/gitlab-org/cli) | GitLab CLI for posting MR comments from skills | `dnf install glab` / `brew install glab` |

Replace the **[EXAMPLE]** MCP server name (`my-jira-server`) and default project key (`ACME`) in skills with your team's values.

## 4. Configure your assistant

- **`skills/`**: Markdown skills any tool can consume—reference them in prompts, symlink into a tool-specific folder, or copy as your workflow requires.
- **Cursor** (optional): Rules in `.cursor/rules/` apply automatically (see `project.mdc`).
- **Claude Code**: Ensure `CLAUDE.md` is present; it points at `AGENTS.md`.

## 5. Write one "agent-ready" task

Pick a small task. Write:

- **Goal**  
- **Acceptance criteria** (testable)  
- **Files to touch**  
- **Constraints**  

## 6. Run a focused session

- One coherent goal per session.  
- Review output like code from a fast junior contributor: correct, consistent, secure.  
- Commit with `Assisted-by:` / `Generated-by:` per `REDHAT.md`.

## 7. Iterate team norms

Capture agreements in `AGENTS.md` or your team's wiki or docs.

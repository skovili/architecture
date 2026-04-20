# Skills — AI Assistant Personas

This directory contains **tool-agnostic persona files** that guide AI coding assistants through specific roles in the development workflow.

## What are skills?

Skills are prompt templates that shape AI assistant behavior for specific tasks. They work with any AI coding assistant (Claude Code, Cursor, GitHub Copilot, etc.) and can be:
- Loaded directly into conversations
- Referenced by file path in prompts
- Symlinked or copied into assistant-specific config directories

## Available skills for this project

| Skill | Purpose | When to use |
|-------|---------|-------------|
| **[engineer.md](engineer.md)** | Software engineer: requirements → code | Implementing features, bug fixes, kustomize templates |
| **[test-writing-qe.md](test-writing-qe.md)** | QE: map acceptance criteria to tests | Creating automation YAML, test scenarios, validation |
| **[adversarial-qe.md](adversarial-qe.md)** | Security-focused QE review | PR review, security analysis, edge cases |
| **[docs-writer/](docs-writer/)** | Technical documentation writer | READMEs, user guides, architecture docs |
| **[performance-agent.md](performance-agent.md)** | Performance testing and benchmarks | Deployment performance, resource validation |
| **[product-engineering.md](product-engineering.md)** | Jira-first engineering discipline | Issue tracking, Definition of Done, agile hygiene |

## How to use skills

### Method 1: Direct reference in prompts

```
Using skills/engineer.md: implement the kustomize template for 
the new storage network isolation in va/hci/ following the 
pattern from va/nfv/sriov/
```

### Method 2: Load into conversation

With Claude Code or Cursor, point the assistant to the skill file:

```
Load skills/engineer.md and help me implement GitHub issue #123.
```

### Method 3: Copy into assistant config

For Cursor:
```bash
cp skills/*.md .cursor/rules/
```

For Claude Code:
- Skills can be loaded via file path in conversation

## OpenStack K8S Architecture-specific usage

### Creating a new VA/DT

```
Using skills/engineer.md: Create a new validated architecture 
for <use case> based on va/hci/. Review AGENTS.md first for 
layering conventions.
```

### Writing tests/automation

```
Using skills/test-writing-qe.md: Create automation YAML stages 
for the new DT following the pattern in automation/dt/uni01alpha/
```

### Reviewing a PR

```
Using skills/adversarial-qe.md: Review PR #456 for:
- Kustomize layering violations
- Hardcoded values that should be parameterized  
- Missing validation in lib/ changes
```

### Updating documentation

```
Using skills/docs-writer/: Update examples/va/nfv/sriov/README.md 
to document the new NUMA pinning configuration
```

### Performance validation

```
Using skills/performance-agent.md: Validate deployment time and 
resource consumption for the HCI VA against our baseline
```

## Customizing skills

These skills are copied from the agentic SDLC starter kit. You can:
- Modify them for project-specific needs
- Add new skills for domain-specific workflows
- Keep them in sync with upstream sdlc-starter or fork entirely

## Attribution

When using skills for AI-assisted development:
- Include `Assisted-by:` or `Generated-by:` in commit messages (see `REDHAT.md`)
- The skill guided the work, but **you own the contribution**
- Review AI output critically—skills are guides, not guarantees

## Learn more

- [AGENTS.md](../AGENTS.md) — Project context and conventions
- [CONTRIBUTING.md](../CONTRIBUTING.md) — Contribution workflow
- [docs/agentic/](../docs/agentic/) — Agentic SDLC principles and playbook

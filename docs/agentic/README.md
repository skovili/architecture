# Agentic-First Development Framework

This directory contains guidance for AI-assisted development on the OpenStack K8S Operators Architecture project.

## Quick Links

- **[principles.md](principles.md)** — Core principles, tenets, and operating model
- **[agentic-sdlc.md](agentic-sdlc.md)** — Practical playbook for teams
- **[getting-started.md](getting-started.md)** — How to adopt this framework

## For Contributors

New to this project and using AI assistants?

1. Read **[../../AGENTS.md](../../AGENTS.md)** — Essential project context
2. Read **[../../REDHAT.md](../../REDHAT.md)** — Mandatory attribution requirements  
3. Skim **[agentic-sdlc.md](agentic-sdlc.md)** — Workflow patterns
4. Check **[../../skills/](../../skills/)** — Personas for specific tasks

## Key Concepts

### Agentic-First Means:

✅ **AI as primary author, human as director** — You set intent, review, and own results  
✅ **Context is infrastructure** — `AGENTS.md`, docs, and conventions reduce rework  
✅ **Human accountability** — You own every commit, AI attribution is mandatory  
✅ **Built-in validation** — Guardrails encoded in workflows, not just inspected after

### What Changes:

- **Issues**: Written as Goal + Acceptance Criteria (agent-friendly)
- **Development**: Agents draft, humans review and approve
- **Testing**: Agents generate test scenarios from AC
- **Documentation**: Agents draft, humans ensure accuracy
- **Attribution**: `Assisted-by:` or `Generated-by:` in all AI-assisted commits

### What Stays the Same:

- **Human review and approval** required for all merges
- **CI/CD gates** apply equally to AI-assisted and human-written code
- **Upstream policy** compliance is mandatory
- **Code quality standards** remain unchanged

## For This Project Specifically

### When working with kustomize templates:

```
Using skills/engineer.md: Create a new storage network 
configuration in va/hci/ following the lib/networking/ 
patterns. Review AGENTS.md for layering rules first.
```

### When writing automation:

```
Using skills/test-writing-qe.md: Create automation YAML 
stages for the new DT with validation commands matching 
existing patterns in automation/
```

### When reviewing PRs:

```
Using skills/adversarial-qe.md: Review PR #123 for:
- Kustomize layering violations  
- Hardcoded values in lib/ or va/ (should be in examples/)
- Missing validation steps
```

## Attribution Requirements (Mandatory)

Per [../../REDHAT.md](../../REDHAT.md), all AI-assisted contributions must include attribution:

```
feat: Add GPU passthrough to HCI VA

Added NVIDIA VFIO passthrough configuration following
the pattern from va/nvidia-vfio-passthrough/

Assisted-by: Claude Code
```

**Failure to attribute AI-assisted work violates Red Hat policy.**

## Resources

- **Upstream**: https://github.com/openstack-k8s-operators/architecture
- **Agentic SDLC**: Based on the sdlc-starter kit
- **Skills**: Tool-agnostic personas in [../../skills/](../../skills/)

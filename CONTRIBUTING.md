# Contributing to OpenStack K8S Operators Architecture

Thank you for your interest in contributing to the OpenStack K8S Operators Architecture project!

## Agentic-first workflow

This project supports **agentic-first development** where AI coding assistants are primary participants in implementation, while humans own intent, architecture decisions, and final review.

### Core principles

1. **Context is infrastructure** — Keep `AGENTS.md`, READMEs, and documentation current
2. **Human accountability** — Every change ships under human judgment and review
3. **Attribution required** — AI-assisted work must be attributed per `REDHAT.md`
4. **Validation always** — Run tests and linting before requesting review

## Before you contribute

### Read the context

1. **[AGENTS.md](AGENTS.md)** — Project architecture, conventions, common pitfalls
2. **[REDHAT.md](REDHAT.md)** — Red Hat AI code assistant policy (mandatory attribution)
3. **[docs/agentic/](docs/agentic/)** — Agentic SDLC principles and playbook
4. **Repository layout** — Understand `lib/` (base) → `va/dt/` (arch-specific) → `examples/` (user-facing)

### Set up your environment

- **Kustomize**: Version 5.0.1+ or OpenShift CLI (oc) 4.14+
- **yamllint**: For YAML validation (`pip install yamllint`)
- **Python**: For automation scripts (`.ci/` directory)
- **mkdocs**: For documentation (`pip install mkdocs`)

## Contribution workflow

### 1. Find or create an issue

- Check existing GitHub issues
- For new features or major changes, create an issue first
- Include **Goal** and **Acceptance Criteria** in issue description

### 2. Create a branch

```bash
git checkout main
git pull upstream main  # Sync with upstream
git checkout -b <descriptive-branch-name>
```

### 3. Make changes

#### For AI-assisted development:

- Point your AI assistant to `AGENTS.md` for context
- Use skills from `skills/` directory for specific tasks:
  - `skills/engineer.md` — Implementation from requirements
  - `skills/test-writing-qe.md` — Test scenarios
  - `skills/adversarial-qe.md` — Security and edge-case review
  - `skills/docs-writer/` — Documentation updates

#### Key guidelines:

- **Never hardcode** environment-specific values in `lib/` or `va/` directories
- **Test broadly** when changing `lib/`—it affects all VAs and DTs
- **Document examples** completely—they're the user's entry point
- **Respect layering**:
  - `lib/` = base templates (reusable across all architectures)
  - `va/` = validated architectures (production-style, complete)
  - `dt/` = deployment topologies (testing only, may be focused)
  - `examples/` = user customization layer

### 4. Validate your changes

**Always run before committing:**

```bash
# Validate kustomize templates
./test-kustomizations.sh

# Lint YAML files
yamllint .

# Test kustomize build for affected VA/DT
kustomize build va/hci/  # example
oc kustomize dt/uni01alpha/  # example
```

### 5. Commit your changes

#### Commit message format:

```
<type>: <short description>

<optional longer description>

<optional issue reference>

Assisted-by: <AI assistant name>
# OR
Generated-by: <AI assistant name>
```

**Types**: `feat`, `fix`, `docs`, `test`, `refactor`, `chore`

**Attribution** (see `REDHAT.md`):
- `Assisted-by:` — You directed work and edited meaningfully (default)
- `Generated-by:` — Substantial generation with minimal human edit

#### Example:

```
feat: Add storage network isolation to HCI VA

Added dedicated storage network configuration to the
Hyperconverged VA following the pattern from NFV SRIOV.

Fixes #123

Assisted-by: Claude Code
```

### 6. Push and create PR

```bash
git push origin <your-branch-name>
```

Create a pull request on GitHub with:
- **Clear title** referencing the issue
- **Description** explaining what changed and why
- **Testing** notes (commands run, validation results)
- **Screenshots** if UI/documentation changes

### 7. Code review

- PRs require approval from `OWNERS` (see [OWNERS](OWNERS) file)
- Address review feedback promptly
- CI must pass (GitHub Actions + Zuul)
- Maintain professional quality—this is an upstream community project

## Types of contributions

### New Validated Architecture (VA)

1. Create structure under `va/<name>/`
2. Follow existing VA patterns (see `va/hci/` or `va/nfv/sriov/`)
3. Add example under `examples/va/<name>/` with complete README
4. Create automation YAML in `automation/va/<name>/`
5. Generate Zuul jobs: `./create-zuul-jobs.py`
6. Update this document and relevant docs

### New Deployment Topology (DT)

1. Create structure under `dt/<name>/`
2. Base on existing DT that's closest to your needs
3. Add example under `examples/dt/<name>/` with README
4. Create automation stages in `automation/dt/<name>/`
5. Mark as "tested" or "untested" in documentation

### Changes to base templates (`lib/`)

⚠️ **High impact** — affects all VAs and DTs

1. Discuss in issue first
2. Test with multiple VAs/DTs before submitting
3. Ensure backward compatibility or document breaking changes
4. Update affected examples

### Documentation improvements

- Keep `AGENTS.md` accurate as architecture evolves
- Update READMEs in `examples/` for user clarity
- Add FAQs in `docs/faq/`
- Improve setup guides in relevant directories

## AI coding assistant guidelines

### Using AI assistants (Claude Code, Cursor, etc.)

✅ **Encouraged for:**
- Generating kustomize templates from requirements
- Creating automation YAML for new VAs/DTs
- Writing comprehensive documentation
- Validating YAML against schemas
- Generating test scenarios

⚠️ **Human review required for:**
- Architecture decisions affecting `lib/`
- Security-sensitive configurations
- Upstream policy compliance
- Review and approval (humans own the merge decision)

### Attribution requirements (MANDATORY)

Per `REDHAT.md`:

1. **Commit messages**: Include `Assisted-by:` or `Generated-by:` trailer
2. **Large generated blocks**: Consider in-file comment at top
3. **Sensitive data**: Never input real credentials, IPs, PII into AI prompts
4. **Third-party matches**: If AI shows code similarity warnings, investigate license implications

### Skills/Personas for workflows

Use tool-agnostic personas from `skills/` directory:

| Workflow stage | Skill file | Purpose |
|----------------|------------|---------|
| Requirements | `skills/product-manager.md` | Define Goal + Acceptance Criteria |
| Implementation | `skills/engineer.md` | Build features from requirements |
| Testing | `skills/test-writing-qe.md` | Create test scenarios from AC |
| Review | `skills/adversarial-qe.md` | Security and edge-case review |
| Documentation | `skills/docs-writer/` | Red Hat-style docs |
| Performance | `skills/performance-agent.md` | Benchmark and validate SLOs |

## Getting help

- **Issues**: Check existing issues or create new ones
- **Discussions**: Use GitHub Discussions for questions
- **Upstream**: https://github.com/openstack-k8s-operators/architecture
- **Documentation**: See `docs/` directory and generated site

## License

Check repository for license information (typically Apache 2.0 for OpenStack projects).

## Code of Conduct

This is an upstream community project. Be respectful, professional, and collaborative.

---

**Remember**: Whether you use AI assistants or not, **you own the contribution**. Review carefully, test thoroughly, and maintain the quality standards of an upstream project.

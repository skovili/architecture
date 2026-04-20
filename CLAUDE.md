# Claude Code — project context

This repository uses **AGENTS.md** as the canonical description of architecture, conventions, and pitfalls.

## Before making changes

1. Read `AGENTS.md` and understand the layered kustomize structure (`lib/` → `va/` or `dt/` → `examples/`).
2. Follow `REDHAT.md` for Red Hat AI policy (attribution, sensitive data, upstream).
3. Prefer small, reviewable steps; ask for constraints (which VA/DT, backward compatibility, OpenStack version).

## Working agreements

- Propose a short plan for non-trivial work (new VA/DT, major lib/ changes); then implement.
- After edits, **always run validation**:
  - `./test-kustomizations.sh` for kustomize validation
  - `yamllint .` for YAML linting
  - Suggest these commands to the user for verification
- For commits: remind the user to add `Assisted-by:` or `Generated-by:` when appropriate per `REDHAT.md`.

## Project-specific commands

- **Validate kustomizations**: `./test-kustomizations.sh`
- **Lint YAML**: `yamllint .` (uses `.yamllint.yml`)
- **Generate Zuul jobs**: `./create-zuul-jobs.py` (for new VAs/DTs)
- **Build kustomize**: `kustomize build <path>` or `oc kustomize <path>`
- **Documentation**: `mkdocs serve` (local preview) or `mkdocs build` (generate static site)

## OpenStack K8S specifics

- **Never hardcode** environment values in `lib/` or `va/`—only in `examples/`
- **Test impact broadly** when changing `lib/`—it affects all VAs and DTs
- **Validate examples** are complete and documented—they're the user's entry point
- **Respect layering**: `lib/` (base) → `va/dt` (architecture-specific) → `examples/` (user customization)

## Upstream awareness

This is an **upstream community project**. All AI-assisted contributions:
- MUST include `Assisted-by:` or `Generated-by:` attribution (see `REDHAT.md`)
- Should maintain professional quality suitable for community review
- Must pass CI gates (GitHub Actions + Zuul)
- Need human approval from `OWNERS` before merge

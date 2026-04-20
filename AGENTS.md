# AGENTS.md — Project context for AI assistants

> **Note**: This file provides context for AI coding assistants working on the OpenStack K8S Operators Architecture repository. Keep it updated as the project evolves.

## Project objective

Build and maintain **validated architectures (VA)** and **deployment topologies (DT)** for OpenStack on Kubernetes using kustomize-compatible templates and custom resources.

- **Success looks like**: Production-ready VAs, well-tested DTs, clear documentation, validated kustomizations, upstream community adoption.
- **Non-goals**: This is not a deployment tool itself—we provide templates that users customize for their environments.

## How we work (agentic first)

- **Human role**: Architecture decisions, upstream policy compliance, review and approval, community engagement.
- **Agent role**: Template generation, YAML validation, automation scripts, documentation updates, test scenarios—always reviewed by a human familiar with OpenStack and Kubernetes.
- **Issues**: Prefer **Goal + Acceptance criteria** format; link to relevant VA/DT paths and constraints.

## Architecture (high level)

- **Base templates**: `lib/` directory contains common components reused across all VAs and DTs
- **VA templates**: `va/*/` directories for production-style validated architectures (HCI, NFV, GPU, etc.)
- **DT templates**: `dt/*/` directories for testing-only deployment topologies
- **User customization**: `examples/va/*` and `examples/dt/*` provide starting points users modify for their environments
- **Automation**: `automation/` defines deployment stages and validation commands
- **CI/CD**: `.ci/` and `.github/workflows/` contain validation and testing pipelines

## Repository layout

| Path | Purpose |
|------|---------|
| `lib/` | Base kustomize templates (control plane, networking, storage, compute, etc.) |
| `va/` | Validated architecture templates (production-style) |
| `dt/` | Deployment topology templates (testing only) |
| `examples/` | User-facing examples that should be customized |
| `automation/` | YAML files defining deployment stages and validation |
| `docs/` | Documentation, FAQs, contributing guides |
| `.ci/` | CI automation scripts (Python) |
| `.github/workflows/` | GitHub Actions workflows |
| `zuul.d/` | Zuul CI/CD configuration |

## Conventions

- **Style / lint**: 
  - YAML must pass `.yamllint.yml` checks
  - Run `test-kustomizations.sh` to validate kustomizations before merge
  - Python scripts should follow project conventions (see `.ci/validate-schema-paths.py`)
- **Commits**: 
  - Use conventional commits when possible
  - Include `Assisted-by:` or `Generated-by:` per `REDHAT.md` when AI assisted
  - Reference GitHub issues in commit messages
- **Kustomize version**: Requires kustomize 5.0.1+ or OpenShift CLI (oc) 4.14+
- **Secrets**: Never commit real credentials, IPs, or hostnames; use placeholders like `changeme` or `192.168.122.x`

## Tech stack details

- **Languages**: YAML (kustomize), Python (automation scripts)
- **Key tools**: kustomize, OpenShift CLI, yamllint, mkdocs
- **OpenStack services**: Nova, Cinder, Glance, Neutron, Ceph, etc.
- **Kubernetes operators**: openstack-k8s-operators family

## Common tasks (copy-paste prompts)

Good starter prompts for contributors:

- "Read `AGENTS.md` and explore the `lib/` structure. Explain how the layered kustomize approach works."
- "Create a new DT based on `dt/uni01alpha/` but with storage network configuration from `dt/uni02beta/`. Put it in `dt/my-new-topology/`."
- "Using `skills/engineer.md`: implement the GitHub issue #123 following the existing kustomize patterns in `lib/`. Run `test-kustomizations.sh` before marking complete."
- "Validate all YAML files in `va/hci/` against the yamllint configuration and fix any violations."
- "Using `skills/docs-writer/`: update the `examples/va/hci/README.md` to reflect the new network isolation parameters."
- "Using `skills/adversarial-qe.md`: review this PR for kustomize layering violations, hardcoded values that should be parameterized, and missing validation steps."
- "Compare `va/nfv/sriov/` with `va/nfv/ovs-dpdk-sriov/` and identify what's missing in the latter (marked untested)."
- "Generate Zuul job configurations for the new VA using `create-zuul-jobs.py` and place them in `zuul.d/`."
- "Using `skills/test-writing-qe.md`: create automation YAML in `automation/` for the new DT with appropriate stage definitions and validation commands."

## Things agents often get wrong here

- **Hardcoding environment-specific values**: Never hardcode IPs, hostnames, passwords in `lib/` or `va/`—only in `examples/` where users are expected to customize.
- **Breaking kustomize layering**: Changes in `lib/` affect ALL VAs and DTs; test broadly. Changes in `va/*` should not depend on `dt/*` or vice versa.
- **Untested validation**: Always run `test-kustomizations.sh` and yamllint before claiming completion.
- **Mixing VA and DT concerns**: VAs are production-style (complete, validated); DTs are testing-only (may be partial or focused). Don't copy DT shortcuts to VAs.
- **Ignoring upstream policy**: This is an **upstream project**—see `REDHAT.md` for AI code assistant attribution requirements before contributing.
- **Not checking examples/**: User-facing examples in `examples/` must be complete, documented, and tested. They are the primary entry point for users.
- **Assuming OpenShift-only**: While this uses OpenShift operators, architecture should be documented in Kubernetes-native terms where possible.

## Review process

- **Approvers**: Listed in `OWNERS` file (abays, cjeanner, fultonj, leifmadsen, raukadah)
- **Reviewers**: Broader set in `OWNERS`—PRs need human review from familiar team members
- **CI gates**: GitHub Actions and Zuul must pass before merge
- **Validation**: Kustomize build must succeed, YAML must lint, automation stages must be testable

## Upstream policy and community

- **Upstream first**: This is an **upstream community project** under openstack-k8s-operators
- **License**: Check repository for license (typically Apache 2.0 for OpenStack projects)
- **AI attribution**: **MANDATORY** per `REDHAT.md`—use `Assisted-by:` or `Generated-by:` in commits for AI-assisted work
- **Community engagement**: PRs visible to upstream community; maintain professional quality and clear explanations

## Key links

- Principles and tenets: [docs/principles.md](docs/principles.md) (to be created)
- Playbook: [docs/agentic-sdlc.md](docs/agentic-sdlc.md) (to be created)
- Policy: [REDHAT.md](REDHAT.md)
- Upstream: https://github.com/openstack-k8s-operators/architecture
- Documentation: Generated via mkdocs (see `mkdocs.yml`)

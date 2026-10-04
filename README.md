# vibecoding-template-infra

> Template for infrastructure, SRE, Ansible, Docker, monitoring, and CMDB projects.

[![Governance](https://img.shields.io/badge/governance-lowcodai-blue)](https://github.com/lowcodai/vibecoding-copilot-governance)

## Description

GitHub template for vibecoding infrastructure projects. Includes everything provided by
`vibecoding-template-base`, plus:
- Ansible structure (`inventory/`, `playbooks/`, `roles/`)
- Docker structure
- Monitoring (dashboards, alerts)
- CMDB
- Dedicated CI/CD workflows: ansible-lint, docker-build, infrastructure-scan

## Agent rulebook

[`AGENTS.md`](AGENTS.md) is the first file every agent (Hermes, Claude Code, Copilot) and every
contributor reads: commands, repository map, the DEV → REVIEW → TEST workflow (ADR-0005),
boundaries and definition of done. Fill in its `TODO` markers when you create a project from
this template. It is rendered by `vibecoding-bootstrap/scripts/apply-template.sh`, the single
source for all templates — change the generator, then re-render, rather than editing one copy.
The orchestration files it refers to (`.ai/`, `.claude/`, `scripts/orchestrate.py`) are
installed by `vibecoding-bootstrap/scripts/sync-governance.sh`.

## Usage

```bash
cd vibecoding-bootstrap
./scripts/new-project.sh --type infra --name <my-infra>
```

## Infra-specific structure

```
.
├── ansible/
│   ├── inventory/   # Inventories (hosts.yml per environment)
│   ├── playbooks/   # Main playbooks
│   └── roles/       # Reusable roles
├── docker/          # Dockerfiles and docker-compose
├── monitoring/
│   ├── dashboards/  # Grafana / other dashboards (JSON)
│   └── alerts/      # Alerting rules (Prometheus/Alertmanager)
└── cmdb/            # Configuration Management Database
```

## Ansible conventions

- Each role follows the `tasks/`, `handlers/`, `defaults/`, `templates/` structure.
- `ansible-lint` is mandatory (see `.github/workflows/ansible-lint.yml`).
- Secrets are managed via Ansible Vault or GitHub Secrets — never in plain text.
- All tasks must be idempotent.

## Infra-specific Awesome Copilot elements

| Element | Type | Usage |
|---------|------|-------|
| `ansible.instructions.md` | Instruction | Ansible conventions |
| `containerization-docker-best-practices.instructions.md` | Instruction | Docker best practices |
| `dependency-license-checker` | Hook | Checks licenses |
| `attester-import-check` | Hook | Checks imports |
| `agent-supply-chain` | Skill | Supply chain analysis |

See `.github/copilot-instructions.md` for this repo's full active hooks list, and the [governance hooks registry](https://github.com/lowcodai/vibecoding-copilot-governance/blob/main/docs/awesome-copilot-map.md) for the full ecosystem-wide catalog.

## References

- [vibecoding-copilot-governance](https://github.com/lowcodai/vibecoding-copilot-governance)

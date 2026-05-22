# homelab-core

`homelab-core` is the operations repository for the shared homelab platform.
It documents the core routing, observability, backup, restore, and incident
response practices that keep the environment supportable.

This repository is intentionally conservative: it contains sanitized
documentation and example configuration only. Private hostnames, IP addresses,
credentials, tokens, alert destinations, and customer or household-specific
service details must not be committed here.

## Current State

This repo is being upgraded from a shell repository into a credible platform
operations repository. Several service names and topology details are still
unknown from the public repo history, so those areas are marked as `TODO` or
`PLACEHOLDER` instead of being invented.

## Repository Map

| Path | Purpose |
| --- | --- |
| `docs/architecture.md` | Platform architecture, trust boundaries, and operational assumptions. |
| `docs/service-inventory.md` | Service ownership and dependency inventory template. |
| `docs/operations/` | Logging, alerting, backup, and restore operating model. |
| `docs/runbooks/` | Incident and maintenance runbooks for repeatable operations. |
| `docs/diagrams/` | Mermaid diagrams for platform, observability, and restore flows. |
| `monitoring/` | Sanitized Prometheus, Alertmanager, and Grafana examples. |
| `scripts/validate` | Local validation entrypoint used by CI. |
| `.github/workflows/validate.yml` | Markdown, YAML, shell, JSON, and Mermaid shape checks. |

## Operating Principles

- Keep production secrets out of Git. Use a secrets manager, environment
  injection, or encrypted deployment channel.
- Prefer reproducible configuration over manual console changes.
- Treat monitoring and backup restore tests as part of the service lifecycle.
- Record unknowns as `TODO(owner/date/context)` or `PLACEHOLDER` until verified.
- Document the failure mode and the rollback path before adding automation.

## Quick Start

Run local validation before opening a pull request:

```bash
scripts/validate
```

The script runs stronger checks when optional tools are installed:

- `markdownlint-cli2` for Markdown formatting
- `yamllint` for YAML syntax and style
- `shellcheck` for shell script safety
- `python3` or `python` for JSON syntax checks

CI installs those tools and runs the same script with `VALIDATE_STRICT=1`.

## Documentation Workflow

1. Add or update the service in `docs/service-inventory.md`.
2. Update any affected architecture notes in `docs/architecture.md`.
3. Add or revise the appropriate runbook in `docs/runbooks/`.
4. Add sanitized monitoring examples under `monitoring/` if the service exposes
   useful metrics or alert conditions.
5. Run `scripts/validate`.

## Safety Notes

- Example config files are intentionally non-routable or local-only by default.
- Alert receivers in this repo are placeholders and must be replaced by private
  configuration during deployment.
- Backup and restore docs describe the expected operating model. Real schedules,
  retention periods, storage providers, and restore targets must be verified
  before being treated as production policy.

## License

Apache License 2.0. See `LICENSE`.

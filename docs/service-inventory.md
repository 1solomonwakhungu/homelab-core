# Service Inventory

This inventory is a sanitized operating record. It should describe enough for a
maintainer to understand ownership, dependencies, and runbooks without exposing
private network details.

Use `PLACEHOLDER` where the public repo cannot safely contain a value. Replace
entries only after verifying the real environment.

## Core Services

| Service | Role | Runtime | Dependencies | Data criticality | Runbook | Status |
| --- | --- | --- | --- | --- | --- | --- |
| Edge routing | Routes LAN and ingress traffic. | `TODO` | DNS, network uplink | High | `docs/runbooks/network-incident.md` | `TODO`: verify implementation. |
| Metrics collection | Scrapes and stores platform metrics. | Prometheus example included | Exporters, service endpoints | Medium | `docs/runbooks/observability-no-data.md` | Example only. |
| Alert routing | Groups and sends operational alerts. | Alertmanager example included | Prometheus, private receivers | Medium | `docs/runbooks/alert-triage.md` | Example only. |
| Dashboards | Presents operational views. | Grafana provisioning examples included | Prometheus datasource | Low | `docs/runbooks/observability-no-data.md` | Example only. |
| Backup coordination | Runs backup and restore workflows. | `TODO` | Backup storage, credentials | High | `docs/runbooks/restore-from-backup.md` | `TODO`: verify tool. |

## Workload Template

Copy this row for each real service after verification.

| Service | Owner | Runtime | Internal endpoint | Public endpoint | Backup scope | Monitoring | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `PLACEHOLDER-service-name` | `TODO` | `TODO` | `PLACEHOLDER.internal.example` | `PLACEHOLDER.example.com` | `TODO` | `TODO` | Replace with verified details. |

## Required Metadata

Each production service should eventually document:

- owner or maintainer
- deployment location
- dependency list
- ingress path
- persistent data paths
- backup scope
- restore priority
- dashboard link
- alert rules
- runbook link
- known maintenance windows

## Criticality Guide

| Level | Meaning | Expected response |
| --- | --- | --- |
| High | Outage blocks network access, identity, backups, or critical data. | Triage immediately; restore before routine changes. |
| Medium | Outage reduces visibility or affects important but recoverable services. | Triage during the next active operations window. |
| Low | Convenience service, dashboard, or non-critical automation. | Fix opportunistically after higher-priority issues. |

## Open Questions

- `TODO`: identify the actual edge routing component and config source.
- `TODO`: identify the logging backend and retention policy.
- `TODO`: identify backup tool, repository location, encryption model, and test cadence.
- `TODO`: list actual homelab workloads and service owners.

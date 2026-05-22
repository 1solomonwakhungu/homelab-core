# Backup and Restore

## Goal

Backups are only useful when restore steps are documented and tested. This
document defines the expected backup and restore operating model for
`homelab-core`.

The repository does not currently include the real backup tool, schedule,
storage target, encryption model, or retention policy. Those details are marked
as `TODO` until verified.

## Backup Policy Template

| Item | Value |
| --- | --- |
| Backup tool | `TODO`: verify. |
| Backup schedule | `TODO`: verify. |
| Retention | `TODO`: verify. |
| Storage target | `PLACEHOLDER`: private backup repository. |
| Encryption | `TODO`: verify key management and recovery process. |
| Restore test cadence | `TODO`: define, recommended at least quarterly for critical data. |
| Success signal | `TODO`: metrics, logs, or alert clear condition. |

## Backup Scope

Back up data that cannot be recreated from Git or package repositories:

- service databases
- object or media storage
- application uploads
- private runtime configuration
- certificates and keys, if policy allows and encryption is verified
- monitoring state only when it is operationally valuable

Do not back up:

- generated caches
- container images that can be pulled again
- local build artifacts
- unencrypted secrets in public storage

## Restore Priority

| Priority | Service type | Restore objective |
| --- | --- | --- |
| P0 | Network access, DNS, identity, backup metadata. | Restore first; blocks other work. |
| P1 | Data-bearing applications. | Restore after platform access is stable. |
| P2 | Observability and dashboards. | Restore when core workloads are stable. |
| P3 | Convenience or experimental services. | Restore last or rebuild. |

## Restore Test Checklist

1. Select a non-production restore target.
2. Confirm the backup snapshot or archive identifier.
3. Confirm credentials are available through the private secret path.
4. Restore data into the isolated target.
5. Start the service against restored data.
6. Run service health checks.
7. Record the result, duration, and any missing steps.
8. Update `docs/runbooks/restore-from-backup.md` if the runbook drifted.

## Failure Modes

| Failure | Detection | Response |
| --- | --- | --- |
| Backup job did not run | Missing success metric or stale backup alert. | Triage scheduler, credentials, and destination reachability. |
| Backup destination full | Storage alert or failed backup log. | Free capacity or rotate retention after confirming policy. |
| Credentials expired | Authentication failure in backup logs. | Rotate through private secret workflow. |
| Restore fails | Restore test or incident restore error. | Preserve logs, identify missing dependency, update runbook. |

## Open Questions

- `TODO`: what backup tool is in use?
- `TODO`: where are backup repositories stored?
- `TODO`: how are restore credentials recovered during a platform outage?
- `TODO`: which services have tested restores?

# Runbook: Restore From Backup

## Purpose

Provide a public-safe restore flow that can be filled in with private commands
once the actual backup tool and storage target are verified.

## Preconditions

- Restore target is isolated from production.
- Backup snapshot or archive identifier is known.
- Restore credentials are available through the private secret path.
- Service owner has approved the restore.

## Steps

1. Identify the affected service in `docs/service-inventory.md`.
2. Confirm restore priority using `docs/operations/backup-restore.md`.
3. Stop writes to the affected production service if data consistency requires
   it.
4. Restore into a non-production target first.
5. Run the service health check against restored data.
6. Compare restored data freshness with the expected recovery point.
7. Promote the restored data only after validation.
8. Record restore duration, snapshot ID, and validation result in the incident
   notes.

## Placeholder Commands

The real restore commands are intentionally not present.

```bash
# PLACEHOLDER: replace with verified private restore command.
backup-tool restore --snapshot SNAPSHOT_ID --target /restore/path
```

## Rollback

If restore validation fails:

- keep the failed restore target intact for investigation
- do not overwrite the previous production state
- collect restore logs
- escalate to the service owner

## Unknowns

- `TODO`: backup tool name.
- `TODO`: snapshot naming convention.
- `TODO`: restore target path.
- `TODO`: data integrity checks per service.

# Runbook: Observability Has No Data

## Purpose

Diagnose missing metrics, logs, or dashboards without exposing private endpoint
details.

## Symptoms

- Grafana panels show no data
- Prometheus targets are down
- alerts stop firing unexpectedly
- logs are missing for an active service

## Metrics Checks

1. Confirm Prometheus is running.
2. Check target health in the Prometheus targets page.
3. Check whether the service exposes metrics on the expected path.
4. Check network reachability between Prometheus and the target.
5. Check recent scrape config changes.
6. Validate the example config if it was changed:

   ```bash
   scripts/validate
   ```

## Dashboard Checks

1. Confirm the Grafana datasource is provisioned.
2. Confirm the datasource URL points to the private Prometheus endpoint.
3. Confirm dashboard variables match current service labels.
4. Check whether panels use labels that no longer exist.

## Logging Checks

The logging backend is not yet identified in the public repo.

`TODO`: add backend-specific checks after logging architecture is verified.

## Resolution

- Restore scrape target health.
- Revert invalid dashboard or alert rule changes.
- Update service labels or dashboards if a rename caused the gap.
- Add missing validation when a config issue was not caught locally.

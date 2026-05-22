# Runbook: Service Onboarding

## Purpose

Add a new homelab service to operations coverage before it becomes a dependency.

## Steps

1. Add the service to `docs/service-inventory.md`.
2. Document owner, runtime, endpoints, dependencies, and data criticality.
3. Identify whether the service stores persistent data.
4. Add backup scope and restore priority if data is persistent.
5. Add Prometheus scrape config or document why metrics are unavailable.
6. Add alert rules only for actionable failure modes.
7. Add or update Grafana dashboard provisioning if a dashboard is useful.
8. Add a runbook for the most likely failure mode.
9. Run validation:

   ```bash
   scripts/validate
   ```

## Acceptance Criteria

- service inventory entry exists
- monitoring decision is recorded
- backup decision is recorded
- owner or maintainer is listed
- runbook coverage exists for critical services
- no secrets or private endpoints are committed

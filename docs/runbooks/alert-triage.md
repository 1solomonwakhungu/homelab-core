# Runbook: Alert Triage

## Purpose

Classify and respond to an alert without assuming private environment details.

## Inputs

- alert name
- severity
- service label
- affected target
- dashboard link, if available
- current maintenance window status

## Steps

1. Confirm whether the alert is still firing.
2. Check whether the alert overlaps with planned maintenance.
3. Identify the service owner from `docs/service-inventory.md`.
4. Open the related dashboard or metrics query.
5. Check recent deployment, configuration, or infrastructure changes.
6. Follow the service-specific runbook if one exists.
7. If no service-specific runbook exists, record the missing runbook as a
   follow-up.

## Escalation

Escalate when:

- severity is critical
- data loss is possible
- routing, DNS, identity, or backup access is affected
- the alert has no known owner and user impact is visible

`TODO`: replace this section with the real private escalation path.

## Resolution

Before closing the incident:

- confirm the alert cleared
- confirm user-facing service health
- capture the root cause or best known cause
- add or update runbook steps
- remove alert noise if the alert was not actionable

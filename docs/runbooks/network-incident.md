# Runbook: Network Incident

## Purpose

Restore core network access when routing, DNS, or ingress appears degraded.

Actual device names, IP addresses, and provider details are intentionally not
documented in this public repo.

## Symptoms

- services unreachable from LAN
- public ingress unavailable
- DNS resolution failure
- monitoring target loss across many services
- router or proxy health alert

## Steps

1. Confirm whether the issue is local device-specific or platform-wide.
2. Check upstream internet availability from a trusted private host.
3. Check DNS resolution for an internal and external name.
4. Check the edge routing or reverse proxy service health.
5. Check whether a recent config change was deployed.
6. Roll back the most recent edge config change if it correlates with impact.
7. If the edge device is unreachable, use the private out-of-band access path.

## Validation

Confirm recovery with:

- one LAN-only service
- one public ingress route, if configured
- one DNS lookup
- Prometheus target health, if Prometheus is available

## Follow-Up

- Record the affected services and timeline.
- Add the exact private commands to the internal runbook if they are safe there.
- Add a public-safe summary here if the generic process changes.

## Unknowns

- `TODO`: edge routing product or service.
- `TODO`: DNS provider and local resolver topology.
- `TODO`: rollback mechanism.

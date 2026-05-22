# Logging and Alerting

## Goal

Provide enough visibility to detect outages, diagnose common failures, and
restore service without relying on memory.

This document describes the desired operating model. Concrete endpoints and
receivers are placeholders until the private environment is verified.

## Metrics

Prometheus-compatible examples live under `monitoring/prometheus/`.

Minimum expected scrape coverage:

- Prometheus self-metrics
- host or node exporter metrics
- edge routing health
- key workload health endpoints
- backup job result metrics, if available

Unknowns:

- `TODO`: actual scrape targets
- `TODO`: TLS and authentication requirements
- `TODO`: retention period
- `TODO`: remote write or long-term storage strategy

## Logs

The public repo does not currently identify the logging backend. Candidate
patterns include systemd journal collection, Loki, OpenSearch, or a hosted log
provider.

Minimum expected log coverage:

- edge routing and reverse proxy access logs
- authentication or identity service events, if present
- platform service errors
- backup job output
- alert delivery failures

Unknowns:

- `TODO`: logging backend
- `TODO`: log retention period
- `TODO`: privacy filtering rules
- `TODO`: dashboard or search links

## Alert Severity

| Severity | Meaning | Example condition |
| --- | --- | --- |
| Critical | Immediate action required to restore core access or protect data. | Core service down, backup repository unavailable, routing failure. |
| Warning | Action needed soon, but service is not fully down. | Disk filling, scrape target missing, backup stale. |
| Info | Awareness only. | Planned maintenance notice or low-priority drift. |

## Alert Routing

The example Alertmanager config uses placeholder receivers only. Real receiver
URLs, tokens, phone numbers, email addresses, and escalation channels must be
provided through private deployment config.

Expected routing behavior:

- group alerts by service and alert name
- send critical alerts to the primary on-call receiver
- send warning alerts to an async operations channel
- inhibit warning alerts when a related critical alert is firing

## Alert Review Cadence

- Review noisy alerts after each incident.
- Remove alerts that are not actionable.
- Add runbook links to alert annotations.
- Confirm each critical alert has an owner and restore path.

## Incident Artifacts

After a significant incident, record:

- start and end time
- affected services
- user impact
- root cause or best known cause
- remediation
- prevention follow-up
- updated runbook links

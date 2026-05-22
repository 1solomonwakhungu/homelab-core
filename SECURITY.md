# Security Policy

## Reporting

Do not open a public issue with secrets, private hostnames, IP addresses,
webhook URLs, credentials, or exploitable details.

Use GitHub private vulnerability reporting if it is enabled for this repository.
If it is not enabled, contact the repository owner through a private channel and
include only the minimum detail needed to coordinate disclosure.

## Secret Handling

Never commit:

- API tokens
- passwords
- private keys
- VPN credentials
- real alert webhook URLs
- real backup repository credentials
- personal IP addresses or hostnames

If a secret is committed:

1. Revoke or rotate it immediately.
2. Remove it from the active branch.
3. Treat the exposed value as compromised even if history is rewritten later.
4. Add a validation rule if the leak pattern can be detected safely.

## Supported Content

This repository supports public-safe operations documentation and sanitized
example configuration. Private deployment values belong in private secret
management or private environment-specific repositories.

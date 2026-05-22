# Contributing

## Scope

Contributions should improve public-safe homelab operations documentation,
sanitized examples, validation, or runbooks.

Do not add private runtime details unless they are already intended for public
release.

## Workflow

1. Create a branch from `main`.
2. Make focused changes.
3. Label unknown operational details as `TODO` or `PLACEHOLDER`.
4. Run validation:

   ```bash
   scripts/validate
   ```

5. Open a pull request with a summary, validation results, and any remaining
   operational unknowns.

## Documentation Standards

- Prefer verified facts over guesses.
- Use `.example` domains, loopback addresses, or documentation IP ranges in
  examples.
- Link alerts to runbooks when possible.
- Keep runbooks action-oriented.
- Avoid secrets and personal identifiers.

## Pull Request Checklist

- [ ] No secrets or private endpoints are included.
- [ ] New services are listed in `docs/service-inventory.md`.
- [ ] Operational changes include runbook updates.
- [ ] Monitoring examples are sanitized.
- [ ] `scripts/validate` passes locally or the blocker is documented.

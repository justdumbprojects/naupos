# Development workflow

Use `main` as the stable source baseline. Create a branch for each feature or fix; test with isolated dummy data and submit a pull request.

Suggested branch names:
- `fix/inventory-atomic-writes`
- `fix/payment-idempotency`
- `feature/owner-app`
- `chore/source-organization`

## Pre-merge checks

- Server source parses with Python.
- POS loads and authenticates as intended.
- Owner and Staff authorization is checked on the server.
- A dummy sale closes exactly once and deducts correct inventory.
- Crash/restart recovery is verified for affected data paths.
- No secrets or runtime databases are present in the diff.

GitHub stores source history; it does not replace live database backups.

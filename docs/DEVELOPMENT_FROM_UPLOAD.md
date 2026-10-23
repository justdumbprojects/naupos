# Náu development workflow

1. Clone the existing `justdumbprojects/naupos` repository with GitHub Desktop.
2. Keep a separate backup of the working bar deployment and its data.
3. Create a branch from `main` for each change.
4. Replace or update only the affected source files in `pos/` and `server/`.
5. Check **Changes** in GitHub Desktop. Verify that no private data or credentials appear.
6. Commit with a descriptive message, push the branch, open a pull request, and merge after testing.
7. Do not treat GitHub as a replacement for database backups.

## Suggested branch names
- `fix/inventory-atomic-writes`
- `fix/payment-idempotency`
- `feature/owner-app`
- `chore/security-audit`

## Smoke tests before merging
- Server starts with the intended Python interpreter.
- Owner and Staff permissions behave correctly.
- Create, modify and close a test order; confirm inventory and sales records.
- Test receipt printing, restart recovery, and backup behavior.
- Never run destructive tests against live bar data.

## Applying the prepared ZIP

This ZIP is a **clean source snapshot**, not a ready-to-push replacement for the repository's history. Extract it into a cloned repository, keeping the repository's `.git/` directory and `LICENSE`. Inspect changes, then commit. Do not use `git init` to replace the existing history.

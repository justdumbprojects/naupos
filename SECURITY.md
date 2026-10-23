# Credential and data handling

## Confirmed in supplied source archive
The source archive contained `google_finance_client.json` with a populated OAuth desktop client ID and client secret. It was excluded from the prepared GitHub package. The application loads this credential from a local file; do not remove that file from the deployed bar machine without arranging a replacement.

## Required follow-up
- If that credential was already pushed to the **public** repository, treat it as exposed. Rotate/recreate the Google OAuth client credential as appropriate in Google Cloud Console, update the local runtime configuration, and remove the old secret from Git history. Merely deleting the file in a new commit does not remove it from earlier commits.
- Review the repository's existing commits for previously exposed credentials; this package cannot sanitize existing Git history.
- Keep OAuth tokens, Cloudflare tunnel credentials, private keys, customer records and sales data out of Git.
- Enable GitHub secret scanning/push protection if available for the repository.
- Do not paste credential values into Issues, PRs, logs or chat.

## Scope
A static pattern-based scan found no obvious literal GitHub token, Google API key, or PEM private key in the first-party source files. This is not a proof that all secrets are absent. Dynamic values, obfuscation, and historical commits require separate review.

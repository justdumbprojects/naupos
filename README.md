# Náu POS

A locally hosted point-of-sale system developed for a cocktail bar. The Python backend manages application logic and HTTP APIs, while the HTML/CSS/JavaScript frontend provides the POS interface.

> **Development repository.** Not a turnkey production deployment. Never commit live sales, customer data, OAuth credentials, tunnel tokens, or database backups.

## Structure

| Path | Contents |
|---|---|
| `server/server.py` | Python backend (current monolithic source) |
| `pos/` | POS frontend pages (HTML/CSS/JavaScript) |
| `server/google_finance_client.example.json` | Placeholder-only configuration schema |
| `docs/` | Development workflow and security guidance |
| `.github/workflows/` | Static CI checks |

## Development

- The backend is developed for **Python 3.14 free-threaded (3.14t)** on Windows.
- The POS communicates with the backend over HTTP, normally on localhost port 8000.
- Additional integrations may require local configuration and dependencies.
- Keep `server/google_finance_client.json` **local and untracked** if using Google Finance. The example file is **not** a credential.
- Refer to `docs/DEVELOPMENT.md` for Git workflow.

## Git workflow

`main` is the last tested source baseline. Make changes in short-lived branches such as `fix/receipt-printing` or `feature/reservations`. Commit small, reviewable changes; test them; then merge by pull request.

## Security

Do not commit runtime data or credentials. If a secret was ever pushed, deleting it from the latest commit is **not sufficient**: revoke/rotate the secret and consider Git history cleanup. See `docs/SECURITY.md`.

## License

The existing public repository has a GPL-3.0 license. Preserve its root `LICENSE` file when applying this package. Third-party extension files are not included in this public source package.

## Public POS edition

The public source removes the remote Founder API, Cloudflare Tunnel autostart and FFmpeg live-camera streaming. Google Sheets/Drive integrations remain optional and use local OAuth credentials.

See [what you need](https://github.com/justdumbprojects/naupos/blob/main/what%20you%20need.md) and [how to setup](https://github.com/justdumbprojects/naupos/blob/main/how%20to%20setup.md).

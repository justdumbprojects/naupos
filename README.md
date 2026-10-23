# Náu POS

Open-source point-of-sale software developed for **Náu**, a cocktail bar in Hanoi.

Náu POS uses a Python backend and an HTML/CSS/JavaScript frontend. The project includes ordering, inventory and recipes, sales, customer records, reservations, finance reporting, and related integrations.

> **Status:** Active development. This repository is not a production-ready deployment guide or a guarantee of security.

## Repository layout

- `server/` — Python backend source
- `pos/` — POS web frontend
- `docs/` — contributor, security, and development notes
- `.github/workflows/` — automated checks

## Getting started

- [What you need](what%20you%20need.md) — Python, Google libraries, FFmpeg, cloudflared and other dependencies.
- [How to set up](how%20to%20setup.md) — Google Drive/Sheets OAuth, backups, POS logos, camera and tunnel configuration.

**Note:** The full sanitized backend/frontend source is being prepared for publication; the repository is not yet a complete runnable distribution.

## Contributing

Please open an Issue before substantial changes. Submit bug fixes and features on separate branches using pull requests. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Security and privacy

**Never commit** customer data, sales records, API keys, OAuth client secrets, tokens, Cloudflare credentials, or live database backups. See [SECURITY.md](SECURITY.md) for responsible disclosure.

## License

GNU General Public License v3.0; see [LICENSE](LICENSE). Bundled third-party components, if any, retain their respective licenses.

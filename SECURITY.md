# Security Policy

Náu POS is under active development. It has not undergone a complete independent penetration test.

## Reporting vulnerabilities

Please do **not** publish exploitable vulnerabilities, secrets, or private data in a public GitHub Issue. Contact the repository maintainer privately through their GitHub profile, or use GitHub's private vulnerability reporting feature if enabled.

## Secret handling

Never commit:
- Google OAuth client credentials or access/refresh tokens
- API keys, Cloudflare tunnel credentials, private keys
- Live customer, reservation, inventory, or sales databases
- Database backups, session material, or logs containing sensitive data

Use local configuration files excluded by `.gitignore`. If a credential was previously committed, **rotate/revoke it** and remove it from Git history; a later deletion commit does not erase the earlier copy.

## Security expectations

The backend must independently validate permissions, input, and one-time action tokens. Frontend hiding of UI elements is not an authorization boundary.

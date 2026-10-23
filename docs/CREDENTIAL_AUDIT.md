# Náu POS credential audit — 2026-10-23

## Scope
Scanned the supplied `payload(2).zip` first-party `server.py`, all HTML pages, and JSON configuration. Bundled third-party `extensions/blockify` contains large external filter lists and was not certified or included in this smaller source package.

## Confirmed
- `payload/google_finance_client.json` includes a real OAuth client ID and client secret. **Excluded from package.** Do not publish it.
- Cloudflare tunnel token was **not hardcoded** in the original `server.py`. The remote Founder API, Cloudflare Tunnel manager, and camera/FFmpeg gateway have now been removed from this public POS source.
- `POSsettings.json` may hold encrypted tunnel credentials and other local settings. Added ignore patterns.
- No recognizable literal Google API keys (`AIza...`), GitHub tokens (`ghp_...` etc.), Cloudflare JWT tunnel tokens (`eyJ...`), or PEM private keys were found in first-party Python/HTML source using pattern scans.
- Public hostname `api.nauapp.dpdns.org` is an endpoint, **not** a secret.

## Limitations
- Pattern scans do not prove absence of unknown or obfuscated credentials.
- Existing Git history must be scanned independently; `.gitignore` does not remove previously committed secrets.
- Existing local Cloudflare tunnel tokens cannot be revoked or rotated by editing code. Rotate them in Cloudflare Zero Trust if compromised.
- OAuth credential may be necessary at runtime: store it locally outside Git, following server's credential lookup.
- The included Python source passed `ast.parse` syntax checking. No live integration tests were run.

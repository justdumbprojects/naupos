# Náu POS

**A bar-first, locally hosted point-of-sale and operations system — built for the way cocktail bars actually work.**

Náu POS began as an in-house system for **Náu**, a small cocktail bar in Hanoi. Instead of treating a bar like a generic retail counter, it brings drink preparation, ingredient-level inventory, recipes, staff workflows, guests, reservations, and financial reporting into one interface.

> **Project status:** Actively developed open-source software. This is a source repository, not a verified one-click production installer. Test with dummy data before using it in a live venue.

## Why bar-first?

In a cocktail bar, a sale is more than a product and a price. One drink can consume several spirits, syrups, garnishes, and house-made preparations. Staff also need to handle remakes, waste, special requests, and repeat guests without losing track of stock or the order.

Náu POS is designed around those realities.

## Features

| Area | What Náu POS supports |
|---|---|
| **Orders and checkout** | Drink ordering, order notes, cash and bank-transfer payments, receipts and reprints |
| **Cocktail recipes** | Ingredient-based recipes and quantities, including preparation recipes and house-made components |
| **Ingredient inventory** | Stock tracking, restocking, stocktakes, ingredient usage, availability checks and 86/out-of-stock handling |
| **Bar-specific operations** | Bespoke drinks, classic specials, remakes, waste recording, and internal Bartender/Owner consumption tables |
| **Sales history** | Searchable transactions, receipt reprints and sales review |
| **Guest profiles** | Customer records, purchase history and booking history |
| **Reservations** | Guest-linked reservations and booking status management |
| **Promotions** | Promotion management alongside the ordering workflow |
| **Finance** | Revenue, cost and profit reporting, with optional Google Sheets integration |
| **Backups** | Local data management and optional Google Drive backup integration |
| **Access control** | Owner and Staff roles with server-side authorization checks |

Features reflect the current project source and ongoing development; individual workflows may require configuration or further testing.

## Design philosophy

- **Built for bartenders:** Keep the order-taking workflow connected to the actual ingredients consumed behind the bar.
- **Recipes are operational data:** A cocktail's ingredient list helps determine what can be made and what stock is used.
- **Flexible service:** Accommodate bespoke requests, house specials, remakes, waste and internal pours.
- **Know your regulars:** Keep customer and reservation history connected to service.
- **Local-first:** Run the POS locally rather than requiring a cloud-hosted checkout service for routine use.

## Screens and source layout

| Path | Purpose |
|---|---|
| `pos/index.html` | Main POS interface |
| `pos/recipes.html`, `pos/prep.html` | Recipes and preparation |
| `pos/ingredients.html`, `pos/stock.html` | Ingredients and inventory |
| `pos/sales.html`, `pos/finance.html` | Sales and financial views |
| `pos/customers.html`, `pos/promo.html` | Guests and promotions |
| `pos/settings.html` | Application settings |
| `server/server.py` | Python backend and HTTP API |
| `server/google_finance_client.example.json` | Example Google OAuth client configuration; **not a real credential** |
| `docs/` | Development and security documentation |

## Windows — download the ready-to-run app

**Using Windows and don't want to build from source?** Head to the [GitHub Releases page](https://github.com/justdumbprojects/naupos/releases) to download a pre-packaged Náu POS executable **when a Windows release is available**.

1. Open the latest release.
2. Under **Assets**, download the Windows `.exe` (or installer, if provided).
3. Follow the release notes for installation, first-run setup, and any prerequisites.

The packaged version is intended for Windows users who prefer not to install Python or build the app themselves. **If the Releases page has no downloadable Windows build yet, use the source setup instructions below.**

## Getting started

This project is primarily developed on **Windows with Python 3.14 / 3.14t**. The frontend is HTML/CSS/JavaScript, served by a local Python backend.

1. Read [What you need](what%20you%20need.md) for prerequisites and optional dependencies.
2. Follow [How to set up](how%20to%20setup.md) for Google Sheets/Drive authorization, local configuration and replacing the POS logos.
3. Use a separate test data directory before trying real orders or inventory.

**Public edition:** The remote Founder App API, Cloudflare Tunnel manager and live-camera gateway have been removed. **FFmpeg and cloudflared are not required.** Google Sheets and Drive integrations remain optional.

## Contributing

Contributions, bug reports and bar-focused feature ideas are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and [the development guide](docs/DEVELOPMENT.md). Keep changes focused, avoid real customer data in tests and describe how you verified operational workflows.

## Security

Do **not** commit OAuth client files, API keys, access tokens, customer records, sales databases or backups. See [SECURITY.md](SECURITY.md). If a credential was exposed in Git history, deleting it in a later commit does not revoke it.

## License

Licensed under the **GNU General Public License v3.0**. See [LICENSE](LICENSE).

---

*Made for a cocktail bar. Open for other bars to build on.*

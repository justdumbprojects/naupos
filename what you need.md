# What you need to run Náu POS

Náu POS is designed primarily for **64-bit Windows 10/11**. You can download a packaged Windows release or work with the Python source.

## Option A — Windows executable (easiest)

1. Visit [GitHub Releases](https://github.com/justdumbprojects/naupos/releases).
2. Download the Windows EXE from the latest suitable release's **Assets**.
3. Follow that release's notes and complete the application's first-run setup using **test data** before live service.

A correctly packaged EXE includes its Python interpreter and Python dependencies, so **Python and pip are not required on the destination PC**. The desktop host may require Microsoft Edge **WebView2 Runtime** (commonly present on modern Windows). Google Sheets/Drive need internet access and separate authorization if you choose to enable them. A published EXE is not proof of clean-install compatibility; verify on a fresh Windows system.

## Option B — Python source (development)

- **Windows 10/11** and **Python 3.14 / 3.14t**. The project is developed with the free-threaded Python build; check installed versions using `py -0p`.
- **Git** or **GitHub Desktop** to clone the repository.
- A modern browser for the local HTML interface.
- Backend source in `server/server.py` and frontend pages in `pos/` (both are included in this repository).

Follow [How to set up](how%20to%20setup.md). This repository has not yet been verified as a complete clean-room source installation.

## Optional Google Sheets finance and Google Drive backup

These integrations are **not necessary for basic local POS operation**. To use them from Python source, install the dependencies into the interpreter that runs the server:

```powershell
py -3.14 -m pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

If using 3.14t, select the corresponding interpreter explicitly. Configure your own Google Cloud project, enable the Drive and Sheets APIs, and create a Desktop OAuth client; see [How to set up](how%20to%20setup.md). Never publish OAuth client files or access tokens.

## Public edition exclusions

The public POS edition is intended to operate locally **without the remote Founder/Owner API, Cloudflare Tunnel autostart, or live-camera streaming**. Neither FFmpeg nor cloudflared is a prerequisite for the public edition. If you encounter references to those features in code, report them as possible leftovers rather than treating them as required setup.

## Before using real business data

Test ordering, payment finalization, inventory deduction, printing, backups and recovery with fake data. Keep independent backups and do not assume a published release has been certified for production use.

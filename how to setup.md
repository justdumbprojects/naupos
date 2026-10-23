# How to set up Náu POS

This guide is for **Windows source development and initial configuration**, not a certified live-bar installation. If you only want to run the packaged Windows application, start at [GitHub Releases](https://github.com/justdumbprojects/naupos/releases) and follow its release notes. Read [What you need](what%20you%20need.md) first.

## 1. Get the source

Clone the repository with GitHub Desktop or PowerShell:

```powershell
git clone https://github.com/justdumbprojects/naupos.git
cd naupos
```

The Python backend is at `server/server.py`; frontend HTML pages are in `pos/`. Both are already published. The project is Windows-oriented and has not yet been validated as a complete fresh-install source distribution.

## 2. Install Python and optional dependencies

Install Python **3.14 / 3.14t**, matching the interpreter used for development. Verify installed interpreters:

```powershell
py -0p
```

Google Sheets and Drive integration is optional. If you plan to use it from source, install:

```powershell
py -3.14 -m pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

Use the corresponding interpreter if running 3.14t. The current source has interactive storage and integration setup; test with an isolated data directory and avoid pointing development runs at live data.

## 3. Optional: configure Google Cloud OAuth

Skip this entire section if you do not use Google Sheets finance or Google Drive backups.

1. Open https://console.cloud.google.com/ and create or select a project.
2. Enable the **Google Drive API** and **Google Sheets API**.
3. Configure the OAuth consent screen / Google Auth Platform branding. For an external app in Testing, add your account as a test user.
4. Create an **OAuth client ID** of type **Desktop app**.
5. Download its JSON privately. **Do not upload it to GitHub or bundle personal credentials in a public EXE.**
6. When prompted by the application, select your local OAuth client JSON. The backend can store its configuration beside `POSsettings.json`, typically under `%APPDATA%\NAUPOSSYS\`.
7. Complete browser authorization using the intended Google account; treat the saved OAuth token as sensitive.

**Permission note:** The current backend uses the broad Google Drive scope `https://www.googleapis.com/auth/drive`. Only authorize an account you trust; changing to narrower scopes requires code review and potentially reauthorization.

## 4. Optional: Google Sheets finance

After OAuth authorization, use the application's Finance/Settings integration controls to connect, test, and synchronize. Verify the generated spreadsheet and its values in the authorized Google account. Do not assume synchronization has succeeded until you check it.

## 5. Optional: Google Drive backup

Use the same OAuth setup with Drive API enabled. Run a manual backup with dummy data, confirm the uploaded copy exists, and **test restoration to a separate folder**. Keep independent local backups.

## 6. Replace the Náu logos

The server uses these image paths inside the selected data root:

```text
NAU/
  ASSETS/
    nau-logo-header.png
    nau-logo-receipt.png
```

- Replace `nau-logo-header.png` for the POS header.
- Replace `nau-logo-receipt.png` for receipts.
- Preserve PNG format and exact filenames.
- The backend includes built-in fallback logos, so **replace** files rather than just deleting them.
- Restart the server and refresh the frontend after replacing logos.

## 7. Public edition and safe testing

The public edition does not require **FFmpeg, camera RTSP configuration, Cloudflare Tunnel, or a remote Founder App connection**. These are not setup steps for the local public POS.

Use fake customers, dummy orders and isolated storage. Do not test payment finalization, inventory adjustments or backup restoration on production records. Keep `google_finance_client.json`, OAuth tokens, `POSsettings.json`, and databases out of version control.

**Known limitation:** A complete end-to-end clean Windows source installation and the published EXE have not been independently validated here. Treat these instructions as project setup guidance, not a guarantee of production readiness.

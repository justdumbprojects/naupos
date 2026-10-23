# How to set up Náu POS

These instructions are for a **development installation** on Windows, not for deploying a live bar with real customer data. Read [what you need.md](what%20you%20need.md) first.

## 1. Get the source

Clone https://github.com/justdumbprojects/naupos using GitHub Desktop or:

```powershell
git clone https://github.com/justdumbprojects/naupos.git
cd naupos
```

The Python backend is expected at `server/server.py` and frontend HTML at `pos/`. If those files have not yet been published, the repository is not runnable; wait for the sanitized source upload.

## 2. Install Python and Google dependencies

Install Python 3.14 (the project was developed using Python 3.14t on Windows). Confirm the interpreter:

```powershell
py -0p
```

Install the Google client libraries if you plan to use Google Finance/backup:

```powershell
py -3.14 -m pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

Launch the server using the matching interpreter after completing its initial configuration. The current code has interactive storage and Google setup steps; do not run it against production data for testing.

## 3. Create Google Cloud OAuth credentials

1. Open https://console.cloud.google.com/ and create or select a Google Cloud project.
2. Open **APIs & Services → Library**. Enable **Google Drive API** and **Google Sheets API** for that project.
3. Configure the Google Auth Platform **Branding / OAuth consent screen**. Choose the audience that matches your use case. For External apps in Testing, add your Google account as a **test user**. Google may impose testing limits and token-expiry behavior.
4. Open **Clients / Credentials**, create an **OAuth client ID**, and select **Desktop app**.
5. Download the client JSON. It contains a client ID and potentially a client secret. **Do not upload it to GitHub, paste it into issues, or bundle it into a public executable.**
6. On first launch, the current backend can prompt you to select this **Desktop OAuth client JSON**. Its configuration routine copies the selected JSON to the local settings directory beside `POSsettings.json`, typically `%APPDATA%\NAUPOSSYS\google_finance_client.json`.
7. Complete Google's browser authorization using the Google account whose Drive and Sheets you want to use. The app stores an OAuth token locally. Treat this token as sensitive too.

**Scope note:** The current backend requests the broad Google Drive scope `https://www.googleapis.com/auth/drive`. Only authorize an account you trust for this purpose. Narrowing the scope would require a reviewed code change and may require reauthorization.

## 4. Set up Google Sheets finance

1. Complete Google authorization above.
2. In the POS's Finance/Settings integration controls, connect or test Google Finance and run a finance synchronization.
3. The current backend is designed to find or create the finance spreadsheet in the connected Google Drive. Check the connected Google account's Drive for the generated spreadsheet and inspect the sheets before relying on it.
4. Do not upload a pre-existing production finance workbook or its sensitive contents to GitHub.

Google Sheets is **not** a separate API key you paste into the source; the application uses OAuth authorization.

## 5. Set up Google Drive backup

1. Use the same OAuth configuration, with Google Drive API enabled.
2. Configure the Google Drive backup in the POS integration settings and run a connection test.
3. Run a manual test backup using dummy data, verify that it appears in the authorized Google Drive, and test restoring it into an isolated folder.
4. Retain an independent local backup. Cloud backup success does not guarantee recovery until restore has been tested.

## 6. Change the Náu logos

The server uses two runtime image files inside the selected data root:

```text
NAU/
  ASSETS/
    nau-logo-header.png
    nau-logo-receipt.png
```

- Replace **`nau-logo-header.png`** to change the POS header logo.
- Replace **`nau-logo-receipt.png`** to change the printed receipt logo.
- Use PNG images and preserve the exact filenames.
- **Important:** The server contains built-in Base64 fallback logos. If a logo file is missing, it can regenerate the original. Therefore **replace** the file rather than deleting it.
- Restart the server and refresh the frontend after replacing logos. Keep backup copies of your artwork.

## 7. Optional FFmpeg camera streaming

1. Install FFmpeg and confirm `ffmpeg -version`.
2. Set `NAU_CAMERA_FFMPEG` if FFmpeg is not in PATH.
3. Set `NAU_CAMERA_RTSP_URL` to your own camera URL. Avoid embedding camera passwords in source or sharing configuration files.
4. Test the stream only on a trusted network.

## 8. Optional Cloudflare Tunnel

1. Install cloudflared and create a Tunnel in the Cloudflare dashboard.
2. Configure a public hostname to route to the correct local server endpoint.
3. Configure the tunnel token through the application's supported local protected settings or environment. Never hardcode it.
4. Confirm the local service works before testing HTTPS access remotely.
5. Rotate the tunnel token immediately if it was previously published.

## 9. Safe development practices

Use fake customers, dummy orders, and isolated storage. Do not test payment finalization, stock deduction, or backup restoration on live business data. Keep `google_finance_client.json`, OAuth tokens, `POSsettings.json`, Cloudflare tokens, and databases out of version control.

**Current limitation:** The codebase has not yet been validated as a complete clean-room installation. The instructions describe the observed source behavior and known dependencies, not a guaranteed one-click installer.

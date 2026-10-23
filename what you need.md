# What you need to run Náu POS

This guide describes the current **Windows-oriented Python source version**. Some parts of the POS require optional integrations. A packaged EXE may bundle components differently.

## Required

1. **Windows 10/11** (the current application includes Windows-specific behavior and deployment assumptions).
2. **Python 3.14 / 3.14t** — the project is developed with Python 3.14 free-threaded; start with the same interpreter used by the maintainer. Download from https://www.python.org/downloads/windows/ and verify with `py -0p`.
3. **Git** (https://git-scm.com/downloads) or **GitHub Desktop** (https://desktop.github.com/) to clone and update the project.
4. A modern browser such as **Microsoft Edge** or **Google Chrome** to open the POS frontend.
5. The backend and frontend source files in `server/` and `pos/`. At the time this document was added, these directories still needed to be published from the sanitized source snapshot.

## Google Sheets finance and Google Drive backup (optional)

Install the Python Google API dependencies using the **same Python interpreter** that starts the server:

```powershell
py -3.14 -m pip install google-api-python-client google-auth-httplib2 google-auth-oauthlib
```

If you run the free-threaded interpreter, ensure the installation and server launch use that same interpreter (check `py -0p`).

You will also need a Google Cloud project, enabled **Google Drive API** and **Google Sheets API**, and an OAuth **Desktop app** client JSON. Setup instructions: [how to setup.md](how%20to%20setup.md).

## Camera streaming (optional)

- Install **FFmpeg** from https://ffmpeg.org/download.html (Windows builds are linked from that page).
- Add `ffmpeg` to PATH, or set the `NAU_CAMERA_FFMPEG` environment variable to the executable path.
- Confirm: `ffmpeg -version`.
- Configure your own camera RTSP URL via `NAU_CAMERA_RTSP_URL`; keep passwords out of Git.

## Remote Founder/Owner API (optional)

- **cloudflared** from https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/
- A Cloudflare account and configured Tunnel with an appropriate public hostname.
- The server may attempt to find/download `cloudflared.exe` on Windows, but manual installation is useful for troubleshooting.
- Store the tunnel token in local protected settings or the supported runtime environment, **never in this repository**.
- Keep the public API protected with HTTPS and application authentication.

## Useful checks

```powershell
py -0p
ffmpeg -version
cloudflared --version
```

Not all integrations are necessary for basic local POS usage. The source currently lacks a fully verified end-to-end fresh-install dependency manifest, so additional environment-specific setup may be needed.

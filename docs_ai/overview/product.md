# Product overview

## What is HttpFS?

**HttpFS** (HTTP File Server / HTTP FS) is an Android application that turns a phone, tablet, or Android TV into a **local network file server**.

Other devices on the same Wi‑Fi (PC, laptop, phone, media player) can:

- Browse and manage files in a **web file manager** in the browser
- Mount the device as a **WebDAV** share (Finder, Windows Map Network Drive, third-party clients)
- Call a **REST API** (and WebSockets) for automation and the web UI
- Optionally subscribe to an **RSS** feed of a folder
- Use **HTTP** or **HTTPS** (self-signed, imported, or Let’s Encrypt DNS-01)

The Android app is the control plane (start/stop, settings, storage permissions). Remote UX is the bundled web client plus WebDAV/API.

## Who it is for

- Users who want a quick “NAS-like” share from a spare Android device
- Developers who need LAN file access without a PC
- Android TV users (Leanback launcher, D-pad-friendly settings)

## Distribution

| Flavor | Package id | Default port |
|--------|------------|--------------|
| Free | `tiar.ua.slf` | 8080 |
| Pro | `tiar.ua.slf.pro` | 8081 |

Both can be installed on the same device. See [free-vs-pro.md](free-vs-pro.md) and the user page [../user/free-vs-pro.md](../user/free-vs-pro.md).

## Core user journey

1. Grant storage (and notification) permissions.
2. Optionally pick server root folder / multi-volume mode.
3. Tap **Start** on Home (or widget / shortcut on Pro).
4. Ongoing notification shows `http(s)://{ip}:{port}`.
5. Open that URL from another device, or mount WebDAV at `/webdav`.
6. Stop from the notification or the app when finished.

Long runs with the screen off use a foreground service (`specialUse`) and optional battery exemption — [../operations/foreground-service.md](../operations/foreground-service.md).

## What this product is not

- Not a cloud sync product
- Not a full FTP product (FTP code may exist experimentally; not a supported user feature)

## Branding / names

- Store / UI: **HTTP FS**, **HttpFS**
- Docs tree: `docs_ai/`
- Namespace: `tiar.ua.slf`

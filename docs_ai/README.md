# HttpFS documentation

Public documentation for **HTTP FS** (HttpFS) — turn an Android phone, tablet, or TV into a LAN file server with a browser UI, WebDAV, optional HTTPS, and more.

**App version covered:** 1.1.22 · Android 5.0+ (`minSdk` 21)

| Start here | Audience |
|------------|----------|
| [user/getting-started.md](user/getting-started.md) | Anyone using the app |
| [user/settings-guide.md](user/settings-guide.md) | Every setting explained |
| [user/https-certificates.md](user/https-certificates.md) | HTTPS / certificates |
| [user/connect-clients.md](user/connect-clients.md) | Browser, WebDAV, RSS |
| [user/free-vs-pro.md](user/free-vs-pro.md) | Free vs Pro |
| [user/safety-and-faq.md](user/safety-and-faq.md) | Safety tips & FAQ |

Developers and integrators: see [Developer docs](#developer-docs) below.

---

## What the app does

On the same Wi‑Fi, other devices can:

- Browse and manage files in a **web file manager**
- Mount storage via **WebDAV**
- Use a **REST API** (used by the web UI; documented for advanced users)
- Follow an **RSS** listing of a folder
- Connect with **HTTP** or **HTTPS** (self‑signed, imported keystore/PEM, or Let’s Encrypt DNS‑01)

---

## User docs

| Doc | Description |
|-----|-------------|
| [user/getting-started.md](user/getting-started.md) | Install, permissions, start server, open from another device |
| [user/settings-guide.md](user/settings-guide.md) | App / Server / Client settings |
| [user/https-certificates.md](user/https-certificates.md) | SSL switch, certificate library, Let’s Encrypt |
| [user/connect-clients.md](user/connect-clients.md) | URLs for browser, WebDAV, RSS |
| [user/free-vs-pro.md](user/free-vs-pro.md) | Feature differences |
| [user/safety-and-faq.md](user/safety-and-faq.md) | Security advice and troubleshooting |

---

## Developer docs

Technical reference for building the app, integrating with the API, or contributing understanding of the architecture. Safe for public mirrors (no signing secrets or AdMob unit IDs).

### Overview & build

| Doc | Description |
|-----|-------------|
| [overview/product.md](overview/product.md) | Product summary |
| [overview/architecture.md](overview/architecture.md) | Architecture |
| [overview/free-vs-pro.md](overview/free-vs-pro.md) | Flavor technical notes |
| [getting-started/build.md](getting-started/build.md) | Gradle flavors |
| [getting-started/run.md](getting-started/run.md) | Dev install / TV notes |

### Features & modules

| Doc | Description |
|-----|-------------|
| [features/http-server.md](features/http-server.md) | Embedded server |
| [features/server-engines.md](features/server-engines.md) | CIO / Netty |
| [features/webdav.md](features/webdav.md) | WebDAV overview |
| [features/api.md](features/api.md) | API overview |
| [features/rss.md](features/rss.md) | RSS |
| [features/ssl-certificates.md](features/ssl-certificates.md) | Certificate library (dev) |
| [features/acme/dns01-guide.md](features/acme/dns01-guide.md) | ACME DNS‑01 |
| [features/storage.md](features/storage.md) | Storage / SAF |
| [features/users-auth.md](features/users-auth.md) | Auth model |
| [features/settings.md](features/settings.md) | Settings screens (code map) |
| [features/thumbnails-folder-size.md](features/thumbnails-folder-size.md) | Thumbs / folder size |
| [features/widgets-shortcuts.md](features/widgets-shortcuts.md) | Pro widgets |
| [features/ads-free.md](features/ads-free.md) | Free ads behavior |
| [modules/app.md](modules/app.md) · [acme.md](modules/acme.md) · [client.md](modules/client.md) · [free-pro.md](modules/free-pro.md) | Modules |

### Reference

| Doc | Description |
|-----|-------------|
| [reference/url-map.md](reference/url-map.md) | URL mounts |
| [reference/api-routes.md](reference/api-routes.md) | `/api/files` routes |
| [reference/websocket-zip.md](reference/websocket-zip.md) | ZIP over WebSocket |
| [reference/websocket-events.md](reference/websocket-events.md) | Live events |
| [reference/webdav-methods.md](reference/webdav-methods.md) | WebDAV methods |
| [reference/storage-paths.md](reference/storage-paths.md) | Path / volume rules |
| [reference/settings-keys.md](reference/settings-keys.md) | Preference keys |

### Operations & development

| Doc | Description |
|-----|-------------|
| [operations/lifecycle.md](operations/lifecycle.md) | Start / stop / boot |
| [operations/foreground-service.md](operations/foreground-service.md) | Long‑running server FGS |
| [operations/play-console-fgs-special-use.md](operations/play-console-fgs-special-use.md) | Play Console `specialUse` text |
| [operations/notifications.md](operations/notifications.md) | Notifications |
| [operations/permissions.md](operations/permissions.md) | Android permissions |
| [development/project-layout.md](development/project-layout.md) | Repo layout |
| [development/web-client.md](development/web-client.md) | Web UI build |
| [development/tv-focus.md](development/tv-focus.md) | Android TV focus |
| [development/conventions.md](development/conventions.md) | Contributor conventions |

---

## Publishing this folder

You can publish **only** the `docs_ai/` directory as a public wiki, GitHub Pages site, or DeepWiki corpus — it is self-contained (no required links outside this folder).

- Point end users at **User docs** (or this README).
- Do **not** add real keystore passwords, private keys, or ad unit IDs.
- Play Console FGS text for store listing: [operations/play-console-fgs-special-use.md](operations/play-console-fgs-special-use.md).

# Architecture

## High-level diagram

```
┌──────────────────────────────────────────────────────────────┐
│  Android UI                                                   │
│  SplashActivity → MainActivity (Home / Settings / Logs / …)   │
│  SettingsActivity (users, redirects, certs, …)                │
└────────────────────────────┬─────────────────────────────────┘
                             │ Settings.kt (SharedPreferences)
                             │ App.kt (singleton)
┌────────────────────────────▼─────────────────────────────────┐
│  KtorServer (embedded)                                        │
│  Engines: CIO or Netty  ·  SSL ⇒ Netty only                   │
│  Auth: Basic / form / sessions · blocked IPs                  │
│  Lifecycle: NotifService (FGS specialUse) + PARTIAL_WAKE_LOCK │
└───────┬──────────────┬──────────────┬──────────────┬─────────┘
        │              │              │              │
   RouteBase      RouteWebdav    RouteApi       RouteRss
   /files + HTML   /webdav/       /api/ (+ WS)   /rss/
        │
   HtmlBuilder + assets/web/template/  (+ runtime config.js)
        │
┌───────▼──────────────────────────────────────────────────────┐
│  storage/                                                     │
│  File API and/or SAF · multi-volume · path resolve/transfer   │
└──────────────────────────────────────────────────────────────┘
```

## Gradle modules

| Module | Role |
|--------|------|
| `:app` | Application: UI, server, storage, assets, flavors |
| `:free` | Free companion: AdMob + limited `ExtendUtils` |
| `:pro` | Pro companion: full `ExtendUtils`, no ads |
| `:acme` | ACME / Let’s Encrypt DNS-01 helpers (acme4j) |
| `client/` | Web UI sources (not a Gradle module; npm → assets) |

## Runtime layers

### Application (`App.kt`)

- Holds `KtorServer` instance
- Starts/stops `NotifService`
- Tracks LAN IP, wake lock (screen-on option), restart flags
- Defines route path constants (`files`, `webdav`, `api`, `rss`)

### Server (`server/KtorServer.kt`)

- Loads preferences via `Settings`
- Installs Ktor plugins (auth, sessions, websockets, compression, …)
- Mounts route modules
- Resolves SSL KeyStore through `server/ssl/`

### Storage (`storage/`)

- Resolves logical URLs to `File` or SAF `DocumentFile`
- Multi-volume “all storages” mode
- Listing, copy/move, zip, thumbnails helpers used by routes

### UI

- Settings screens are mostly **code-built preferences** (`PreferenceCustom`, etc.), not XML preference graphs
- Certificate edit uses a custom scrollable form with TV focus support
- Leanback `VerticalGridView` for TV preference lists

## Data persistence

- **SharedPreferences** via `settings/Settings.kt` (ports, SSL flags, users JSON, …)
- **App private files** for ACME stores, auto-cert caches, web resource copies
- **SAF persisted URI permissions** for removable volumes

## Process model

1. User starts server → `App.startService()` → `NotifService` as foreground service.
2. Service starts `KtorServer` on a background dispatcher if not already running.
3. Notification stays until Stop / server error / destroy.
4. Optional boot receiver restarts the server when “start on boot” is enabled.

## Related docs

- [product.md](product.md)
- [../features/http-server.md](../features/http-server.md)
- [../modules/app.md](../modules/app.md)

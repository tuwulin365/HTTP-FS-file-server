# Module `:app`

Main Android application. Namespace / package: `tiar.ua.slf`.

## Responsibilities

- Native UI (activities, fragments, dialogs, widgets)
- Embedded `KtorServer` and route modules
- Storage resolution (File + SAF)
- Settings façade
- Bundled web assets under `src/main/assets/web/`
- Product flavors `free` / `pro`

## Important packages

| Package | Purpose |
|---------|---------|
| `tiar.ua.slf` | `App`, `NotifService`, receivers |
| `…server` | `KtorServer`, engines, routes, SSL |
| `…storage` | Multi-volume, path resolve, transfers |
| `…settings` | `Settings.kt` |
| `…ui` | Activities, fragments, preference cards |
| `…utils` | Storage helpers, Pro façade, dialogs, logs |
| `…widget` | Pro home-screen widgets |

## Source sets

| Path | Role |
|------|------|
| `src/main/` | Shared code, resources, base manifest |
| `src/free/` | Free manifest overlays (ads, package) |
| `src/pro/` | Pro manifest overlays (widgets, shortcuts) |

## Entry activities

- `SplashActivity` — launcher / leanback / shortcuts
- `MainActivity` — Home, Settings hub, Logs, About
- `SettingsActivity` — nested settings (users, certs, …)

## When to edit here

Almost all product behavior lives in `:app`. Use `:free` / `:pro` only for the thin `ExtendUtils` / ads split, and `:acme` for ACME protocol details.

# HTTP(S) server

## Stack

- **Ktor 2.3.12** embedded server
- Engines: **CIO** or **Netty** (custom `NettyApplicationEngine` available)
- **HTTPS** forces **Netty**
- Extra: netty-tcnative BoringSSL, BouncyCastle for certs

## Lifecycle

1. `App.startServer()` / `startService()`
2. `NotifService` → `startForeground` (`specialUse` on API 34+)
3. `KtorServer.start()` binds host + port
4. Stop via notification action, Home UI, or `tryStop()`

`START_STICKY` + wake lock keep the process useful while the notification is active.

## Main URL map

| Path | Purpose |
|------|---------|
| `/` | Redirect / landing |
| `/files/...` | Web file manager HTML UI |
| `/web/template/...` | Static web assets |
| `/webdav/...` | WebDAV |
| `/api/...` | REST + WebSockets |
| `/rss/...` | RSS feed |
| `/login` | Login when password auth enabled |

Route name constants live on `App` (`fmDirName`, webdav, api, rss).

## Configuration (high level)

From `Settings` / server settings UI:

- Bind IP / interface selection
- Port
- Engine type
- Buffer size
- SSL on/off + selected certificate id
- Auth, users, session timeout
- WebDAV / RSS toggles
- Root path / multi-volume
- Initial file + optional hard redirect
- Blocked IPs, redirects (Pro)

## Engines

| Engine | Notes |
|--------|-------|
| CIO | Lighter; OK for simple HTTP |
| Netty | Preferred for SSL / heavier load |

## Logging

Server and app logs surface in the Logs tab; useful for bind failures (port in use) and SSL errors.

## Related

- [webdav.md](webdav.md)
- [api.md](api.md)
- [rss.md](rss.md)
- [server-engines.md](server-engines.md)
- [ssl-certificates.md](ssl-certificates.md)
- [../reference/url-map.md](../reference/url-map.md)
- [../operations/foreground-service.md](../operations/foreground-service.md)
- [../operations/lifecycle.md](../operations/lifecycle.md)

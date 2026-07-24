# URL map (server mounts)

Logical mounts from `App` + `KtorServer` routing. Host/port omitted.

| Mount | Constant | Doc |
|-------|----------|-----|
| `/` | landing / redirect | [http-server.md](../features/http-server.md) |
| `/files/…` | `fmDirName` | Web UI HTML (`RouteBase`) |
| `/web/template/…` | static assets | Bundled client |
| `/webdav/…` | `fmWebDavName` | [webdav-methods.md](webdav-methods.md) |
| `/api/…` | `fmApi` | [api-routes.md](api-routes.md) |
| `/rss/…` | `fmRssName` | [../features/rss.md](../features/rss.md) |
| `/login` | form login | [../features/users-auth.md](../features/users-auth.md) |

Pro **redirects** add extra `route(path)` entries from settings (mapped toward `/files` paths).

Auth plugin wraps most of the tree when password protection is on; WebDAV uses Basic, browser uses sessions after `/login`.

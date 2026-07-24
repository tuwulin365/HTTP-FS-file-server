# RSS feed

## Endpoint

**`/rss/{path…}`** (`App.fmRssName` = `rss`), enabled by Server → RSS (`rss_key`, default on).

## Behavior

- `GET` only (`RouteRss`).
- Directory → RSS XML listing of children (media-oriented feed for folder contents).
- File → serve/download that file (same storage stack as files/WebDAV).
- Multi-volume: resolves via `StorageRouteHelper.resolveRss` / `StorageUrlPaths.normalizeRssPath`.
- Respects hidden-file rules and volume errors like other mounts.
- Initial-file / hard-redirect helpers may apply in single-root mode (`handleFileRedirect`).

## Clients

Any RSS reader pointed at `http(s)://host:port/rss/` or a subfolder path. Not a full podcast CMS — folder listing as feed items.

## Implementation

`app/src/main/java/tiar/ua/slf/server/routes/RouteRss.kt`

# REST API reference

Base mount: **`/api/files`** (`App.fmApi` = `api`, `App.fmDirName` = `files`).

Unless noted, JSON uses UTF-8. Write operations require write permission (session user or anonymous write). Read operations require read permission when password auth is on.

Volume / SAF failures often return JSON:

```json
{ "error": "VOLUME_UNKNOWN|VOLUME_UNMOUNTED|…", "message": "…" }
```

Permission denied:

```json
{ "error": "Error#9", "message": "Permission denied" }
```

---

## WebSockets

| URL | Purpose |
|-----|---------|
| `WS /api/files/status` | Keepalive / online probe. Sends `online` periodically; `offline` if server stops. Disabled when Client “check connection” is off. Auth required if password mode on. |
| `WS /api/files/events` | Live storage/UI events via `LiveEventHub`. Auth: must `canRead`. |
| `WS /api/files/download-zip` | Interactive zip build over the socket (progress frames). Auth: `canRead`. |

Exact zip protocol frames are defined in `RouteApi.route` (download-zip) and the web client — read code when integrating externally.

---

## HTTP GET

### `GET /api/files/list`

Directory listing JSON for the web UI.

| Query | Default | Meaning |
|-------|---------|---------|
| `path` | `""` | Logical path under files mount (URL-decoded) |
| `type` | `all` | Filter (as used by client) |
| `sort` | `name` | Sort field |
| `order` | `asc` | `asc` / `desc` |
| `show_parent` | `0` | Include parent entry when `1` |

### `GET /api/files/tree`

Recursive / tree JSON listing (same path resolution family as list).

### `GET|HEAD /api/files/file`

Download or metadata for a file. Supports **Range** requests for partial content. Query/path conventions follow `getFileJsonResponse()` (see `RouteApi.kt`).

### Empty stubs

`GET /api/files`, `GET /api/files/`, `GET /api/` → `404` with `{ "error": "Empty request" }`.

---

## HTTP POST (mutations)

Bodies are JSON unless upload (raw stream).

### `POST /api/files/delete`

```json
{ "names": ["a.txt", "folder"], "path": "storage/Documents" }
```

Deletes each name under `path`. Write required. Multi-volume: `path` is the logical URL path (see [storage-paths.md](storage-paths.md)).

### `POST /api/files/rename`

JSON map (string values), typically:

```json
{ "path": "storage/Documents/old.txt", "name": "new.txt" }
```

(`path` = current item; `name` = new basename.) Write required.

### `POST /api/files/move`

```json
{ "paths": ["storage/a.txt", "storage/b.txt"], "pathEnd": "storage/Archive" }
```

Moves each source path into destination folder `pathEnd`. Write required.

### `POST /api/files/save`

```json
{ "path": "storage/notes.txt", "content": "file text…" }
```

Overwrite text file contents. Write required. Hidden paths may return `Error#66`.

### `POST /api/files/create`

```json
{ "path": "storage/Documents", "name": "NewFolder/" }
```

- `name` ending with `/` → create directory
- otherwise → create empty file  

Write required.

### `POST /api/files/upload`

Raw body = file bytes.

| Query | Meaning |
|-------|---------|
| `path` | Parent folder logical path |
| `name` | File name |
| `overwrite` | Optional; interpreted as true/false |

Supports `Content-Length` and `Content-Range` for resumable-style uploads (`HttpUtils.parseContentRangeForUpload`). Rejects upload to multi-volume virtual root. May emit low-space notifications.

---

## Auth notes

- Browser UI uses sessions after `/login`.
- When password protection is off, anonymous rights come from global Read/Write settings.
- WebSockets check `canRead` / connection settings similarly to HTTP.

## Implementation

Primary file: `app/src/main/java/tiar/ua/slf/server/routes/RouteApi.kt`  
Listing JSON shape: `storage/listing/ApiListingAdapter.kt`

When this table drifts, trust the Kotlin source.

# REST API and WebSockets

## Base path

**`/api/...`** — implemented in `RouteApi.kt` (and helpers).

The bundled web UI talks to this API for listing, uploads, renames, deletes, zip, thumbnails, etc.

## Capabilities (overview)

Exact paths evolve with the web client; conceptually the API covers:

- Directory listing / tree
- Upload / download
- Rename, move, copy, delete
- Zip download
- Thumbnails
- Live events over **WebSockets** (`LiveEventHub`)

**Full route table:** [../reference/api-routes.md](../reference/api-routes.md)  
ZIP framing: [../reference/websocket-zip.md](../reference/websocket-zip.md) · Events: [../reference/websocket-events.md](../reference/websocket-events.md)  
Prefer reading `RouteApi.kt` and `client/src/js/` if that table drifts.

## Auth

Same session / Basic / anonymous rules as the HTML UI. Rights are reflected in runtime `config.js` for the browser client.

## WebSockets

Used for live updates (storage changes, operation progress). Keep the connection on the same host/port as the server.

## Errors

JSON error payloads for volume/SAF failures are normalized via storage helpers (`respondVolumeErrorJson`, etc.).

## Related

- [../reference/api-routes.md](../reference/api-routes.md)
- [../reference/storage-paths.md](../reference/storage-paths.md)
- [../modules/client.md](../modules/client.md)
- [storage.md](storage.md)
- [users-auth.md](users-auth.md)

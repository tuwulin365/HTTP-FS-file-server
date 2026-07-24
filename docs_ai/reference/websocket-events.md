# Live events WebSocket

Endpoint: **`WS /api/files/events`** (`LiveEventHub`).

Requires `canRead`. The web client keeps a connection for live list refresh after uploads/deletes/moves.

## Hub API (server)

| Call | Effect |
|------|--------|
| `LiveEventHub.register(session)` | Track socket |
| `unregister` | Drop on close |
| `broadcastListChanged(relativePath)` | Notify clients that a folder listing changed |
| `broadcastUploadBlocked(message, error)` | e.g. low space (`Error#21`) |

`StorageLiveEvents` normalizes paths and calls the hub after storage mutations.

## Client

`connectLiveEvents` / reconnect helpers in the web client (`client/src/js`). Treat payload as JSON text frames; exact keys live in `LiveEventHub` + client parsers — prefer code if integrating externally.

Status probe is a **separate** socket: `/api/files/status` (online/offline text), gated by Client “check connection”.

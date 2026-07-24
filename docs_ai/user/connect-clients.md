# Connect from other devices

Replace `IP` and `PORT` with the values shown in the app / notification.

| Service | URL |
|---------|-----|
| Web file manager | `http://IP:PORT/` or `https://IP:PORT/` |
| WebDAV | `http://IP:PORT/webdav/` |
| RSS | `http://IP:PORT/rss/` or a subfolder under `/rss/…` |
| REST API (advanced) | `http://IP:PORT/api/…` — see [../reference/api-routes.md](../reference/api-routes.md) |

With **password protection**, the browser asks you to log in; WebDAV clients use **HTTP Basic** (username/password).

## Browser

1. Same Wi‑Fi as the Android device.
2. Open the home URL.
3. Upload / download / rename as allowed by permissions.

## WebDAV examples

Enable **Settings → Server → WebDAV** first (default is off).

- **macOS Finder:** Go → Connect to Server → `https://IP:PORT/webdav/` (or `http://…`).
- **Windows:** Map network drive / third‑party WebDAV tools with the same URL.
- **Mobile file managers:** Add a WebDAV account with host, port, path `/webdav/`, and credentials if needed.

Some clients prefer HTTPS. If you use a self‑signed cert, trust/export it — [https-certificates.md](https-certificates.md).

## RSS

Point an RSS reader at `/rss/` (or a folder path) to see items derived from that directory listing. Useful for media folders; not a full podcast CMS.

## Multi‑volume (“All storages”)

Paths include a volume id, e.g. `/files/storage/DCIM/…`. WebDAV and RSS follow the same idea. Grant SD access under App → Storage permissions if a volume shows as needing permission.

## Widgets (Pro)

Home‑screen widgets and a launcher shortcut can start/stop or show status — see [../features/widgets-shortcuts.md](../features/widgets-shortcuts.md).

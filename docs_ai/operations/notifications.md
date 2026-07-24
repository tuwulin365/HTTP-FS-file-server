# Notifications

## Server ongoing notification

Shown while `NotifService` runs (foreground service).

| Item | Notes |
|------|-------|
| Purpose | Keep FGS alive; show LAN URL; Stop action |
| Channel | Name like `HTTP FS Background Service`; id derived per package helper |
| Action string | Free: `tiar.ua.slf.NOTIFICATION_BUTTON` · Pro: `tiar.ua.slf.pro.NOTIFICATION_BUTTON` |
| Stop | Intent to `NotifService` with stop id — shuts down server / service |

Notification IDs can overlap across Free and Pro installs; channels/actions are package-scoped so dual-install is safe.

## Other notifications

Low free space / transfer helpers may post additional notifications (`LowSpaceNotifier` and related). Treat those as UX, not FGS anchors.

## Related

- [foreground-service.md](foreground-service.md)
- [../features/widgets-shortcuts.md](../features/widgets-shortcuts.md)

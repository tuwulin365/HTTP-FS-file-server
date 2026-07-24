# Server lifecycle (start / stop / boot)

## Start paths

| Trigger | Flow |
|---------|------|
| Home UI Start | `App.startServer()` → `startService()` → `NotifService` → `KtorServer.start()` |
| Splash / shortcut / widget | Same service path (Pro shortcuts/widgets) |
| Start with app | Splash may start service after permissions |
| Boot | `BootReceiver` on `BOOT_COMPLETED` if “start on boot” enabled → `startServer()` |

`LOCKED_BOOT_COMPLETED` is handled carefully: auto-start waits for normal boot after unlock (see `BootReceiver`).

## Stop paths

| Trigger | Flow |
|---------|------|
| Notification Stop | `NotifService` action → stop server / service |
| Home UI Stop | `App` stop helpers → `ktorServer?.tryStop()` |
| Restart | `restartServer()` → tryStop then start again |
| Engine switch / SSL change | Often needs restart (UI/settings may call restart) |

`tryStop()` sets a flag used when tearing down CIO/Netty cleanly.

## Reliability pieces

- FGS `specialUse` + notification (see [foreground-service.md](foreground-service.md))
- `PARTIAL_WAKE_LOCK` while service runs
- Optional ignore-battery-optimizations
- `START_STICKY`-style service behavior as implemented in `NotifService`

## Dual Free + Pro

Separate packages → separate services, ports (8080 / 8081), notifications, prefs. Both may run at once.

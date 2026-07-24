# Widgets and shortcuts (Pro)

Pro-only entry points declared in `app/src/pro` (+ widget classes under `app/.../widget/`).

## Home-screen widgets

| Provider | Action constant | Behavior |
|----------|-----------------|----------|
| `ServerWidgetProvider` | `tiar.ua.slf.action.WIDGET_TOGGLE_SERVER` | Toggle start/stop server |
| `ServerInfoWidgetProvider` | `tiar.ua.slf.action.WIDGET_INFO_TOGGLE` | Shows status/IP; toggle delegates to same start/stop path |

Shared busy/state helper: `WidgetServerToggleState` (prevents double-taps while starting/stopping; refreshes widgets).

Tap target also opens `SplashActivity` / app as configured in the provider layouts.

Free builds: widget providers are not in the free manifest; `UtilsPro.isPro` guards no-op early returns in providers.

## App shortcut

`app/src/pro/res/xml/shortcuts.xml` + Splash intent-filter:

| Action | Meaning |
|--------|---------|
| `tiar.ua.slf.action.SHORTCUT_START_SERVER` | Launcher long-press shortcut to start server via Splash |

`SplashActivity.ACTION_SHORTCUT_START_SERVER` detects the action and continues into the start flow after permissions as implemented.

## Notifications (both flavors)

Ongoing FGS notification (not Pro-exclusive):

- Shows URL
- Stop action → `NotifService` with `id=stop` (action string differs by package: free vs pro — see `NotifService.ACTION`)

## Related

- [../overview/free-vs-pro.md](../overview/free-vs-pro.md)
- [../operations/foreground-service.md](../operations/foreground-service.md)

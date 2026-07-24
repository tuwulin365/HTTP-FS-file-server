# Foreground service and wake lock

## Why

HttpFS must accept TCP connections and transfer files while the UI is backgrounded and the **screen is off**, often for days. That is not a short sync job.

## Type: `specialUse` (not `dataSync`)

On Android 14+ / target 35+:

- `dataSync` FGS has a **~6 hour / 24h** budget and cannot be started from `BOOT_COMPLETED` (Android 15+).
- **`specialUse`** has no that timeout and is allowed for this user-started server use case (subject to Play review).

Manifest (`NotifService`):

- Permission: `FOREGROUND_SERVICE_SPECIAL_USE`
- `android:foregroundServiceType="specialUse"`
- Property: `android.app.PROPERTY_SPECIAL_USE_FGS_SUBTYPE` → `@string/fgs_special_use_subtype`
- Runtime: `ServiceCompat.startForeground(..., FOREGROUND_SERVICE_TYPE_SPECIAL_USE)` on API 34+

## Wake lock

While the notification service runs, a **PARTIAL_WAKE_LOCK** is held (`{packageName}:NotifService`) so the CPU can service the socket with the display off.

A separate optional screen wake lock in `App` is tied to battery/settings UX (keep screen on), not the server socket itself.

## Older Android

- API &lt; 34: FGS type not enforced the same way; `startForeground` without type; wake lock still used.
- API 21–25: `startService` instead of `startForegroundService`.

## OEM caveat

Aggressive battery savers can still kill long-running apps. Users should allow **ignore battery optimizations** when they need weeks-long uptime.

## Play Console

Full English justification text: [play-console-fgs-special-use.md](play-console-fgs-special-use.md)  
(also summarized for reviewers in that file).

Declare **Foreground service types → Special use** in App content, with a short demo video (start → notification → LAN client → stop).

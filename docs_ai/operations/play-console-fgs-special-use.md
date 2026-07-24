# Google Play: Foreground service type `specialUse`

HTTP FS runs a **user-started local HTTP/WebDAV file server** on the device.
That work is not covered by `dataSync` (or other predefined FGS types): the
server must stay alive for hours or weeks while the screen is off, until the
user explicitly stops it. Android 14+ therefore requires
`foregroundServiceType="specialUse"` plus a Play Console declaration.

## Manifest (already in the app)

- Permission: `FOREGROUND_SERVICE_SPECIAL_USE`
- Service: `NotifService` → `android:foregroundServiceType="specialUse"`
- Property: `android.app.PROPERTY_SPECIAL_USE_FGS_SUBTYPE`
  (`@string/fgs_special_use_subtype`)
- Runtime: `ServiceCompat.startForeground(..., FOREGROUND_SERVICE_TYPE_SPECIAL_USE)`
- `WAKE_LOCK` / `PARTIAL_WAKE_LOCK` keeps the CPU available for the listening
  socket while the display is off (only while the server notification is active)

## Play Console declaration (English)

**Path:** Play Console → App content → Foreground service types → `Special use`

### Short description (manifest subtype / summary field)

```
User-started local HTTP/WebDAV file server that must stay running while the screen is off so clients on the LAN can browse and transfer files for as long as the user keeps the server enabled.
```

### Detailed explanation for reviewers

```
HTTP FS (HTTP File Server) is a local network file server app. Its core feature is that the user can start an HTTP and/or WebDAV server on their Android phone or tablet and then access the device’s files from other devices on the same Wi‑Fi network (PC, laptop, another phone, media player, etc.).

Why a foreground service is required
• The server must accept incoming TCP connections and serve file transfers even when the app UI is not visible and the screen is turned off.
• Stopping the process would immediately disconnect clients and interrupt uploads/downloads.
• The user explicitly starts and stops the server from the app (or notification). The service is not started for opportunistic background sync.

Why the “specialUse” type (not “dataSync” or others)
• This is not a short background sync, backup, or upload job. The server is a long-running network listener that users commonly leave enabled for days or weeks (home NAS-style use).
• The “dataSync” foreground service type is intended for finite sync tasks and is not appropriate for an indefinite, user-controlled local server that must remain reachable around the clock.
• No other predefined foreground service type (mediaPlayback, connectedDevice, remoteMessaging, etc.) matches hosting a user-initiated HTTP/WebDAV file server on the device.

How the service is used
1. User opens the app and taps Start (or uses a widget / shortcut).
2. NotifService starts as a foreground service with an ongoing notification that shows the server URL and a Stop action.
3. A PARTIAL_WAKE_LOCK is held only while this service is running so the CPU can keep the server socket responsive with the screen off.
4. When the user stops the server (notification Stop, in-app Stop, or related controls), the service releases the wake lock and stops.

User control and transparency
• An ongoing notification is always visible while the server is running.
• The user can stop the server at any time from the notification or the app.
• Battery optimization exemption may be requested so OEMs do not kill the long-running server; that is optional and explained in app settings.

This specialUse declaration is limited to keeping the user-started local file server process alive. It is not used for ads, location tracking, or undisclosed background work.
```

### Demo video tips (if Play asks for one)

Show: open app → Start server → notification with URL → open the URL from another device on the same Wi‑Fi → transfer a file → Stop from the notification → service/notification gone.

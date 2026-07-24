# Users and authentication

## Modes

1. **Password protection off** — anonymous access; global read/write switches apply.
2. **Password protection on** — users must authenticate (form login for browser, Basic for WebDAV/API as configured).

## User model

`UserInfo` (serialized in preferences):

- Name / password
- Permissions string: `r`, `w`, `rw` (and related flags as implemented)
- Optional custom home folder

## Sessions

- Cookie / server sessions with configurable timeout
- Force logout / logout-all helpers in settings
- Session limits may differ by Free/Pro

## Free vs Pro

- Free: effectively a **single** user (Pro labels / `UtilsPro` guards)
- Pro: multiple users

## Blocked IPs

Separate list under Server security settings.

- Free: capped count
- Pro: unlimited

Edit UI: `SettingsFragmentBlockedIps` + dialog.

## Redirects (Pro)

Experimental URL/file redirects (`SettingsFragmentRedirects`). Gated behind Pro.

## Implementation entry points

- `settings/Settings.kt` — persistence
- `server/` auth plugins + `UserSession`
- `UtilsPro` / `ExtendUtils` — Free limits
- UI: `SettingsFragmentUsers`, `SettingsFragmentUserEdit`

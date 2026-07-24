# Settings guide

Settings are grouped into **App**, **Server**, and **Client**. Some items appear only when a parent switch is on, or only in Free / Pro.

Defaults below match the current app (1.1.22). Items that need the server **stopped** say so.

---

## 1. App

### Language

App UI language. Default: system. Changing it reloads settings UI.

### Start server with device

Auto‑start after reboot. Default: OFF. On Xiaomi / Huawei / Oppo / Vivo / Honor / etc. you may also need OEM auto‑start permission.

### Start server with app

Start when you open the app. Default: OFF. Otherwise use **Start** on Home.

### Logs / All logs

Request logging for the Logs tab. Logs default ON; “All logs” is OFF and only shown when Logs is on.

### Haptics / Blur in dialogs

UI feedback. Blur defaults ON on Android 12+, OFF on older devices.

### Ads & privacy (Free)

Open the consent / ad privacy screen.

### Disable ads (Free)

On the main Settings screen after About: watch a **rewarded ad** to hide banner/interstitial ads until the **app process ends** (force‑stop or system kill). Not a multi‑day timer.

### Battery permissions

Request ignore‑battery‑optimizations so the server is less likely to be killed. Recommended for long runs.

### Permissions for folders / Storage permissions

Grant SAF access for SD cards and removable volumes. Use after **All storages** or when a volume needs re‑granting.

### Clear app data

Wipes HttpFS settings and app cache only — **not** your photos/documents on the device.

---

## 2. Server

### WebDAV

Enable `/webdav/`. Default: **OFF**. Summary shows the WebDAV URL when the server is up. Can toggle while running.

### RSS

Enable `/rss/`. Default: **ON**. Summary shows the RSS URL. Can toggle while running.

### Name (Pro)

Server display name. Default: “HTTP FS”. Change when server is stopped.

### IP

Which address to bind (auto / interfaces / localhost). Changing restarts if running; edit when stopped.

### PORT

Listen port. Defaults: Free **8080**, Pro **8081**. Change when stopped. If the port is busy, pick another.

### Path to folder

Server root. Default: internal shared storage.

- Summary may show `/`, `/[storage]`, or `/[sd card] …`.
- **All storages (multi‑volume):** from the picker, go up to the volume list (`/`) and confirm. URLs look like `/files/storage/…` or `/files/{volumeId}/…`. Grant removable volumes under App → Storage permissions.
- Change when server is stopped.

### Initial file / Path to file / Hard redirect

Optional homepage file under the root. Hard redirect always sends `/` to that file. Change when stopped.

### Server type

**Auto** (default), **CIO**, or **Netty**. With **SSL on**, Netty is forced. Change when stopped. Prefer Auto unless you are debugging.

### Buffer Size

Transfer buffer. Larger can be faster, uses more RAM. Use reset/recommended if unsure.

### Blocked IP Addresses

Deny listed client IPs immediately. Free: limited count; Pro: unlimited. Edits apply without full restart.

### Redirects (Pro, experimental)

Map a path/URL to another path or URL. Add / edit / delete rules on the Redirects screen.

### Use password

Require login. Default: OFF. When OFF, anyone on the LAN can use the server per **Permissions**. Change when stopped.

### Users (when password on)

Accounts with Read / Write / Read+Write and optional home folder. Free: effectively one user; Pro: multiple. WebDAV uses HTTP Basic. Change when stopped.

### Session time / Logout

Session lifetime in minutes (default 60). Logout disconnects all sessions immediately.

### Permissions (when password off)

Anonymous **Read** and/or **Write**. Default: Read. Write lets guests delete/overwrite — use carefully.

### SSL (https)

Serve `https://`. Default: OFF. Forces Netty. Change when stopped. See [https-certificates.md](https-certificates.md).

### Certificates (when SSL on)

Opens the **certificate library**: Auto (self‑signed), Import (keystore/PEM), Let’s Encrypt (DNS‑01). Select one profile for the server. Export PEM when available for trusting clients.

---

## 3. Client

### Name

Client/device label used in places in the UI.

### Welcome dialog / text (Pro for full text)

Optional message shown to browser visitors.

### Hide files (Pro)

Paths hidden from listings / WebDAV. Changes apply immediately.

### Get size of folder

Recursive folder sizes in listings. Default: **OFF**. Uses more CPU/disk (“battery expense”).

### Get thumbnails

Image/video thumbs in the web UI. Default: **ON**. Uses more CPU/battery. Clear cache when shown.

### Check connection socket

Periodically checks whether the browser client is still connected to the server (WebSocket status). Default: **OFF**. Small extra cost (“battery expense”).

---

## Related

- [getting-started.md](getting-started.md)
- [https-certificates.md](https-certificates.md)
- [safety-and-faq.md](safety-and-faq.md)
- Developer preference keys: [../reference/settings-keys.md](../reference/settings-keys.md)

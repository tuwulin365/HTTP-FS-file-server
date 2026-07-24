# SSL certificates

HttpFS maintains a **certificate library** (multiple profiles). The server stores:

- `useSsl` (boolean)
- `sslCertificateId` (selected profile)

UI: **Settings → Server → Certificates** (list) and certificate edit screen.

## Profile modes

| Mode | Purpose |
|------|---------|
| **Auto** | Self-signed cert generated on device; optional “keep after restart”; regenerate action |
| **Import** | User keystore (`.p12` / `.jks`) or PEM cert+key; password for keystore |
| **Let’s Encrypt** | ACME DNS-01 via `:acme` — Prepare DNS → publish TXT → Verify & issue |

## Selection UX

- Radio selects the active HTTPS certificate.
- Edit icon / long-press (TV) opens the editor.
- Re-clicking the selected item opens edit.
- If a profile is not ready, selection may redirect the user to finish setup.

## Auto details

- Generator: `AutoCertificateGenerator`
- Cache toggle (switch) — keep material across restarts
- Export PEM when available

## Import details

- Format radios: Keystore vs PEM
- File pickers for cert/keystore and optional key
- Password dialog for keystore
- Validation when used for HTTPS / export

## Let’s Encrypt details

Categories on the edit screen:

1. **Domain** — domain, email, Prepare DNS
2. **DNS record** — TXT host/value, share (after prepare)
3. **Issue** — Verify & issue, export when issued

Prepare / Verify use cancelable progress dialogs (result or error shown afterward).

Step-by-step + failure modes: [acme/dns01-guide.md](acme/dns01-guide.md).

## Storage on disk

Under app-private SSL/ACME directories (per profile id): keystores, password files, pending DNS instructions. See `server/ssl/` in the app source and [acme/dns01-guide.md](acme/dns01-guide.md).

## Engine note

Enabling SSL switches the server engine to **Netty**.

## Play / security notes

Certificates are for serving HTTPS on the LAN (and public LE domains). Cleartext HTTP remains available when SSL is off. App `usesCleartextTraffic` / network security config govern **outbound** app traffic, not the LAN listener semantics.

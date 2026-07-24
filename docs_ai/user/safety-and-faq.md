# Safety tips and FAQ

## Safety

- Prefer **password protection** on any network that isn’t fully trusted.
- Prefer **Read‑only** for guests; give **Write** only to people you trust (write can delete files).
- Use **HTTPS** on untrusted Wi‑Fi; for LAN self‑signed, export and trust the certificate on clients.
- Choose a **narrow root folder** instead of sharing the whole device when possible.
- **Hidden files** (Pro) hide paths from listings — not a substitute for passwords.
- **Blocked IPs** stop specific clients quickly.
- Exposing the server to the **internet** (router port forward) increases risk. Use strong passwords, HTTPS with a real cert when possible, and understand what you are sharing. Not recommended for beginners.

## FAQ / troubleshooting

**Server won’t start**  
Port in use → change **PORT**. Check Logs for bind/SSL errors.

**Other devices can’t open the URL**  
Same Wi‑Fi? VPN/isolation (“AP isolation” / guest Wi‑Fi) can block device‑to‑device traffic. Try `http://` vs `https://` to match SSL. Confirm the IP on the phone still matches.

**WebDAV fails**  
Enable WebDAV in Server settings. Try HTTPS + trusted cert. Check username/password and Read/Write rights.

**SD card / write fails**  
Grant **Storage permissions** / folder access for that volume. In multi‑volume mode, re‑run the permission wizard after replugging the card.

**Files missing**  
They must be under the server root. Check **Hide files**. In multi‑volume mode, open the correct volume id in the path.

**Slow or hot phone**  
Disable thumbnails and folder sizes; turn down “all logs”; keep buffer at recommended size.

**Ads still show (Free)**  
Rewarded “disable ads” lasts until the app process ends. Upgrade to Pro for no ads.

**Certificate / Let’s Encrypt verify fails**  
TXT record wrong or not propagated; wait and retry. Avoid hammering production Verify (rate limits). See [https-certificates.md](https-certificates.md).

**Server dies overnight**  
Enable battery exemption; keep the notification; disable aggressive OEM battery savers for HttpFS; optional start‑on‑boot.

## More help

- [settings-guide.md](settings-guide.md)
- [getting-started.md](getting-started.md)
- Developer FGS notes: [../operations/foreground-service.md](../operations/foreground-service.md)

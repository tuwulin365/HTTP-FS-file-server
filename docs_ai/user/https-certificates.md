# HTTPS and certificates

## Enable HTTPS

1. Stop the server if it is running.
2. **Settings → Server → SSL (https)** → ON.
3. Open **Certificates** and pick or create a profile.
4. Start the server. URLs become `https://IP:PORT/…`.

Server engine switches to **Netty** automatically while SSL is on.

## Certificate types

### Auto (self‑signed)

- Generated on the device.
- Browsers and many WebDAV clients will warn until you trust the cert.
- Use **Export** (PEM) and install/trust it on clients when possible.
- **Keep after restart** (cache) reuses the same material across restarts when enabled on the profile / related switch.

### Import

- Load a **keystore** (`.p12` / `.jks`) with password, or **PEM** certificate + private key.
- Use this if you already have a cert from another CA or tool.

### Let’s Encrypt (DNS‑01)

For a **public domain name you control** (not required for pure LAN self‑signed use).

1. Create a Let’s Encrypt profile; enter **domain** and **contact email**.
2. **Prepare DNS** → app shows a **TXT** host and value.
3. Create that TXT record at your DNS provider; wait for propagation.
4. **Verify & issue** → certificate is stored on the device.
5. Select the profile and enable SSL.

Use DNS staging only while testing (staging certs are **not** trusted by browsers). Production is for real clients. Rate limits apply on production — don’t spam Verify.

Details for power users: [../features/acme/dns01-guide.md](../features/acme/dns01-guide.md).

## Tips

- LAN‑only: Auto + export/trust is usually enough.
- Internet exposure (port forward): use a real hostname + Let’s Encrypt or a proper imported cert, **and** password protection. See [safety-and-faq.md](safety-and-faq.md).
- Changing certificate or SSL usually needs a server restart.

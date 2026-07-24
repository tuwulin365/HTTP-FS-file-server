# Module `:acme`

Pure JVM/Android library for **Let’s Encrypt** certificate issuance using **DNS-01** (acme4j).

## Why it exists

HttpFS cannot complete HTTP-01 challenges for arbitrary public domains from a phone behind NAT. DNS-01 lets the user publish a TXT record and then finish issuance on-device.

## Used by

`app` → `server/ssl/AcmeCertificateStorage.kt` and the certificate edit UI (Prepare DNS / Verify & issue).

## Typical flow

1. User enters domain + contact email.
2. **Prepare DNS** → ACME account + order → pending TXT host/value stored on disk.
3. User creates the TXT record at their DNS provider (share/copy helpers in UI).
4. **Verify & issue** → complete challenge → store KeyStore + password files under app ACME dir.
5. Server selects the ACME profile and serves HTTPS.

## Notes

- Staging vs production is controlled by profile flags in app code (`acmeStaging`).
- Long ACME network calls run off the UI thread; the edit screen shows a cancelable progress dialog.
- Do not put Play/UI strings in this module — keep it protocol-focused.

See [../features/ssl-certificates.md](../features/ssl-certificates.md) and [../features/acme/dns01-guide.md](../features/acme/dns01-guide.md).

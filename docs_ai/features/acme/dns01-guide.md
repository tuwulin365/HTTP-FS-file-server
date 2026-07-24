# Let’s Encrypt (ACME DNS-01) guide

## When to use

You need a **publicly trusted** cert for a **DNS name you control**. The phone usually cannot receive Let’s Encrypt HTTP-01 on port 80 from the internet, so HttpFS uses **DNS-01** (TXT record).

## Staging vs production

`SslCertificateProfile.acmeStaging` (default `false` = production).

| | Staging | Production |
|---|---------|------------|
| CA | Let’s Encrypt staging | Let’s Encrypt production |
| Trust | **Not** trusted by browsers | Trusted |
| Rate limits | Loose | Strict |

Use staging while debugging DNS; switch to production for real HTTPS clients. Staging issuance still exercises the full Prepare → TXT → Verify flow.

*(If the UI does not expose a staging switch in your build, change the profile field in storage / add UI — field exists on the profile model.)*

## User flow

1. Create certificate profile, mode **Let’s Encrypt**.
2. Enter **domain** (e.g. `files.example.com`) and **contact email**.
3. **Prepare DNS** (progress dialog, cancelable).
4. Create the shown **TXT** record at your DNS host (`TXT host` / `TXT value`; Share action available).
5. Wait for DNS propagation.
6. **Verify & issue** (progress dialog). On success, KeyStore is stored and Status becomes valid.
7. Select the profile for the server and enable SSL; restart server if needed.

## On-disk layout (per cert id)

Under ACME storage dir for the profile (`AcmeCertificateStorage.storageDir`):

| File / store | Role |
|--------------|------|
| Pending DNS instructions | After Prepare, before Verify |
| TXT record helper file | Share / copy |
| `store` + password file | Issued KeyStore after Verify |

`hasIssuedStore` / `loadPendingInstructions` drive UI enablement.

## Failure modes

| Symptom | Likely cause |
|---------|----------------|
| Prepare fails immediately | Network, ACME API, invalid email/domain |
| Verify fails: DNS / TXT | Record missing, wrong name/value, not propagated, wrong zone |
| Verify fails: rate limited | Too many production attempts — use staging or wait |
| Status “DNS pending” | Prepared but not issued yet |
| Status “Not issued yet” | No store on disk |
| Browser warns on staging cert | Expected for staging CA |

UI shows exception `message` in the result dialog when available.

## Guards

- Domain / email required before Prepare.
- Verify requires pending instructions (`Prepare DNS first`).
- Changing mode away from Auto clears auto cache; selection may clear if profile becomes unready.

## Related

- [../ssl-certificates.md](../ssl-certificates.md)
- [../../modules/acme.md](../../modules/acme.md)
- [../../user/https-certificates.md](../../user/https-certificates.md)

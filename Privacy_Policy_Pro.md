# Privacy Policy — HTTP FS Pro

**App:** HTTP FS (file server) — Pro  
**Package:** `tiar.ua.slf.pro`  
**Developer:** Tiar Develop / Tiar Apps  
**Contact:** [tiar.develop@gmail.com](mailto:tiar.develop@gmail.com)

This Privacy Policy describes how the **HTTP FS Pro** application (“Service”, “app”) handles information.  
It applies only to the **Pro** edition. The free edition may include advertising and has a separate privacy policy.

**Effective date:** 2026-07-25

---

## Summary

- HTTP FS Pro is a **paid / Pro** local network file server for Android.
- **No ads.** The Pro app does **not** include AdMob, advertising SDKs, or advertising identifiers for ads.
- App settings, certificates, and optional server logs are stored **on your device**.
- The developer does **not** operate a backend that collects your personal files or browsing history from the app.
- If you start the built-in HTTP/WebDAV server, **other devices you allow on your network** may access the folders you share — that is the purpose of the app.
- Optional features (for example **Let’s Encrypt** certificates) may send limited data to **third-party certificate authorities** that you choose to use.

---

## Who provides the Service

Tiar Apps / Tiar Develop provides HTTP FS Pro. The Service is intended for use as purchased or obtained through official distribution channels (for example Google Play).

By using the Service, you agree to this Privacy Policy. If you do not agree, do not use the app.

---

## Information Collection and Use

### Data stored on your device

For the app to work, it may store on your device (and not upload to the developer):

- App preferences and settings (port, paths, users, blocked IPs, language, and similar)
- Optional SSL/TLS certificate material you generate or import
- Optional local request logs if you enable logging in settings
- Cached files such as thumbnails (if enabled)

**Files on your storage** (photos, documents, and other data you choose to share through the server) remain on your device unless **you** transfer them via the server to another device or service.

The developer does **not** receive a copy of your personal files through normal use of this Pro app.

### Permissions

Depending on Android version and features you use, the app may request access to:

- **Storage / files** — to serve and manage the folders you select  
- **Network** — to run the local server and, if you choose, obtain certificates online  
- **Notifications** — to show that the server is running  
- **Battery optimization exemption** (optional) — so the server can keep running reliably  
- Other related permissions declared in the app’s Play Store listing / manifest  

You can deny optional permissions; some features may then be unavailable.

### No advertising

HTTP FS Pro:

- Does **not** show ads  
- Does **not** use Google Mobile Ads / AdMob  
- Does **not** request the advertising ID for ad personalization  

There is **no** in-app “Ads & privacy” consent flow for advertising in Pro (that exists only in the free edition).

### Optional Let’s Encrypt / ACME

If you use the optional **Let’s Encrypt** (DNS-01) certificate feature, you may enter a **domain name** and **contact email**. That information is used to request a certificate from the certificate authority (Let’s Encrypt) according to their processes and policies. Certificate-related data may also be stored locally on your device.

This step happens only when **you** start the certificate issuance flow. See Let’s Encrypt’s own privacy policy for how they process ACME-related data.

### Local network server

When you start the server:

- Devices on the same network (or any network path you configure) may connect to the URLs shown in the app  
- Depending on your settings, visitors may list, download, upload, or delete files under the shared roots  
- If you enable password protection, access is limited to the credentials you configure  
- Server access logs (if enabled) stay on your device unless you export or share them yourself  

You are responsible for choosing what to share, who can reach your device, and whether to use passwords / HTTPS.

---

## Log Data

The app can write **local** logs on your device (for example connection or error information you enable in settings). Those logs are for your troubleshooting.

The developer does **not** automatically collect crash or analytics telemetry from HTTP FS Pro as part of an advertising or analytics SDK stack.

If you contact support and voluntarily send logs, screenshots, or diagnostics, that information is used only to help resolve your request.

Google Play (the store) may process install, purchase, and review-related data under Google’s policies when you obtain the app from Play — that is outside this app’s own processing.

---

## Cookies

The Android app itself does not use browser cookies for advertising tracking.

The **web file manager** served by your local server may use normal session mechanisms (for example cookies or sessions) **on devices that connect to your server**, so that login and browsing work. That traffic stays between those clients and **your** device; it is not sent to the developer.

---

## Service Providers / Third Parties

HTTP FS Pro does **not** embed advertising providers.

Depending on how you use the app and how you obtained it, third parties may include:

| Party | When | Role |
|-------|------|------|
| Google Play / Google | Install, updates, payments, store policies | Distribution and store services — see [Google Privacy Policy](https://policies.google.com/privacy) |
| Let’s Encrypt (or ACME CA you use) | Only if you issue a certificate in the app | Certificate issuance — see their privacy policy |
| Your own clients / users | When your server is running | Access to folders you shared, under your configuration |

The developer does not sell your personal information.

---

## Security

Reasonable technical measures are used to protect data stored by the app on your device (for example app-private storage for certificates). No method of electronic storage or network transmission is 100% secure.

You should use password protection, careful folder selection, and HTTPS where appropriate, especially on untrusted networks.

---

## Children’s Privacy

The Service is not directed at children under 13. The developer does not knowingly collect personal information from children under 13. If you believe a child has provided such information to the developer (for example via email support), contact us so it can be deleted.

---

## Links to Other Sites

The app or its web UI may contain links (for example to GitHub, donation pages, or documentation). External sites are not operated by the developer; their privacy practices are their own.

---

## Changes to This Privacy Policy

This policy may be updated from time to time. The current version will be posted at the same location (for example this file in the project repository or the URL linked from the Play Store listing). Continued use of the Service after changes means you accept the updated policy.

**Effective date of this Pro policy:** 2026-07-25

---

## Contact Us

Questions about this Privacy Policy:  
**Email:** [tiar.develop@gmail.com](mailto:tiar.develop@gmail.com)

---

## Free vs Pro (privacy note)

| | Free (`tiar.ua.slf`) | Pro (`tiar.ua.slf.pro`) |
|---|---------------------|-------------------------|
| Ads / AdMob | May apply — see Free privacy policy | **No** |
| Advertising ID for ads | May apply | **Not used for ads** |
| Core file server on device | Yes | Yes |
| Optional Let’s Encrypt | Yes (if offered in build) | Yes (if offered in build) |

Always use the privacy policy that matches the edition you installed.

# Server engines (CIO / Netty)

Selection lives in `KtorServer` after reading Server → engine type (`servtype_key0`, often `"Auto"`).

## Decision

```text
useNetty = (type == Netty) || (type == "Auto") || sslEnabled
```

| Case | Engine |
|------|--------|
| SSL on | **Netty** (always) |
| Auto | **Netty** |
| Explicit Netty | Netty |
| Explicit CIO | CIO (HTTP only) |

HTTPS uses `sslConnector` with KeyStore from `SslCertificateResolver` / selected profile. Bind host from IP setting: `0.0.0.0`, `127.0.0.1`, or a specific address.

## Netty tuning (why it matters)

Comments in code: large buffer + short write timeout broke slow Wi‑Fi video. Current knobs:

- `responseWriteTimeoutSeconds = 60`
- `requestQueueLimit = 100`
- `HttpServerCodec` max chunk size tied to **buffer size** setting (`coerceAtLeast` default decoder chunk)

CIO path: `connectionIdleTimeoutSeconds = 60`. CIO uses smaller HTTP chunks and does **not** honor buffer size the same way for uploads — another reason Auto → Netty.

Custom `Netty2` factory exists in source but is not the active default path.

## Plugins (both engines)

Installed in `module()` roughly: CallLogging, ForwardedHeaders, Compression, PartialContent, WebSockets, StatusPages, Sessions, Authentication, then routes (redirects, `/`, files, login, API, optional WebDAV/RSS).

## Related

- [../features/http-server.md](../features/http-server.md)
- [../operations/lifecycle.md](../operations/lifecycle.md)
- [../features/ssl-certificates.md](../features/ssl-certificates.md)

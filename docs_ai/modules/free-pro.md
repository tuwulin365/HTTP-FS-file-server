# Modules `:free` and `:pro`

Thin Android library modules with a **shared API surface** and different implementations.

## API surface (conceptually)

- `ua.tiar.slf.pro.ExtendUtils` — `isPro()`, user list limits, redirects/hidden-files helpers, etc.
- Ad initialization hooks (real AdMob in free; no-ops / absent in pro)

`:app` depends on one of them via flavor:

```text
freeImplementation project(':free')
proImplementation project(':pro')
```

## Free (`:free`)

- `ExtendUtils.isPro() == false`
- AdMob SDK + APPLICATION_ID in free manifest
- `AD_ID` permission
- Enforces free limits when called from `UtilsPro`

## Pro (`:pro`)

- `ExtendUtils.isPro() == true`
- No ads
- Full multi-user / redirects / hidden files persistence behavior

## App-side façade

Prefer `tiar.ua.slf.utils.UtilsPro` inside `:app` instead of calling `ExtendUtils` everywhere. That keeps call sites clean and testable.

## Manifest split

Widget providers and app shortcuts are declared in **`app/src/pro/AndroidManifest.xml`**, not inside the `:pro` AAR necessarily — check both when changing Pro-only entry points.

## Related

- [../overview/free-vs-pro.md](../overview/free-vs-pro.md)
- [../features/ads-free.md](../features/ads-free.md)

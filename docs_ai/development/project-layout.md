# Project layout

```text
HttpFS/
├── app/                 # Android application (:app)
│   ├── src/main/        # Shared code, res, assets, manifest
│   ├── src/free/        # Free overlays
│   ├── src/pro/         # Pro overlays
│   └── build.gradle     # Flavors, version, SDK
├── free/                # :free library
├── pro/                 # :pro library
├── acme/                # :acme ACME library
├── client/              # Web UI sources (npm)
├── docs_ai/             # Public documentation (this tree)
├── docs/                # Optional legacy notes in the full repo (not required to publish docs_ai)
├── build.gradle         # Root plugins / versions
├── settings.gradle      # Module includes
├── gradle.properties
└── gradle.properties.local   # Optional signing (local)
```

## Where to look first

| Task | Start here |
|------|------------|
| Version / SDK | `app/build.gradle` |
| Server routes | `app/.../server/routes/` |
| SSL | `app/.../server/ssl/` + `acme/` |
| Settings keys | `app/.../settings/Settings.kt` |
| Free/Pro gates | `app/.../utils/UtilsPro.kt` |
| Web UI | `client/src/` then deploy to assets |
| FGS / Play text | `docs_ai/operations/foreground-service.md`, `play-console-fgs-special-use.md` |

## Generated / local (usually not for docs commits)

- `build/`, `.gradle/`, `client/dist/`
- IDE `.idea/`
- `local.properties`

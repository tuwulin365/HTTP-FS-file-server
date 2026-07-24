# Storage

## Goals

Expose device files to HTTP / WebDAV / API clients while supporting:

- Primary shared storage
- SD cards / USB (often via **SAF**)
- Optional **multi-volume** root (“all storages”)

## Key types

| Area | Role |
|------|------|
| `StoragePathResolver` | Map URL/path → `ResolvedAccess` (File or SAF) |
| `VolumeGrant` / registry | Persisted volume permissions |
| `StorageListingService` | Directory listings |
| `StorageTransfer` | Copy/move streams |
| `StorageVolumeReceiver` | Mount/unmount events |

## Server root modes

Configured in Server settings:

1. **Single folder** — user-picked path / tree URI
2. **Multi-volume** — virtual root listing volumes; deeper paths resolve per volume

## SAF vs File

- Where possible, direct `java.io.File` is used.
- Removable / restricted trees use Storage Access Framework document trees.
- Upload free-space checks and error messages are volume-aware (`LowSpaceNotifier`, volume error strings).

## Permissions

- Legacy `READ/WRITE_EXTERNAL_STORAGE` (maxSdk 32)
- `MANAGE_EXTERNAL_STORAGE` for broader access on newer APIs
- Runtime folder permission UX in App settings / dialogs

## Hotplug

`StorageVolumeReceiver` reacts to media mounted/unmounted so listings stay consistent.

## Related

- [../reference/storage-paths.md](../reference/storage-paths.md) — URL paths and volume ids
- [settings.md](settings.md)
- [../operations/permissions.md](../operations/permissions.md)

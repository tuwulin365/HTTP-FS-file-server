# Storage URL paths and multi-volume

## Mount prefixes

| Mount | Constant | Example |
|-------|----------|---------|
| Web UI / files | `files` | `http://host:port/files/…` |
| WebDAV | `webdav` | `http://host:port/webdav/…` |
| RSS | `rss` | `http://host:port/rss/…` |
| API | `api` + `files` | `http://host:port/api/files/list?path=…` |

Normalization strips the mount prefix and rejects `.` / `..` segments (`StorageUrlPaths`).

## Root modes

`ServerRootMode` (`server_root_mode` pref):

| Mode | Behavior |
|------|----------|
| `SINGLE_PATH` | One root folder (`path_value` / per-user root). Logical path is relative to that folder. |
| `MULTI_VOLUME` | Virtual root lists volumes. Paths are `{volumeId}/relative/path`. |

Multi-volume picker token (settings UI): `$httpfs$multi_volume` (`VolumeGrant.MULTI_VOLUME_PICKER_TOKEN`).

## Volume IDs

| Pattern | Meaning |
|---------|---------|
| `storage` | Primary volume (`VolumeGrant.PRIMARY_VOLUME_ID`) |
| `sd:…` | Removable / SD style id |
| UUID-like hex | Other volumes from `VolumeGrantRegistry.volumeIdFor` |

Invalid first segments in multi-volume mode are treated carefully in `parseUrlPath` (may yield errors / empty relative).

## Resolution pipeline

```text
URL / query path
  → StorageUrlPaths.normalize*(…)
  → StoragePathResolver.resolve(urlPath, UserPathContext)
       SINGLE → File(root + relative)
       MULTI  → VirtualRoot | FileAccess | SafAccess | VolumeError
  → routes / transfers
```

## Access kinds

- **FileAccess** — `java.io.File`
- **SafAccess** — SAF `DocumentFile` tree
- **VirtualRoot** — list of volumes (cannot upload/delete here)
- **VolumeError** — unknown / unmounted / needs grant

Grant state machine: `NOT_NEEDED`, `REQUIRED`, `GRANTED`, `SKIPPED`, `DENIED`, `STALE` (`VolumeGrant`).

## Examples

Single root:

```text
path=Documents/Photos
→ {root}/Documents/Photos
```

Multi-volume:

```text
path=storage/DCIM/Camera
→ primary volume + DCIM/Camera

path=          (empty)
→ virtual root listing volumes
```

WebDAV hrefs include volume id segments in multi-volume mode (`WebDavListingAdapter`).

## Related code

- `storage/StorageUrlPaths.kt`
- `storage/StoragePathResolver.kt`
- `storage/VolumeGrant.kt` / `VolumeGrantRegistry.kt`
- `storage/StorageListingService.kt`

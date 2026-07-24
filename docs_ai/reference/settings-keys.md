# Settings keys reference

Persistence: default `SharedPreferences` via `settings/Settings.kt`.  
Many keys are defined as `translatable="false"` string resources in `app/src/main/res/values/strings.xml`; others are hard-coded in Kotlin.

Defaults below are approximate — always confirm in `Settings.kt`.

## Server

| Pref key | Accessor (approx.) | Type | Default / notes |
|----------|--------------------|------|-----------------|
| `port_value` | `getPortVal` | Int | Free 8080 / Pro 8081 (`KtorServer.defaultPort`) |
| `name_client_value` | `getClientNameVal` | String | `"Client"` / `"PRO"` |
| `name_serv_value` | `getServerNameVal` | String | `"HTTP FS"` |
| `path_value` | `getRootFolderVal` | String | Internal storage path; multi-volume token possible |
| `server_root_mode` | `getServerRootMode` | String enum | `SINGLE_PATH` / `MULTI_VOLUME` |
| `volume_grants_v1` | `getVolumeGrantsJson` | String JSON | Volume grant list |
| `usefile_value` | `getUseRootFileVal` | Boolean | Use initial file |
| `file_redirect_value` | hard redirect | Boolean | |
| `file_value_path` | initial file path | String | |
| `file_value_name` | initial file name | String | |
| `ssl_key` | `getUseSSLVal` | Boolean | HTTPS on/off |
| `ssl_certificate_id` | `getSslCertificateId` | String | Selected profile id |
| `cache_cert` | `getIsCacheCert` | Boolean | Auto cert keep-after-restart (also mirrored per profile) |
| `secure_key` | `getUsePassVal` | Boolean | Password protection |
| `pass_key` | `getPassVal` | String | Legacy single-password field when users list empty — see `Settings.getPassVal` (do not hard-code defaults in docs) |
| `users_list` | `getUsersList` | String list | Preferred users storage |
| `users` | legacy set | Set | Migrated into `users_list` |
| `session_key` | `getSessionVal` | Int | Minutes, default `60` |
| `session_num_key` | `getSessionNumVal` | Int | Session count limit |
| `permissions_key` | anonymous R/W set | Set | contains `permissions_key_read` / `_write` |
| `servtype_key0` | `getServerTypeVal` | String | `"Auto"` (engine selection) |
| `buffer_size` | `getBufferSizeVal` | Int | Optimal default from `StorageUtils` |
| `blocked_ips` | `getBlockedIpsVal` | Set | |
| `redirects` | `getRedirectsVal` | Set | Pro |
| `webdav_key` | `getUseWebDavVal` | Boolean | default false |
| `rss_key` | `getUseRssVal` | Boolean | default true |
| `ip_host` | `getIpTypeVal` | String | `"all"` etc. bind/host mode |

## App

| Pref key | Accessor | Type | Notes |
|----------|----------|------|-------|
| `start_app_key` | start with device | Boolean | Boot |
| `start_server_key` | start with app | Boolean | |
| `show_logs` | `getLogsVal` | Boolean | default true |
| `show_logs_all` | verbose logs | Boolean | |
| `app_lang` | app UI language | String | empty = system |
| `server_lang` | server/web language | String | |
| `use_vibro` | haptics | Boolean | |
| `use_blur` | dialog blur | Boolean | default true on API 31+ |
| `battery_key` | battery exemption / keep awake prefs | Boolean | default true |
| `permission_folder_key` | folder permission related | | |
| `version_value` | last seen version | String | |
| `count_server_started` | starts counter | Int | ads / tips |
| `show_first_splash` / `show_first_msgs` | onboarding flags | Boolean | |
| `main_started` | MainActivity started flag | Boolean | |
| `rewarded_ad_free_until` | Free ads pause | | cleared on demand |

## Client

| Pref key | Accessor | Type | Notes |
|----------|----------|------|-------|
| `client_con` | connection check socket | Boolean | drives `/api/files/status` WS |
| `battery_folder_size_key` | compute folder sizes | Boolean | |
| `battery_thumbnail_key` | thumbnails | Boolean | default true |
| `welcome_dialog_key` | welcome HTML | String | Pro editable |
| `welcome_dialog_show_key` | show welcome | Boolean | |

## Storage helpers

| Pref key | Notes |
|----------|-------|
| `uri_sd_{name}` | Legacy/per-volume SAF URI helpers |
| `uri_cur` | Current picker URI |

## Certificate profiles (not plain prefs)

Certificate library metadata lives in app-private files under the SSL/ACME store (see `SslCertificateRepository`), not only SharedPreferences. Prefs keep `ssl_key` + `ssl_certificate_id` (+ `cache_cert`). User guide: [../user/https-certificates.md](../user/https-certificates.md).

## Notes

- Prefer `Settings` getters/setters over raw keys when changing code.
- Free/Pro limits are enforced in `UtilsPro`, not by omitting keys.
- Clearing app data wipes these prefs and local cert stores.
- End-user descriptions: [../user/settings-guide.md](../user/settings-guide.md).

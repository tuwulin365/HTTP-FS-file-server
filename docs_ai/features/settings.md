# Settings (developer map)

UI is built in code (`PreferenceCustom`, nested `SettingsActivity` screens), not XML preference graphs.

**End-user explanations:** [../user/settings-guide.md](../user/settings-guide.md)

## Categories (code)

| Area | Fragment |
|------|----------|
| App | `SettingsFragmentApp` |
| Server | `SettingsFragmentServer` |
| Client | `SettingsFragmentClient` |
| Users / edit | `SettingsFragmentUsers`, `SettingsFragmentUserEdit` |
| Redirects | `SettingsFragmentRedirects` |
| Hidden files | `SettingsFragmentHiddenF` |
| Blocked IPs | `SettingsFragmentBlockedIps` |
| Certificates / edit | `SettingsFragmentCertificates`, `SettingsFragmentCertificateEdit` |

Category extras: `Utils.SETTINGS_CAT_*`.

## TV

Leanback `VerticalGridView` on TV lists; certificate edit uses focusable rows + `ensureFocus()`. See [../development/tv-focus.md](../development/tv-focus.md).

## Pref keys

[../reference/settings-keys.md](../reference/settings-keys.md)

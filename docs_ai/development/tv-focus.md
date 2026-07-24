# Android TV / D-pad focus

Detection: `UiUtils.isTv(context)`.

## Settings lists

Preference-style screens swap the list host to Leanback **`VerticalGridView`** when on TV (same pattern as Users / Certificates / App / Redirects / Hidden / Blocked IPs):

- Window alignment / focus scroll strategy set for D-pad navigation
- Preference click / long-press wiring stays on the preference adapter (`PreferenceCustom`)

## Certificate edit

Custom rows (`item_setting_row` / category headers):

- Rows are focusable; padding adjusted for TV
- Non-interactive chrome (`ScrollView`, progress, cards) marked non-focusable so focus stays on rows
- After panel rebuilds (mode / DNS state), call **`ensureFocus()`** so the first useful row gets focus

## End actions on TV

Where phone UI uses a trailing edit icon click, TV often uses **long-press** via `endActionListeners` on `PreferenceCustom` (Certificates list → open editor).

## For contributors

When adding a settings list screen, copy an existing TV block (`SettingsFragmentUsers` / `SettingsFragmentCertificates`). For custom screens, mirror certificate edit: focusable rows + `ensureFocus` after async UI changes.

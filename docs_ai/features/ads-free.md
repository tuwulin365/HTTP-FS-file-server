# Free ads and Pro upgrade UI

High-level product behavior only. Ad unit IDs stay in the Free module / manifests, not in public docs.

## Where ads live

| Piece | Location |
|-------|----------|
| AdMob init / interstitial / rewarded | `:free` → `ua.tiar.slf.pro.ad.AdMobInitialize` |
| UMP / privacy options | `GoogleMobileAdsConsentManager` + App settings “Ads privacy” |
| Session “ads off after reward” | `RewardedAdFreeSession` (in-process flag until process death) |
| App façade | `MainActivity` + `Settings` grant/clear helpers |

Pro flavor has no ad SDK wiring.

## User flows

1. **Interstitial** — Free may show on certain navigation / resume paths when not in rewarded-free session (`MainActivity`).
2. **Disable ads (rewarded)** — Settings → App entry `disable_ads_reward` → watch rewarded ad → `grantRewardedAdFree()`; banner/interstitial gated off until process ends.
3. **Privacy / consent** — Settings → Ads privacy → `AdMobInitialize.showPrivacyOptions`.
4. **Upgrade to Pro** — `UtilsDialog.openProDialog` from About, Pro-locked preferences, limit hits (users, blocked IPs, etc.).

Legacy pref `rewarded_ad_free_until` is cleared on upgrade paths; current model is process-lifetime session, not a stored expiry.

## Limits vs ads

Free feature caps (users, blocked IPs, …) are **`UtilsPro` / `ExtendUtils`**, independent of whether ads are temporarily disabled.

## Related

- [../overview/free-vs-pro.md](../overview/free-vs-pro.md)
- [../modules/free-pro.md](../modules/free-pro.md)

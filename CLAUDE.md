# CLAUDE.md

Guidance for Claude Code (and other contributors) working in this repository.

## What this is

**Prayers Time** is a personal fork of [Bilal](https://github.com/cdjalel/Bilal) — a free,
ad-free, privacy-friendly Android app that shows Muslim prayer times computed on-device from
the user's location. Licensed **GPL-3.0** (see `COPYING`). Keep upstream credits and the
license intact in any change you publish.

- **App id:** `com.djalel.android.bilal` (unchanged from upstream)
- **Display name:** "Prayers Time" (`app/src/main/res/values/strings.xml` → `app_name`)
- **Min/target/compile SDK:** 17 / 33 / 33 · Java 8 · AGP 8.1 · Gradle 8.0 (needs **JDK 17**)

## Remotes

- `origin` → this fork (`nouman-tariq/prayers-time`)
- `upstream` → `cdjalel/Bilal`
- Pull upstream updates: `git fetch upstream && git merge upstream/master`
- A GitHub fork of a public repo is itself public; this repo was created as a standalone
  private repo (later made public) rather than a GitHub "fork".

## Changes this fork makes vs upstream

| Change | Where |
|--------|-------|
| App renamed to "Prayers Time" | `app/src/main/res/values/strings.xml` (`app_name`) |
| Hijri (Umm al-Qura) date under the Gregorian date | `activities/MainActivity.java` → `formatHijriDate()` + `updatePrayerViews()` |
| 12-hour AM/PM prayer times | `helpers/PrayerTimes.java` → `formatPrayerTime()` |
| Athan off by default | `res/xml/notifications_preferences.xml` + `helpers/UserSettings.java` (`isAthanEnabled`) |
| About text updated for the fork, About view set to `locale` direction | `res/values/strings.xml` (`pref_txt_about`), `res/layout/activity_about.xml` |
| `keystore.properties` made optional so CI/debug builds work | `app/build.gradle` |

Notes:
- The Hijri date uses `android.icu.util.IslamicCalendar` (API 24+); it returns null on older
  devices, so the code is guarded by `Build.VERSION.SDK_INT`. Build the formatter **from** the
  Islamic calendar (`DateFormat.getDateInstance(calendar, …)`) — using a plain `SimpleDateFormat`
  with `setCalendar()` keeps Gregorian month/era names ("January"/"BC").

## Build

CI builds a debug APK on every push: `.github/workflows/build.yml` (JDK 17 →
`./gradlew assembleDebug`) and uploads it as the `prayers-time-debug-apk` artifact.

Locally: `./gradlew assembleDebug` → `app/build/outputs/apk/debug/app-debug.apk`.

Release signing reads `keystore.properties` at the repo root if present (not committed); without
it, only debug builds are produced.

## Installing the debug APK (caveats)

- The CI APK is **debug-signed**, and each CI run uses a **fresh debug key**, so you cannot
  upgrade in place — **uninstall first**, then install.
- Play Protect blocks debug installs over adb (`INSTALL_FAILED_VERIFICATION_FAILURE`). Either
  turn off "Scan apps with Play Protect" in the GUI, or temporarily
  `adb shell settings put global verifier_verify_adb_installs 0` (restore to `1` after).
- For a stable upgrade path, add release signing in CI via a keystore stored as a GitHub secret.

## Conventions

- Keep it lightweight and offline; no ads, no trackers, no new network permissions.
- Preserve GPL-3.0 headers and upstream attribution.
- Prayer-time strings are localized — update both `values/` and `values-ar/` where relevant.

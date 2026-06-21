# Prayers Time

A lightweight, ad-free, privacy-friendly **Muslim prayer-times** app for Android.
It shows the five daily prayer times calculated from your location, with no ads,
no tracking, no account, and no internet required — everything is computed on-device.

This is a personal fork of [**Bilal**](https://github.com/cdjalel/Bilal) by Djalel Chefrour,
released under **GPL-3.0**.

## Features

- Five daily prayer times based on your GPS location
- **Gregorian and Hijri (Islamic) date** shown together
- **12-hour (AM/PM)** time format
- Multiple calculation methods (MWL, ISNA, Umm al-Qura, …) and Asr madhab
- Athan (adhan) alarm — **off by default**, can be enabled in Settings
- Fully offline · no ads · no data collection

## Changes from upstream Bilal

- Renamed the app to **"Prayers Time"**
- Added the **Hijri date** under the Gregorian date
- Prayer times shown in **12-hour AM/PM** format
- **Athan disabled by default**
- Builds the debug APK automatically via GitHub Actions (no keystore required)

## Build

Pushing to this repo triggers a GitHub Actions build that produces a debug APK.
Download it from the run's **Artifacts**, or build locally:

```bash
./gradlew assembleDebug
# output: app/build/outputs/apk/debug/app-debug.apk
```

## Credits & License

Based on **Bilal** by Djalel Chefrour, which uses the PrayerTime library from the
[Arab Eyes](http://arabeyes.org) Islamic Tools project.

Licensed under the **GNU General Public License v3.0** — see [COPYING](./COPYING).

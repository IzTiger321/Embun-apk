# Embun (Android)

Embun is a personal finance app for Malaysia. This repository is the **Android version** (APK). It is a thin shell that opens the Embun web app, so the Android version has the same features and data as the browser version.

The web version lives in the Embun-web repository. Both versions are one product; project documentation is kept in Notion.

## What this app does

- Opens https://iztiger-embun.vercel.app inside an Android app.
- Web updates appear on the next launch, so you do not need a new APK for web changes.
- Shows an offline page with a Retry button if the phone cannot reach Embun.

Publish a new APK only when the Android shell changes (app ID, icon, permissions or native plugins).

## App details

- App ID: `com.embun.iztiger`
- Web address: set in `capacitor.config.json` (`server.url`)
- Version: set in `package.json` (`version`)

## Download the APK

Each build is published on the **Releases** page of this repository as `embun-<version>v.apk`, for example `embun-1.1.0v.apk`.

1. Open the repository's **Releases** page.
2. Download the APK for the latest version.
3. On the phone, allow installs from your file manager, then open the APK.

If you already have an older Embun app installed with a different app ID, uninstall it first.

## Build (GitHub Actions)

The workflow **Build and Release Embun APK** runs on every push to `main`, or manually from the **Actions** tab. It:

1. Installs Node.js 20 and Java 17.
2. Creates the Android project (`npx cap add android`) if it is missing, and syncs it.
3. Builds a debug APK with Gradle.
4. Creates a GitHub Release tagged `v<version>` and attaches the renamed APK.

To release a new version, change `"version"` in `package.json` first. Building again without a version change replaces the APK in the same release.

## Build locally (optional)

Requires Node.js 20, JDK 17 and Android Studio.

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android
```

In Android Studio, choose **Build > Build APK(s)**.

## Project layout

```
capacitor.config.json   App ID, app name and web address
package.json            Capacitor dependencies, scripts and version
www/index.html          Offline page shown when Embun cannot be reached
.github/workflows/      GitHub Actions build and release
.gitignore              Files Git should not track
README.md               This file
```

The `android/` folder is created at build time and is not stored in this repository.

## Changing the web address

Edit `server.url` in `capacitor.config.json` and `www/index.html` (Retry button), then run `npx cap sync android`.

## Signing

The release APK is a debug build and is not signed for the Play Store. A signed release build needs a keystore stored as GitHub secrets, which is not set up yet.

## Privacy and terms

The Privacy Policy and Terms of Service are in the app (Settings, or the link on the sign-in page).

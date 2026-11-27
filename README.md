# Embun APK

Android app for Embun. It is a thin shell that loads https://embun-theta.vercel.app.
Web updates reach the app automatically on the next launch, so you do not need
to publish a new APK for web changes. Publish a new APK only when native
plugins or Android permissions change.

## Build the APK (GitHub Actions)

1. Push to `main` (or open the Actions tab and run **Build Embun APK** manually).
2. When the run finishes, download the `embun-debug-apk` artifact.
3. Copy `app-debug.apk` to your phone, allow installs from your file manager, and install.

## Build locally (optional)

Requires Node 20, JDK 17 and Android Studio.

    npm install
    npx cap add android
    npx cap sync android
    npx cap open android

Then use Build > Build APK(s) in Android Studio.

## Changing the web address

Edit `server.url` in `capacitor.config.json`, then run `npx cap sync android`.

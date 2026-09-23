# Flight Weather for Android

The flight weather planner (METAR, decoded TAF, SIGMETs, G-AIRMETs, PIREPs, a 7-day outlook with crosswinds, and the bluebird) as an installable Android app.

GitHub builds the APK for you. You don't need Android Studio or anything installed on your computer.

## Build the APK

1. Create a new repository on GitHub. Private is fine.
2. Upload everything in this folder, keeping the folders as they are, including the hidden `.github` folder.
   - With Git: `git init`, `git add .`, `git commit -m "Flight Weather"`, `git branch -M main`, `git remote add origin <your repo URL>`, `git push -u origin main`.
   - Without Git: on the repo page, click **Add file**, then **Upload files**, and drag in the contents of this folder. Check afterwards that `.github/workflows/build-apk.yml` made it up, because some file pickers skip hidden folders. If it's missing, use **Add file**, then **Create new file**, name it `.github/workflows/build-apk.yml`, and paste the contents in.
3. Open the repo's **Actions** tab. The "Build Android APK" workflow starts by itself on every push to `main`, and you can also run it by hand with **Run workflow**. A build takes about 5 to 8 minutes.
4. When it's green, open the repo's **Releases**, on the right of the main repo page. Each build publishes a release with a file like `FlightWeather-1.0.3.apk`.

## Install on your phone

1. On your Android phone, open the release page in Chrome and tap the `.apk` file to download it. If the repo is private, sign in to GitHub in Chrome first.
2. Open the download. Android asks you to allow installs from this source (Chrome) the first time. Allow it, go back, and tap **Install**.
3. Google Play Protect may warn that it doesn't recognize the app. Choose **More details**, then **Install anyway**. That happens because the app didn't come from the Play Store.

## Updating

Push any change to `main`, wait for the new release, and install the new APK over the old one. Your saved crosswind limit and last search are kept.

Updates only install over the old app because every build is signed with the same key, `signing/debug.keystore`. Keep that file in the repo. If it's lost or replaced, uninstall the app before installing a new build.

## What's in here

- `www/index.html` is the app itself. In the app it calls aviationweather.gov directly through Android's own networking, so there's no helper script.
- `www/vendor/` holds React, Recharts and htm bundled locally, so the app doesn't rely on a CDN.
- `assets/` holds the bluebird icon and splash screen. Replace these PNGs to change them.
- `capacitor.config.json` holds the app's name, ID and native settings.
- `.github/workflows/build-apk.yml` is the build recipe GitHub runs.
- `signing/debug.keystore` is the fixed key that signs every build.

For planning only. This is not an official weather briefing. Get a standard briefing from 1800wxbrief.com or call 1-800-WX-BRIEF before you fly.

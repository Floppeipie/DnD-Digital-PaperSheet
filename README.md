# D&D 5e Character Sheet: Android app

Your `index.html` character sheet (in `www/`) wrapped as an Android app with Capacitor.

## Get the APK without installing anything (GitHub Actions)

1. Create a new repository on GitHub and push this folder to it (the branch must be `main` or `master`).
2. Open the repository's **Actions** tab. The **Build APK** workflow runs on every push; you can also start it with **Run workflow**.
3. When it finishes (a few minutes), open the run and download the **dnd-character-sheet-apk** artifact. It is a zip containing `app-debug.apk`.
4. Copy `app-debug.apk` to your phone and open it. Android will ask you to allow installing from that source the first time.

## Build it yourself

Needs Node 22+, JDK 21 and the Android SDK (Android Studio installs the SDK).

```
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```

The APK ends up in `android/app/build/outputs/apk/debug/app-debug.apk`. To open the project in Android Studio instead, run `npx cap open android`.

## Notes

- This is a debug build: fine for installing on your own phone, not for the Play Store. A Play Store release needs a signed `.aab` (`./gradlew bundleRelease` plus a signing key).
- App name and ID are in `capacitor.config.json`. Change `appId` before publishing anywhere.
- After editing `www/index.html`, run `npx cap sync android` (or push, if you use the workflow) and rebuild.
- Characters are stored in the app's local storage on the phone. Uninstalling the app or clearing its data deletes them, so use **Export** now and then. In the app, Export opens the Android share sheet (save to Files or Drive, or send it to yourself), and Import picks that `.json` file again.
- The Alegreya heading font loads from Google Fonts when the phone is online and falls back to a system serif font offline.

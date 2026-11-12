# Capacitor Android CI fix

The previous package.json had empty dependencies and devDependencies. Therefore `npx cap` had no local Capacitor CLI executable, producing `npm error could not determine executable to run`.

## GitHub Actions

The included `.github/workflows/android.yml` installs the local Capacitor packages before invoking the CLI, uses Node 22 and Java 21, adds Android, syncs the `www/` web assets, builds a debug APK, and uploads it as an artifact.

## Local commands

```bash
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```

If `android/` already exists, do not run `npx cap add android` again; run `npx cap sync android` instead.

The app's web assets are in `www/`, matching `webDir` in `capacitor.config.json`.

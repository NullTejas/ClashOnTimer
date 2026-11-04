# Upload ClashOnTimer to GitHub from an Android phone

Repository: https://github.com/NullTejas/ClashOnTimer

## Important: upload the extracted project files, not this ZIP as a single file

1. Download and extract `ClashOnTimer_Android_Project.zip` on your phone.
2. Open the repository in Chrome: https://github.com/NullTejas/ClashOnTimer
3. Make sure the branch selector shows `main`.
4. Choose **Add file → Upload files**.
5. Select all files and folders inside the extracted project folder. Include hidden folders, especially `.github/workflows`.
6. Keep the folder structure unchanged. At the repository root you should see:
   - `settings.gradle.kts`
   - `build.gradle.kts`
   - `gradle.properties`
   - `app/`
   - `.github/workflows/android-apk.yml`
   - `README.md`
7. Scroll down and commit the upload to `main`.

If the mobile browser does not let you select the hidden `.github` folder, the APK workflow will not be uploaded. In that case, create `.github/workflows/android-apk.yml` in GitHub using the exact contents of that file from this ZIP, or use GitHub's desktop-site mode.

## Start the APK build

1. Open the repository's **Actions** tab.
2. Select **Build Clash Tracker APK**.
3. Tap **Run workflow**, choose `main`, and confirm.
4. Wait for a successful green check.
5. Open the completed run and download the artifact named `clash-tracker-debug-apk`.
6. Extract the artifact ZIP; it contains `app-debug.apk`.
7. Open the APK on your phone and approve installation if Android asks.

## What is in this project

This is an early Android/Kotlin starter with a dark Compose dashboard, JSON import/parser foundation, local snapshot data layer, and schema notes for both Clash of Clans villages.

One Clash of Clans JSON export contains both villages. Import it once: unsuffixed collections are Home Village data and corresponding `*2` collections are Builder Base data.

## Current limitations — please read

This is not yet a complete production app. Accurate live upgrade countdowns, builder/lab availability scheduling, verified potion/helper calculations, full game-data labels, and end-to-end testing are not complete. The workflow has been authored but has not yet been run. The first successful GitHub Actions build is the compile check.

The workflow creates a debug APK for personal testing, not a Play Store release.

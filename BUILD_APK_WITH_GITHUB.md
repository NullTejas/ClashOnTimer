# Build an APK from a phone using GitHub Actions

This project includes `.github/workflows/android-apk.yml`. GitHub's cloud runner builds
a debug APK; Android Studio is not needed on your phone.

## Important
- A GitHub account is required.
- Keep the repository **Private** unless you explicitly want the source code public.
- The current project contains no Supercell API key or signing key.
- This produces a debug APK for personal testing, not a Play Store release.
- GitHub Actions usage is subject to the account's current plan and quota.

## Steps
1. Sign in at https://github.com/ in your phone browser.
2. Create a new repository. Choose **Private** and name it `ClashTracker`.
3. Upload the contents of this project (not just the ZIP file) to the repository, preserving folder paths.
4. Open the repository's **Actions** tab.
5. If GitHub asks, enable Actions for the repository.
6. Select **Build Clash Tracker APK** on the left.
7. Press **Run workflow** and choose `main`.
8. Wait for the run to finish with a green check.
9. Open the successful workflow run. Under **Artifacts**, download `clash-tracker-debug-apk`.
10. Extract the downloaded artifact ZIP. It contains `app-debug.apk`.
11. Open the APK on your Android phone and allow installation from that source if Android asks.

## If uploading folders from Android is difficult
The GitHub mobile website may make it awkward to upload a complete folder tree. You can use a browser-based Codespace (if available on your account) to upload the project ZIP, unzip it in the Codespace terminal, and push the extracted files. Alternatively, connect the GitHub integration in ChatGPT so repository operations can be assisted where supported.

## Build details
- Java 17
- Android Gradle Plugin 8.7.3
- Gradle 8.9
- Android SDK 35
- Compose compiler plugin for Kotlin 2.0.21
- Task: `:app:assembleDebug`

The workflow has been authored but has not yet been run in your GitHub account. The first cloud build is the actual compile check.

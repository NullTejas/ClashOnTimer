# Clash Tracker — Phase 1 starter

Android/Kotlin starter for a private, local-first Clash of Clans village tracker.

## Phase 1 included
- Premium dark dashboard foundation
- Home Village / Builder Base selector
- Multiple account nicknames
- Clipboard JSON paste and manual JSON input
- JSON validation and root-field inspection
- Local Room database storing separate snapshots
- Snapshot deletion

## Important current limitation
This first build intentionally stores the raw export and inspects its top-level keys. It does **not** yet decode individual building/research timers. The exact in-game export schema must be mapped against a real, redacted export before we implement typed upgrade models. Do not infer field names from sample data found online.

## Build
1. Install Android Studio (current stable) and Android SDK 35.
2. Open this folder as an existing Gradle project.
3. Use JDK 17.
4. Let Gradle sync, then Run the `app` configuration on an Android device/emulator.

## Test import
In Clash of Clans: Settings → More Settings → Data Export → Copy.
In this app: SYNC → enter an account nickname → select the village → Paste from Clipboard → Validate & Save.

The app does not request Internet permission and does not connect to Supercell in Phase 1. The JSON remains in the local Room database.

## Next required input
Provide one sample Home Village export and one Builder Base export. Redact the player tag/name if desired, but preserve the JSON structure and timer values. We will use these to build a versioned parser and typed models.

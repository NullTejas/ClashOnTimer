# Phase 2 schema map — based on the supplied Home Village export

## Root fields
- `tag`: player tag string.
- `timestamp`: Unix epoch seconds. Supplied sample converts to 2026-11-04 20:10:56 at UTC+05:30.
- `helpers[]`: helper object IDs, levels, optional `helper_cooldown`.
- `boosts.builder_boost`, `boosts.lab_boost`: numeric timer-like values, retained as seconds pending validation of exact semantics.

## Repeated object records
Common fields:
- `data`: numeric game-data ID. Not a human-readable name.
- `lvl`: level, where present.
- `cnt`: quantity represented by a grouped record, where present.
- `timer`: timer-like value in seconds, where present.
- Other properties (e.g. `supercharge`, `gear_up`, `extra`, `helper_recurrent`, `modules`, `types`) must be preserved as flags/metadata.

## Category mapping
- Home Village: `buildings`, `traps`, `units`, `siege_machines`, `heroes`, `spells`, `pets`, `equipment`, `guardians`.
- Builder Base: `buildings2`, `traps2`, `units2`, `heroes2`.
- Other collections: `decos`, `obstacles`, `decos2`, `obstacles2`, `house_parts`, `skins`, `sceneries`, `skins2`, `sceneries2`.

## Timer-bearing entries in this sample
All timer values below are raw seconds converted to d/h/m/s:
- buildings 1000003 lvl 18: 399286 = 4d 14h 54m 46s
- buildings 1000005 lvl 18: 399283 = 4d 14h 54m 43s
- buildings 1000003 lvl 18: 400280 = 4d 15h 11m 20s
- buildings 1000005 lvl 18: 399284 = 4d 14h 54m 44s
- units 4000123 lvl 4: 275633 = 3d 04h 33m 53s; `helper_recurrent=true`
- heroes 28000001 lvl 97: 233674 = 2d 16h 54m 34s
- heroes 28000007 lvl 21: 204841 = 2d 08h 54m 01s; `helper_recurrent=true`
- spells 26000000 lvl 12: 395779 = 4d 13h 56m 19s; `extra=true`
- pets 73000008 lvl 14: 15081 = 04h 11m 21s

## Helpers and boosts
- Helper cooldown values present: 64622 = 17h 57m 02s.
- `boosts.builder_boost`: 9092 = 02h 31m 32s.
- `boosts.lab_boost`: 2575 = 00h 42m 55s.

These names strongly suggest cooldown/boost durations, but their exact meaning (remaining duration vs another timer convention, activation semantics, overlap behavior) must be validated against a live game state before calculating authoritative ETAs.

## Important timestamp observation
The sample timestamp is 2026-11-04 20:10:56 at UTC+05:30. The conversation's approximate current local time was around 20:00, so this export timestamp appears about 10m56s in the future relative to that estimate. Verify device clock/timezone and capture a fresh export before relying on timestamp-based countdowns.

## Parser design rules
1. Preserve raw JSON for forward compatibility.
2. Treat `data` as an ID and resolve names only via a versioned game-data catalogue.
3. Do not treat `cnt` as an active upgrade count.
4. A record with `timer` is a timer-bearing candidate, but validate its category semantics before labelling it an upgrade.
5. Preserve unknown flags and unknown root fields.
6. Do not assume a missing timer means the object is idle until confirmed for each category.
7. Store snapshot timestamp and raw timer together; derive ETA only after validating timer units and reference time.

## Corrected village and timestamp interpretation
The supplied export is a combined account snapshot containing both villages.
Do not request a separate Builder Base export. Import once, then route `*2`
collections to the Builder Base view and unsuffixed village collections to
the Home Village view. The root `timestamp` is a Unix epoch timestamp and is
not tied to the exporting player's time zone. Store the instant and render it
using the viewing device's local time zone.

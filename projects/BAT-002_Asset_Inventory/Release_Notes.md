# BAT-002 Release Notes

## v0.2 Backup and Presence Automation Update — July 13, 2026

- Added Alfred as the Home Assistant backup target.
- Documented daily automatic backups to `AlfredBackups` with 20-day retention.
- Added backup failure, stale-backup, and weekly success-summary notification automation exports.
- Updated Terry away-cleaning logic to use Dustin/Kaylie person entities with a 15-minute away window.
- Kept `binary_sensor.home_occupied` as the babysitter/guest safety guard for Terry.
- Removed vacation mode as a blocker for Terry cleaning.
- Added Kaylie location reliability and Home Occupied template review notes.

## v0.1 Draft
Initial asset inventory generated from known BATCAVE information.

## Dustin Review Checklist
- Confirm Eero satellite location
- Confirm camera names and locations
- Confirm Govee sensor locations
- Confirm smart switch models and entity names
- Confirm whether Babysitter Mode and House Occupied are active or planned
- Add missing devices

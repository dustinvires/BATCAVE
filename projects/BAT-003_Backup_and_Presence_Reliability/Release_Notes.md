# BAT-003 Release Notes

## v0.1 Implemented — July 13, 2026

### Added

- Configured Alfred as Home Assistant network backup storage.
- Created `\\ALFRED\HomeAssistantBackups` SMB share.
- Set Alfred Ethernet IP to static `192.168.4.96`.
- Configured Home Assistant daily automatic backups to `hassio.AlfredBackups`.
- Set Home Assistant backup retention to 20 days.
- Added Alfred-side scheduled cleanup task for backup files older than 20 days.
- Created a restore playbook for Home Assistant disaster recovery.
- Added backup failure notification to Dustin’s iPhone.
- Added daily stale-backup health check.
- Added weekly Sunday success-summary notification.
- Updated Terry Working automation to use person entities and a 15-minute away window.
- Kept `home_occupied` as a safety guard for babysitter/guest scenarios.
- Removed vacation mode as a blocker for Terry cleaning.

### Verified

- Test backup completed successfully to Alfred.
- Backup file visible in `\\ALFRED\HomeAssistantBackups`.
- Home Assistant mount `AlfredBackups` is active.
- Backup notification automations are enabled.
- Terry Working automation is enabled with revised logic.

### Still observing

- Kaylie mobile app location update reliability.
- Whether `binary_sensor.home_occupied` blocks Terry unexpectedly after the new automation logic.
- Tomorrow’s first fully unattended scheduled backup to Alfred.

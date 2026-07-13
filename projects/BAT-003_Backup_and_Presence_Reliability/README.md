# BAT-003: Backup and Presence Reliability

## Objective

Make BATCAVE safer and more resilient by adding reliable Home Assistant backups to Alfred, backup health notifications, and improved presence-based Terry cleaning behavior.

## Status

Implemented / observation phase — July 13, 2026

## What was built

### Home Assistant backups to Alfred

- Alfred configured as the backup target for Home Assistant.
- Alfred static IP: `192.168.4.96`.
- SMB share: `\\ALFRED\HomeAssistantBackups`.
- Home Assistant backup mount: `AlfredBackups`.
- Backup agent: `hassio.AlfredBackups`.
- Automatic backups: daily.
- Retention: 20 days.
- Test backup verified on Alfred.

### Backup monitoring

- Failure alert sends to `notify.dustins_iphone` and creates a persistent Home Assistant notification.
- Daily stale-backup health check creates a persistent notification if the last successful backup is older than 36 hours.
- Weekly Sunday evening success summary sends to `notify.dustins_iphone` when backups are healthy.

### Terry presence cleaning

- Terry now uses `person.dustin` and `person.kaylie` instead of raw device trackers.
- Terry starts only after both people have been away for 15 minutes.
- `binary_sensor.home_occupied` is retained as a safety guard for babysitter/guest scenarios.
- Vacation mode no longer blocks Terry cleaning.

## Current state

- Backups are configured and verified.
- Notification automations are enabled.
- Terry automation is updated and enabled.
- Kaylie location reliability remains under observation.
- `binary_sensor.home_occupied` may need template review if it continues to block Terry unexpectedly.

## Related documentation

- `../../docs/technical_manual/Home_Assistant_Backups.md`
- `../../docs/technical_manual/Presence_Automations.md`
- `../../home_assistant/automations/home_assistant_backup_to_alfred_notifications.yaml`
- `../../home_assistant/automations/terry_working_presence_cleaning.yaml`

## Next verification steps

1. Confirm tomorrow morning’s scheduled backup lands on Alfred automatically.
2. Confirm Home Assistant lists the Alfred backup under Backups.
3. Observe Terry’s next away-cleaning event after both Dustin and Kaylie leave.
4. If Terry still does not run, inspect whether `binary_sensor.home_occupied` is blocking it.
5. If Kaylie location remains delayed, add a stale-location diagnostic notification.

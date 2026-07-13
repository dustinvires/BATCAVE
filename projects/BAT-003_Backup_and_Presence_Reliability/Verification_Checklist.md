# BAT-003 Verification Checklist

## Backup verification

- [x] Alfred SMB share exists: `\\ALFRED\HomeAssistantBackups`.
- [x] Alfred has static IP `192.168.4.96`.
- [x] Home Assistant network storage `AlfredBackups` is active.
- [x] Home Assistant automatic backups target `hassio.AlfredBackups`.
- [x] Manual/test automatic backup completed to Alfred.
- [x] Backup share contains a real `.tar` backup file.
- [ ] Confirm next unattended scheduled backup appears on Alfred.
- [ ] Confirm weekly success notification sends on Sunday evening.

## Restore verification

- [x] Restore playbook created.
- [ ] Confirm Home Assistant backup UI can see the Alfred backup.
- [ ] Optional: perform non-destructive restore readiness review.

## Presence / Terry verification

- [x] Terry Working automation updated to use `person.dustin` and `person.kaylie`.
- [x] Terry Working uses 15-minute away window.
- [x] Vacation mode no longer blocks Terry cleaning.
- [x] `binary_sensor.home_occupied` retained as guest/babysitter safety guard.
- [ ] Observe next real away event and verify Terry starts only when appropriate.
- [ ] If Terry does not start, inspect automation trace and `home_occupied` state.
- [ ] If Kaylie location remains stale, add stale-location diagnostic alert.

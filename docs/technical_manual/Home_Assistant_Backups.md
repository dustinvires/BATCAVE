# Home Assistant Backups to Alfred

Last updated: Monday, July 13, 2026 at 1:33 PM CDT

## Purpose

Home Assistant on the Raspberry Pi 5 stores daily automatic backups on Alfred so the system can be restored from an off-device backup if the Raspberry Pi or Home Assistant install fails.

## Current backup architecture

```mermaid
graph LR
    HA[Home Assistant OS\nRaspberry Pi 5] -->|Daily automatic backup| Mount[AlfredBackups\nHome Assistant backup mount]
    Mount --> Share[\\\\ALFRED\\HomeAssistantBackups]
    Share --> Folder[C:\\HomeAssistantBackups\non Alfred]
    Cleanup[Alfred scheduled task\n20-day cleanup] --> Folder
```

## Network and storage details

- Alfred hostname: `ALFRED`
- Alfred static IP: `192.168.4.96`
- SMB share: `\\ALFRED\HomeAssistantBackups`
- Alfred local folder: `C:\HomeAssistantBackups`
- Home Assistant network storage name: `AlfredBackups`
- Home Assistant backup agent: `hassio.AlfredBackups`
- Home Assistant mount state verified: `active`

## Backup schedule and retention

- Home Assistant automatic backups: enabled
- Schedule: daily
- Backup target: `hassio.AlfredBackups`
- Home Assistant retention: 20 days
- Alfred-side cleanup task: `Home Assistant Backup Retention - 20 Days`
- Alfred cleanup schedule: daily at 3:15 AM

## Verified backup

A test backup was generated and verified on Alfred on July 13, 2026:

```text
Automatic_backup_2026.7.1_2026-07-13_13.09_18499183.tar
```

Approximate size: 590 MB.

## Monitoring and notifications

Home Assistant automations monitor the backup workflow:

1. **Home Assistant Backup to Alfred - Failure Alert**
   - Sends `notify.dustins_iphone` notification if automatic backup reports a failed event.
   - Also creates a persistent notification in Home Assistant.

2. **Home Assistant Backup to Alfred - Daily Health Check**
   - Runs daily at 7:00 AM.
   - Creates a persistent notification if the last successful automatic backup is missing or older than 36 hours.

3. **Home Assistant Backup to Alfred - Weekly Success Summary**
   - Runs Sundays at 6:00 PM.
   - Sends `notify.dustins_iphone` a weekly success summary when backups are healthy.

Automation YAML exports are stored in:

- `home_assistant/automations/home_assistant_backup_to_alfred_notifications.yaml`

## Restore process

### Routine restore while Home Assistant is running

1. Open Home Assistant.
2. Go to **Settings → System → Backups**.
3. Select a backup stored on `AlfredBackups`.
4. Choose full restore or partial restore.
5. Follow Home Assistant prompts and let it reboot if required.

### Disaster recovery / fresh Raspberry Pi restore

1. Install Home Assistant OS fresh on the Raspberry Pi.
2. During onboarding, choose restore from backup if offered.
3. Use one of these approaches:
   - Upload a backup `.tar` from `C:\HomeAssistantBackups`, or
   - Finish onboarding, then add network storage:
     - Type: Samba/Windows/CIFS
     - Usage: Backup
     - Name: `AlfredBackups`
     - Server: `192.168.4.96`
     - Share: `HomeAssistantBackups`
     - Username: `ha-backup`
4. Select the desired backup and restore.
5. Wait for Home Assistant to complete restore and reboot.

## Alfred admin helper

Alfred has a scheduled task named `Craft Agent Admin Helper` that runs queued admin jobs as `NT AUTHORITY\SYSTEM` from:

- Queue: `C:\CraftAgentAdminTasks\queue`
- Logs: `C:\CraftAgentAdminLogs`

This was used to configure/verify the SMB share, static IP, scheduled cleanup, and logs without repeated UAC prompts.

## Security notes

- The backup SMB user is dedicated to Home Assistant backup access.
- The backup share should contain backup `.tar` files only.
- Setup artifacts were moved out of the backup share and archived under `C:\CraftAgentAdminLogs\ha-backup-setup-artifacts`.
- Plaintext password artifacts from setup scripts were redacted after setup.

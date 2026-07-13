# 🦇 BATCAVE

## Mission
BATCAVE is the engineering repository for the Vires family home. It serves as the source of truth for Home Assistant, ESPHome, infrastructure documentation, engineering decisions, and future projects.

## Principles
- Reliability over novelty
- Local-first whenever practical
- Design before implementation
- Document everything
- Every automation has a purpose

## Current Build Status

BATCAVE is currently in **BAT-003: Backup and Presence Reliability**.

### Completed

- ✅ Home Assistant core environment documented
- ✅ HACS / Tailscale / Reolink / ESPHome documented
- ✅ Shark vacuum “Terry” integrated
- ✅ Alfred configured as Home Assistant backup target
- ✅ Daily Home Assistant backups to Alfred configured
- ✅ 20-day backup retention configured
- ✅ Backup failure and weekly success notifications configured
- ✅ Terry away-cleaning automation revised for person-based presence

### In observation / validation

- 🚧 First fully unattended scheduled backup to Alfred
- 🚧 Terry’s next real away-cleaning event
- 🚧 Kaylie location update reliability
- 🚧 `binary_sensor.home_occupied` behavior as Terry safety guard
- 🚧 B-hyve BLE status reliability

### Future / planned

- 📋 Water Protection
- 📋 Energy Monitoring
- 📋 Crawl Space Monitoring expansion
- 📋 Network/UPS/infrastructure watchdogs

## Project Iterations

- `projects/BAT-002_Asset_Inventory/` — baseline BATCAVE asset inventory and system map.
- `projects/BAT-003_Backup_and_Presence_Reliability/` — current stage: Home Assistant backups to Alfred, restore readiness, backup notifications, and Terry presence automation reliability.

## Key Documentation

- `docs/technical_manual/Home_Assistant_Backups.md` — daily Home Assistant backups to Alfred, restore path, retention, and monitoring.
- `docs/technical_manual/Presence_Automations.md` — Terry presence-based cleaning automation and Kaylie location reliability notes.
- `home_assistant/automations/home_assistant_backup_to_alfred_notifications.yaml` — backup failure, stale-backup, and weekly success notifications.
- `home_assistant/automations/terry_working_presence_cleaning.yaml` — current Terry away-cleaning automation export.

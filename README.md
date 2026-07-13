# 🦇 BATCAVE

## Mission
BATCAVE is the engineering repository for the Vires family home. It serves as the source of truth for Home Assistant, ESPHome, infrastructure documentation, engineering decisions, and future projects.

## Principles
- Reliability over novelty
- Local-first whenever practical
- Design before implementation
- Document everything
- Every automation has a purpose

## Current Status
- ✅ Home Assistant
- ✅ HACS
- ✅ Tailscale
- ✅ Reolink Cameras
- ✅ Shark Vacuum
- ✅ ESPHome
- ✅ Home Assistant backups to Alfred
- ✅ Backup failure/success notifications
- 🚧 Presence-based Terry cleaning reliability
- 🚧 Crawl Space Monitoring
- 🚧 B-hyve BLE
- 📋 Water Protection
- 📋 Energy Monitoring

## Key Documentation

- `docs/technical_manual/Home_Assistant_Backups.md` — daily Home Assistant backups to Alfred, restore path, retention, and monitoring.
- `docs/technical_manual/Presence_Automations.md` — Terry presence-based cleaning automation and Kaylie location reliability notes.
- `home_assistant/automations/home_assistant_backup_to_alfred_notifications.yaml` — backup failure, stale-backup, and weekly success notifications.
- `home_assistant/automations/terry_working_presence_cleaning.yaml` — current Terry away-cleaning automation export.
- `projects/BAT-002_Asset_Inventory/` — current BATCAVE system inventory, stage notes, known issues, and release notes.

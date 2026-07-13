# BAT-002: Asset Inventory

## Objective
Create the first engineering inventory of BATCAVE.

## Status
Draft v0.2 — backup and presence automation updates added July 13, 2026

## Purpose
This project establishes the baseline list of infrastructure, devices, integrations, systems, known issues, and future projects currently known in the Vires home.

## Review Needed
Dustin should review locations, names, models, IPs, missing devices, and statuses.

## Related Documentation

### Dashboards

- `../../home_assistant/dashboards/batcave-operations-center.yaml` — live BATCAVE Operations Center dashboard source of truth.
- `../../home_assistant/dashboards/batcave-operations-center.backup-2026-07-13.yaml` — pre-expansion dashboard backup for rollback.
- `../../home_assistant/dashboards/batcave-command-center.yaml` — initial generated dashboard draft/reference.
- `../../home_assistant/dashboards/README.md` — dashboard folder notes and deployment workflow.
- `../../docs/owner_manual/BATCAVE_Command_Center.md` — owner-facing dashboard guide.
- `../../docs/technical_manual/Home_Assistant_Dashboards.md` — technical dashboard documentation and maintenance rules.

### Backups and Presence Automations

- `../../docs/technical_manual/Home_Assistant_Backups.md` — Home Assistant daily backups to Alfred, retention, restore steps, and monitoring.
- `../../docs/technical_manual/Presence_Automations.md` — Terry away-cleaning logic and Kaylie location reliability notes.
- `../../home_assistant/automations/home_assistant_backup_to_alfred_notifications.yaml` — backup notification automation export.
- `../../home_assistant/automations/terry_working_presence_cleaning.yaml` — Terry presence-cleaning automation export.

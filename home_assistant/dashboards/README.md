# Home Assistant Dashboards

This folder contains YAML dashboards for BATCAVE.

## Dashboards

### `batcave-operations-center.yaml`

**Live Home Assistant dashboard.** This file represents the BATCAVE Operations Center dashboard that was edited through the Home Assistant raw configuration editor on 2026-07-13.

It preserves the existing Home Assistant dashboard structure and tabs Dustin had already created:

- Overview
- Infrastructure
- Security
- Environment
- Utilities
- Automations
- Engineering

### `batcave-operations-center.backup-2026-07-13.yaml`

Backup of the BATCAVE Operations Center raw dashboard YAML before the 2026-07-13 dashboard expansion.

Keep this file as a rollback reference until the updated dashboard has been reviewed over time.

### `batcave-command-center.yaml`

Initial generated dashboard draft built from live Home Assistant entities. This is retained as a design/reference artifact, but the active dashboard is now `batcave-operations-center.yaml`.

Design goals:
- Safe
- Reliable
- Comfortable
- Efficient
- Maintainable
- Understandable
- Native Home Assistant cards first; no HACS dependency required for v1

Live Operations Center views included:
- **Overview** — mission, house modes, weather, thermostat, comfort snapshot, security snapshot, Terry, updates
- **Infrastructure** — Home Assistant, Raspberry Pi, eero WAN, backups, updates, ESPHome/sump ESP
- **Security** — front camera, Malachi room camera, detection entities, camera status
- **Environment** — thermostat, Henry humidifier, room temperature/humidity, trends
- **Utilities** — B-hyve BLE status, water-protection roadmap, Terry vacuum controls/status
- **Automations** — mode, presence, lighting/comfort, and Terry automations
- **Engineering** — GitHub/repository links, active work, documentation references, health helpers

## Related Documentation

- `docs/owner_manual/BATCAVE_Command_Center.md` — owner-facing guide for what each view is for.
- `docs/technical_manual/Home_Assistant_Dashboards.md` — technical design, maintenance rules, installation notes, and future roadmap.

## Current install approach

The live dashboard currently exists in Home Assistant's dashboard storage and was updated through:

```text
BATCAVE Operations Center → Edit dashboard → Raw configuration editor
```

The repository copy of `batcave-operations-center.yaml` is the documented source of truth for the live dashboard configuration.

Until a Git/file-based deployment path is installed, changes should be applied in this order:

1. Edit/commit the YAML in this repository.
2. Copy the YAML into the Home Assistant raw configuration editor.
3. Save in Home Assistant.
4. Verify the rendered dashboard.
5. Commit any final changes and documentation updates together.

## Safety note

The first dashboard intentionally avoids broad destructive controls. Water, lock, siren, alarm, and system restart style actions should be added only after explicit review.

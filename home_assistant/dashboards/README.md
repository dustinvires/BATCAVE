# Home Assistant Dashboards

This folder contains YAML dashboards for BATCAVE.

## Dashboards

### `batcave-command-center.yaml`

Primary family-facing dashboard built from live Home Assistant entities.

Design goals:
- Safe
- Reliable
- Comfortable
- Efficient
- Maintainable
- Understandable
- Native Home Assistant cards first; no HACS dependency required for v1

Views included:
- **Overview** — house modes, weather, thermostat, camera snapshots, Terry, updates
- **Security** — Reolink/Ring camera views and detection status
- **Climate** — Nest thermostat, room sensors, humidity, Henry humidifier
- **Infrastructure** — Home Assistant, Raspberry Pi, eero WAN, backups, updates, ESPHome
- **Water** — B-hyve BLE, sump ESP, future water-protection roadmap
- **Robotics** — Terry vacuum status, room clean buttons, automations

## Related Documentation

- `docs/owner_manual/BATCAVE_Command_Center.md` — owner-facing guide for what each view is for.
- `docs/technical_manual/Home_Assistant_Dashboards.md` — technical design, maintenance rules, installation notes, and future roadmap.

## Current install approach

This dashboard is written as Lovelace YAML. To use it in Home Assistant, either:

1. Copy/import the YAML into a dashboard configured in YAML mode, or
2. Use it as a source template while recreating cards in the Home Assistant UI.

If using YAML dashboards from `configuration.yaml`, the shape is typically:

```yaml
lovelace:
  mode: yaml
  dashboards:
    batcave-command-center:
      mode: yaml
      title: BATCAVE Command Center
      icon: mdi:bat
      show_in_sidebar: true
      filename: dashboards/batcave-command-center.yaml
```

Exact file placement depends on the live Home Assistant config directory layout. This repository copy is the documented source of truth.

## Safety note

The first dashboard intentionally avoids broad destructive controls. Water, lock, siren, alarm, and system restart style actions should be added only after explicit review.

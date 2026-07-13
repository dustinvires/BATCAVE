# Home Assistant Dashboards

## Purpose

BATCAVE dashboards are the human-facing control and observability layer for the Vires home.

They should make the home easier to understand, safer to operate, and faster to troubleshoot. Dashboards are not just visual decoration; they are part of the operating manual for the house.

## Design Principles

Dashboards must follow the BATCAVE philosophy:

- **Safety first** — avoid accidental destructive controls.
- **Reliability over novelty** — prefer stable native Home Assistant cards before custom cards.
- **Local-first whenever practical** — dashboards should continue to function as much as possible without cloud dependencies.
- **Understandability** — entities should be grouped by real household system, not random integration names.
- **Documentation is part of installation** — every dashboard file should have enough documentation for future maintenance.

## Current Dashboard Files

| File | Purpose |
|---|---|
| `home_assistant/dashboards/batcave-operations-center.yaml` | **Live dashboard source of truth** for the BATCAVE Operations Center currently installed in Home Assistant dashboard storage. |
| `home_assistant/dashboards/batcave-operations-center.backup-2026-07-13.yaml` | Backup of the Operations Center before the 2026-07-13 expansion. |
| `home_assistant/dashboards/batcave-command-center.yaml` | Initial generated dashboard draft retained as a reference artifact. |
| `home_assistant/dashboards/README.md` | Dashboard folder usage notes and installation guidance. |

## Live Dashboard: BATCAVE Operations Center

The BATCAVE Operations Center is the active Home Assistant dashboard. It was updated on 2026-07-13 through the Home Assistant raw configuration editor while preserving Dustin's existing dashboard and tab structure.

Home Assistant path:

```text
/batcave-operations-center/overview
```

Update method used:

```text
BATCAVE Operations Center → Edit dashboard → Raw configuration editor
```

## Views

### Overview

Family-facing summary view.

Includes:

- BATCAVE mission and operating principles
- Vacation Mode
- Babysitter Mode
- Home Occupied
- House Healthy
- Infrastructure Healthy
- Weather forecast
- Dining Room thermostat
- Comfort snapshot
- Security snapshot
- Terry status
- Important updates

### Infrastructure

Reliability and maintenance view.

Includes:

- Infrastructure Healthy helper
- eero WAN status
- External IP
- Raspberry Pi power status
- Processor usage
- Memory usage
- Processor temperature
- Backup manager state
- Last/next backup timestamps
- Sump ESP / Bluetooth proxy diagnostics
- Update entities

### Security

Camera and detection view.

Includes:

- One live-friendly stream per physical camera
- Front Reolink using the `fluent` stream for lower-latency viewing
- Front Door Ring live view as a separate doorbell camera
- Front motion/person/vehicle/animal detection
- Doorbell/motion events
- Front camera activity
- Malachi room camera using the `fluent` stream for lower-latency viewing
- Malachi room motion/person/animal/baby-cry detection
- Malachi room privacy/recording status

### Environment

Comfort and humidity view.

Includes:

- Dining Room thermostat
- Henry humidifier
- Dining Room temperature/humidity
- Master temperature/humidity
- Malachi Bedroom temperature/humidity
- Garage temperature/humidity
- 24-hour temperature trend
- 24-hour humidity trend
- Henry low-water/tank-lifted/mist-level status

### Utilities

Utility systems and robotics view.

Includes:

- B-hyve BLE battery/status information
- Water-protection roadmap
- Terry robot vacuum status
- Terry battery/charging/error/Wi-Fi
- Terry clean mode
- Terry room clean buttons

B-hyve control/status design, added 2026-07-13:

- `switch.bhyve_ble_44_67_55_86_26_9d_port_1` is displayed as **Outdoor Spigot**. Treat this as the command/control surface for the single B-hyve hose timer.
- `sensor.outside_bhyve_ble_44_67_55_86_26_9d_port_1_status` is displayed as **Spigot Status**. Treat this as the preferred status/truth source.
- `number.outside_bhyve_ble_44_67_55_86_26_9d_port_1_run_time` is displayed as **Watering Duration**.
- The output-port count is intentionally hidden because this installation uses a single-output B-hyve device.

This distinction is intentional because the older integration previously showed the switch as `on` even when the physical hose timer was not watering. After updating Orbit B-hyve BLE from `v0.0.8` to `v0.1.0`, the status sensor should be used for displayed state. The older `sensor.bhyve_ble_44_67_55_86_26_9d_last_message_type` may be restored/unavailable and should not be used as the primary dashboard status.

### Automations

Automation visibility view.

Includes:

- Vacation Mode automations
- Kaylie presence automations
- Humidity alert automation
- Automatic Dining Room light automation
- Terry automations

### Engineering

Repository and documentation view.

Includes:

- GitHub repository link
- Active BATCAVE work
- Completed BAT projects
- Dashboard documentation references
- House/infrastructure health helpers

## Source of Truth

The repository copy is the documented source of truth:

```text
home_assistant/dashboards/batcave-operations-center.yaml
```

The live Home Assistant dashboard currently exists in Home Assistant dashboard storage. Until a Git/file-based deployment path is installed, the repository and live dashboard must be kept synchronized manually through the raw configuration editor.

## Deployment / Update Procedure

Current procedure:

1. Edit `home_assistant/dashboards/batcave-operations-center.yaml` in Git.
2. Commit documentation and YAML together when possible.
3. Open Home Assistant.
4. Open **BATCAVE Operations Center**.
5. Select **Edit dashboard**.
6. Open **Raw configuration editor**.
7. Paste the repository YAML.
8. Save.
9. Exit edit mode.
10. Verify each tab renders.
11. Commit any final changes and push to GitHub.

## Rollback Procedure

If the dashboard breaks after a change:

1. Open the raw configuration editor.
2. Replace the current YAML with the contents of:

```text
home_assistant/dashboards/batcave-operations-center.backup-2026-07-13.yaml
```

3. Save.
4. Verify the dashboard renders.
5. Document what failed before attempting the change again.

## Maintenance Rules

When changing dashboards:

1. Update dashboard YAML.
2. Confirm entity IDs exist in Home Assistant.
3. Avoid destructive controls unless explicitly intended.
4. Update this documentation if views, entities, or design intent change.
5. Commit dashboard and documentation changes together.
6. Keep a dated backup before major raw-editor replacements.

## Future Improvements

Planned dashboard work:

- Create a permanent Git/file-based deployment path into Home Assistant.
- Add a dedicated water-protection dashboard after sump/leak/shutoff entities exist.
- Add an infrastructure dashboard with network topology and unavailable entity reporting.
- Add energy monitoring after CT clamps or another energy monitor are installed.
- Add maintenance reminders for HVAC filters, sump testing, water softener, firmware, UPS, and seasonal hose shutoff.
- Consider HACS cards later only where they materially improve reliability or clarity.

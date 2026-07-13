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
| `home_assistant/dashboards/batcave-command-center.yaml` | Primary BATCAVE family dashboard with overview, security, climate, infrastructure, water, and robotics views. |
| `home_assistant/dashboards/README.md` | Dashboard folder usage notes and installation guidance. |

## BATCAVE Command Center

The BATCAVE Command Center is the first full dashboard generated from live Home Assistant entities.

### Views

#### Overview

Family-facing summary view.

Includes:

- House modes
- Vacation Mode
- Babysitter Mode
- Home Occupied
- House Healthy
- Infrastructure Healthy
- Weather
- Dining Room thermostat
- Key room temperature/humidity readings
- Security snapshot
- Front and Malachi room cameras
- Terry status
- Important updates

#### Security

Camera and detection view.

Includes:

- Front camera views
- Front motion/person/vehicle/animal detection
- Doorbell/motion events
- Front camera recording/notification settings
- Malachi room camera views
- Malachi room motion/person/animal/baby-cry detection
- Malachi room recording/privacy/notification settings

#### Climate

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

#### Infrastructure

Reliability and maintenance view.

Includes:

- Infrastructure Healthy helper
- eero WAN status
- External IP
- Raspberry Pi power status
- Processor usage and temperature
- Memory usage
- Backups
- Sump ESP / Bluetooth proxy diagnostics
- Update entities

#### Water

Early water-protection view.

Includes:

- B-hyve BLE battery/status information
- Sump ESP diagnostics
- Henry low-water/tank-lifted status
- Vacation Mode context
- Future water protection roadmap notes

Intentional safety decision: v1 does **not** expose direct B-hyve port/valve controls. Water controls should be added only after explicit review.

#### Robotics

Terry robot vacuum view.

Includes:

- Terry vacuum status
- Battery
- Charging
- Error state
- Error status
- Wi-Fi signal
- Clean mode
- Room clean buttons
- Terry automations

## Source of Truth

The dashboard source of truth is this repository.

Live Home Assistant entities were read from the Home Assistant API and then captured in the dashboard YAML. If entities are renamed in Home Assistant, this dashboard should be updated in GitHub as part of the change.

## Installation Notes

The dashboard is written as Lovelace YAML.

Potential install methods:

1. Copy/import the YAML into a Home Assistant dashboard.
2. Use it as a source template while recreating cards in the Home Assistant UI.
3. Configure Home Assistant YAML dashboards from `configuration.yaml`.

Example YAML dashboard config:

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

Exact placement depends on the live Home Assistant config directory layout.

## Maintenance Rules

When changing dashboards:

1. Update dashboard YAML.
2. Confirm entity IDs exist in Home Assistant.
3. Avoid destructive controls unless explicitly intended.
4. Update this documentation if views, entities, or design intent change.
5. Commit the dashboard and documentation together.

## Future Improvements

Planned dashboard work:

- Split specialized dashboards out of the Command Center if views become too dense.
- Add a dedicated water-protection dashboard after sump/leak/shutoff entities exist.
- Add an infrastructure dashboard with network topology and unavailable entity reporting.
- Add energy monitoring after CT clamps or another energy monitor are installed.
- Add maintenance reminders for HVAC filters, sump testing, water softener, firmware, UPS, and seasonal hose shutoff.
- Consider HACS cards later only where they materially improve reliability or clarity.

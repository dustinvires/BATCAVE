# BATCAVE Operations Center Owner Guide

## What This Is

The BATCAVE Operations Center is the main Home Assistant dashboard for quickly understanding the state of the home.

It is designed for everyday family awareness and for quick troubleshooting when something does not look right.

## Where It Lives

In Home Assistant:

```text
BATCAVE Operations Center
```

Repository source of truth:

```text
home_assistant/dashboards/batcave-operations-center.yaml
```

Related technical documentation:

```text
docs/technical_manual/Home_Assistant_Dashboards.md
```

## Main Tabs

### Overview

Use this first.

It shows:

- BATCAVE mission
- Vacation Mode
- Babysitter Mode
- Home Occupied
- House Healthy
- Infrastructure Healthy
- Weather
- Dining Room thermostat
- Temperature snapshot
- Security snapshot
- Terry vacuum status
- Important updates

### Infrastructure

Use this when Home Assistant, networking, backups, or the Raspberry Pi might need attention.

It shows:

- Infrastructure Healthy
- eero WAN
- External IP
- Raspberry Pi power
- CPU use
- Memory use
- Pi temperature
- Backup status
- Sump ESP / Bluetooth proxy details
- Update status

### Security

Use this to check camera and detection status.

It shows:

- Front camera views
- Front motion/person/vehicle/animal detection
- Front door events
- Malachi room camera views
- Malachi room detection
- Malachi privacy/recording state

### Environment

Use this to check comfort and humidity.

It shows:

- Dining Room thermostat
- Henry humidifier
- Room temperatures
- Room humidity
- 24-hour temperature trend
- 24-hour humidity trend
- Henry low-water/tank status

### Utilities

Use this to check water-adjacent utilities and Terry.

It shows:

- B-hyve BLE battery/status
- Water-protection roadmap
- Terry status
- Terry battery/error/Wi-Fi
- Terry room clean buttons

### Vehicles

Use this to check Dadvan status and Uconnect data freshness.

It shows:

- Last Dadvan vehicle data timestamp
- Last location update and location map
- Fuel remaining
- Oil life
- Odometer
- Tire pressure gauges and tire warnings
- Uconnect refresh buttons
- Deliberate vehicle controls for doors, remote start, and lights/horn
- Troubleshooting checklist for stale SyncUP/Uconnect data

Use the vehicle controls deliberately. Lock, remote start, horn, and light commands can cause real-world vehicle actions.

### Automations

Use this to verify important automations are present and enabled.

It shows:

- Vacation Mode automations
- Presence automations
- Humidity/lighting automations
- Terry automations

### Engineering

Use this to find BATCAVE repository/documentation references.

It shows:

- GitHub link
- Active work
- Completed BAT projects
- Dashboard documentation references
- Health helpers

## Safety Notes

This version intentionally avoids broad dangerous controls.

Examples of controls that should be reviewed carefully before adding:

- Main water shutoff
- Hose valve actuation
- Vehicle lock/start/horn/light commands
- Locks
- Sirens
- Alarm system actions
- Home Assistant restart/stop actions
- Vacuum start actions that could run during Babysitter Mode or while someone is home

## If Something Looks Wrong

1. Check whether the entity is unavailable in Home Assistant.
2. Check the related device/integration.
3. Check the technical manual for dashboard source files.
4. If a dashboard edit caused the issue, use the dated backup documented in the technical manual.
5. Update GitHub documentation when the fix changes the system.

## Owner Rule

If a dashboard changes how the house is understood or operated, the documentation should change with it.

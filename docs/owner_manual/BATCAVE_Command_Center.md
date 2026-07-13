# BATCAVE Command Center Owner Guide

## What This Is

The BATCAVE Command Center is the main Home Assistant dashboard for quickly understanding the state of the home.

It is designed for everyday use by the family and for quick troubleshooting when something does not look right.

## Where It Lives

Repository file:

```text
home_assistant/dashboards/batcave-command-center.yaml
```

Related technical documentation:

```text
docs/technical_manual/Home_Assistant_Dashboards.md
```

## Main Sections

### Overview

Use this first.

It shows:

- Whether Vacation Mode is on
- Whether Babysitter Mode is on
- Whether Home Assistant thinks the home is occupied
- Overall house/infrastructure health helpers
- Weather
- Thermostat
- Important temperatures and humidity readings
- Camera snapshot/status cards
- Terry vacuum status
- Important updates

### Security

Use this to check camera and detection status.

It shows front camera detection, Malachi room detection, and camera-related settings.

### Climate

Use this to check comfort and humidity.

It shows the Dining Room thermostat, Henry humidifier, room sensors, and 24-hour climate trends.

### Infrastructure

Use this when Home Assistant, networking, backups, or the Raspberry Pi might need attention.

It shows WAN status, system monitor readings, backup status, ESPHome/sump ESP diagnostics, and updates.

### Water

Use this to monitor early water-protection pieces.

It currently shows B-hyve BLE status, sump ESP information, Henry water alerts, and future water-protection notes.

### Robotics

Use this to check Terry the robot vacuum.

It shows Terry's status, battery, charging state, errors, Wi-Fi signal, room clean buttons, and automations.

## Safety Notes

This first version intentionally avoids broad dangerous controls.

Examples of controls that should be reviewed carefully before adding:

- Main water shutoff
- Hose valve actuation
- Locks
- Sirens
- Alarm system actions
- Home Assistant restart/stop actions
- Vacuum start actions that could run during Babysitter Mode or while someone is home

## If Something Looks Wrong

1. Check whether the entity is unavailable in Home Assistant.
2. Check the related device/integration.
3. Check the technical manual for dashboard source files.
4. Update the GitHub documentation when the fix changes the system.

## Owner Rule

If a dashboard changes how the house is understood or operated, the documentation should change with it.

# BATCAVE Systems Overview

## Network System
Frontier fiber, Eero mesh, PoE switch, Pi, cameras, ESP32 nodes, and remote access.

## Automation System
Home Assistant, HACS, ESPHome, helpers, scripts, dashboards, automations, notifications, and integrations.

## Water Protection System
Sump monitoring, leak detection, outdoor hose valve control, and future main water shutoff.

## Climate System
Nest thermostat, room sensors, crawl space monitoring, garage monitoring, and humidity management.

## Energy System
Future CT clamp monitoring for whole-home and branch circuit energy usage.

## Security / Camera System
Reolink cameras, AI detection, TV display ideas, motion/person events, and future crawl space camera.

## Robotics System
Shark robot vacuum “Terry,” away-mode cleaning, stuck notifications, and docking behavior. Terry away-cleaning now starts when Dustin and Kaylie have both been away for 15 minutes, the house is not otherwise occupied, Terry is docked, and battery is above 90%.

## Backup / Resilience System
Home Assistant creates daily automatic backups to Alfred via the `AlfredBackups` SMB mount. Alfred keeps backup files for roughly 20 days and has a scheduled cleanup task. Backup failure, stale-backup, and weekly success-summary notifications are configured.

## Maintenance System
Future reminders for HVAC filters, sump testing, water softener, camera cleaning, UPS, firmware updates, seasonal hose shutoff, and backup verification.

# BAT-005 Release Notes

## v0.1 Started — July 13, 2026

### Added

- Started BAT-005 for vehicle integration reliability.
- Researched Home Assistant Uconnect integration behavior.
- Confirmed Uconnect integration is current at `v0.5.2`.
- Confirmed default scan interval is already 5 minutes.
- Enabled Uconnect command entities.
- Added stale-data notification automation for Chrysler Dadvan telemetry.
- Added T-Mobile SyncUP DRIVE / OBD-II research notes.
- Added vehicle tracking alternatives comparison including Traccar and API-first OBD trackers.
- Added standalone Dadvan dashboard source and Vehicles view for the BATCAVE Operations Center.
- Added Dadvan SVG placeholder image for the dashboard.

### Findings

- Dadvan telemetry source timestamp is stale even after Home Assistant update requests.
- Official app staleness suggests the root cause may be the van/Stellantis cloud rather than Home Assistant.
- Uconnect update requests re-fetch cloud data but do not guarantee fresh vehicle data.
- Real-time vehicle tracking is not supported by the Uconnect API.
- T-Mobile SyncUP DRIVE-style OBD devices may not report fresh data until the vehicle is started/driven.
- Since the Dadvan has not been driven since July 10, the stale July 10 timestamp may be normal no-drive/sleep behavior.
- No obvious public Home Assistant integration was found for T-Mobile SyncUP DRIVE itself.

### Pending

- Observe whether Dadvan data refreshes after driving.
- Determine whether Uconnect/SiriusXM Guardian subscription state affects refresh behavior.
- Determine whether command PIN setup improves refresh/location command success.
- Sync the source-controlled Vehicles/Dadvan view into the live Home Assistant dashboard UI and verify rendering.

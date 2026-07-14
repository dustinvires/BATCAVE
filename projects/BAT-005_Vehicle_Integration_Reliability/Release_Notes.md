# BAT-005 Release Notes

## v0.1 Started — July 13, 2026

### Added

- Started BAT-005 for vehicle integration reliability.
- Researched Home Assistant Uconnect integration behavior.
- Confirmed Uconnect integration is current at `v0.5.2`.
- Confirmed default scan interval is already 5 minutes.
- Enabled Uconnect command entities.
- Added stale-data notification automation for Chrysler Dadvan telemetry.

### Findings

- Dadvan telemetry source timestamp is stale even after Home Assistant update requests.
- Official app staleness suggests the root cause may be the van/Stellantis cloud rather than Home Assistant.
- Uconnect update requests re-fetch cloud data but do not guarantee fresh vehicle data.
- Real-time vehicle tracking is not supported by the Uconnect API.

### Pending

- Observe whether Dadvan data refreshes after driving.
- Determine whether Uconnect/SiriusXM Guardian subscription state affects refresh behavior.
- Determine whether command PIN setup improves refresh/location command success.
- Add vehicle dashboard status/freshness card.

# BAT-005: Vehicle Integration Reliability

## Objective

Improve reliability and observability for BATCAVE vehicle integrations, starting with the Chrysler Dadvan Uconnect integration.

## Status

Started — Monday, July 13, 2026 at 8:09 PM CDT

## Current findings

### Uconnect / Chrysler Dadvan

The Home Assistant Uconnect integration is installed and current:

- Integration: `hass-uconnect/hass-uconnect`
- Installed version: `v0.5.2`
- Latest version: `v0.5.2`
- Config entry: `CHRYSLER_US dustinvires@gmail.com`
- Default polling interval: 5 minutes

The integration is polling Home Assistant frequently, but the van’s own Uconnect/Stellantis cloud data is stale.

Observed stale source timestamp:

```text
sensor.chrysler_dadvan_last_info_update_at = 2026-07-10T23:50:09+00:00
```

This matters because Home Assistant can only report what the Uconnect/Stellantis cloud returns. If the official Chrysler/Uconnect app is stale too, the likely issue is the vehicle modem, vehicle sleep state, account/cloud backend, or Stellantis service rather than Home Assistant polling.

## Actions taken

- Researched `hass-uconnect` behavior and limitations.
- Confirmed the integration default scan interval is already 5 minutes.
- Confirmed `uconnect.update` re-fetches cloud data but does not force the van to produce fresh telemetry.
- Confirmed `deep_refresh` is primarily useful for EV battery refresh scenarios and is not a general real-time refresh mechanism.
- Enabled Uconnect command entities in the integration options.
- Verified command entities were created:
  - `button.garage_chrysler_dadvan_update_data`
  - `button.garage_chrysler_dadvan_refresh_location`
  - `button.garage_chrysler_dadvan_deep_refresh`
  - `lock.garage_chrysler_dadvan_doors_lock`
  - `switch.garage_chrysler_dadvan_engine`
  - `button.garage_chrysler_dadvan_lights_horn`
- Tested `button.garage_chrysler_dadvan_update_data`; it ran but returned the same stale source timestamp.
- Tested `button.garage_chrysler_dadvan_refresh_location`; it returned an error, likely unsupported/rejected for the vehicle/account or requiring different command credentials/PIN behavior.
- Added stale-data alert automation:
  - `automation.uconnect_dadvan_stale_data_alert`

## Automation added

`Uconnect Dadvan - Stale Data Alert`

Runs daily at 8:30 AM and notifies Dustin’s iPhone if Dadvan Uconnect data is older than 24 hours.

## Working theory

The main issue is probably not Home Assistant polling frequency. The official app being stale strongly suggests the van or Stellantis cloud is not publishing fresh telemetry.

Possible root causes:

- Van cellular modem asleep/offline.
- Uconnect/SiriusXM Guardian subscription or service limitations.
- Stellantis cloud not receiving updated data from the van.
- Vehicle does not support live status/location refresh reliably.
- Uconnect integration can only poll stale cloud data.

## Next steps

1. Compare Home Assistant timestamps against the official app after the van is driven.
2. Test whether data updates shortly after engine start/drive/park cycles.
3. Confirm Uconnect/SiriusXM Guardian connected services subscription status.
4. Investigate whether a PIN enables more command refresh functionality.
5. Decide whether to expose command entities on a dashboard, with lock/engine/horn controls protected or hidden.
6. Add a vehicle dashboard card showing stale/fresh status clearly.

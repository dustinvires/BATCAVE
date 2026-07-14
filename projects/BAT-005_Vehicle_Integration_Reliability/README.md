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

Important context added July 13, 2026 at 8:21 PM CDT: the van has not been driven since July 10. That lines up exactly with the stale timestamp and may be normal behavior if the vehicle or connected service only publishes fresh data after engine/start/drive events.

### T-Mobile SyncUP DRIVE / OBD-II research

The T-Mobile OBD-II plug-in product is likely **SyncUP DRIVE**.

Official T-Mobile documentation indicates:

- The device plugs into the vehicle OBD-II port.
- It uses T-Mobile cellular data and GPS.
- Initial setup requires starting the engine and going for a drive.
- Troubleshooting explicitly says to wait after setup and take the car on a drive.
- LED status matters:
  - solid green means connected to cellular data/GPS,
  - solid red means powered but not connected,
  - blinking green can mean it has not connected to cellular/GPS yet.
- SyncUP DRIVE is a **one-way reader**. It reports vehicle/location data but cannot remotely control locks, engine, horn, etc.

Implication for Dadvan:

- If the Dadvan has not moved since July 10, stale SyncUP/Uconnect-style telemetry may be expected.
- A parked/sleeping vehicle may not continuously produce fresh OBD/location events.
- If the official app still shows July 10 after the next drive, the likely issue shifts toward the OBD device, cellular/GPS signal, account provisioning, device firmware, or T-Mobile/SyncUP backend.

No obvious public Home Assistant integration was found for T-Mobile SyncUP DRIVE itself. That means SyncUP DRIVE is useful in its own app, but it is not currently a strong automation-native BATCAVE data source unless a supported API or reverse-engineered integration becomes available.

### Better-solution comparison

Current best options:

1. **Keep Uconnect/SyncUP as-is and monitor freshness**
   - Lowest effort.
   - Best if stale data simply means the van has not been driven.
   - Home Assistant stale-data alert handles visibility.

2. **Use Home Assistant mobile-app location as the practical automation source**
   - Best for person-based automations.
   - Already works with iPhones.
   - Does not provide vehicle health/fuel/odometer.

3. **Use Traccar with a dedicated GPS tracker**
   - Strongest Home Assistant-native option for vehicle location.
   - Home Assistant has official Traccar Client and Traccar Server integrations.
   - Supports device trackers, motion/status, speed, geofence events, and sensors.
   - Requires separate tracker hardware/SIM or phone client.
   - Better for reliable location/geofencing than Uconnect/SyncUP, but not necessarily better for vehicle-health data.

4. **Use Bouncie or another API-first OBD tracker**
   - Potentially better if official API access is available.
   - Needs more product/API verification before adopting.
   - May duplicate SyncUP monthly cost.

Preliminary recommendation: do not replace the current setup yet. First drive the van and observe whether data refreshes. If it refreshes after driving, the stale July 10 timestamp is probably normal sleep/no-drive behavior. If it does not refresh after driving, consider reseating/restarting the OBD device, checking LED/cellular/GPS state, and contacting T-Mobile before buying new hardware.

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
- Added Dadvan dashboard source:
  - `home_assistant/dashboards/dadvan-command-center.yaml`
- Added Dadvan view to the BATCAVE Operations Center source dashboard:
  - `home_assistant/dashboards/batcave-operations-center.yaml`
- Added Dadvan dashboard placeholder image:
  - `home_assistant/www/batcave/dadvan.svg`

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
6. Sync the new Vehicles/Dadvan dashboard view into the live Home Assistant dashboard UI and verify rendered layout.

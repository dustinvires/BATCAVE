# Known Issues

## Reolink Streaming
Camera streaming through Home Assistant has been slow or unreliable. WebRTC/go2rtc work has been explored.

## B-hyve BLE
Multiple integrations tested. Official/cloud integration sees hose timer but entities may be unavailable. BLE integrations are being tested with ESP32 Bluetooth proxy.

### 2026-07-13 Update

Observed issue: Home Assistant showed `switch.bhyve_ble_44_67_55_86_26_9d_port_1` as `on`, but the physical B-hyve hose timer was not actually watering.

Actions taken:

- Updated Orbit B-hyve BLE integration from `v0.0.8` to `v0.1.0`.
- Restarted Home Assistant as required by the integration update.
- Confirmed Home Assistant Core updated to `2026.7.2`.
- Pressed the B-hyve BLE refresh-status button.

Post-update state:

- `switch.bhyve_ble_44_67_55_86_26_9d_port_1`: `off`
- `sensor.outside_bhyve_ble_44_67_55_86_26_9d_port_1_status`: `off`
- `number.outside_bhyve_ble_44_67_55_86_26_9d_port_1_run_time`: `600`
- Battery: `92%` / `2956 mV`

Likely cause: stale or incomplete state reporting in the older BLE integration version. The older `last_message_type` sensor is now restored/unavailable and should not be treated as the primary status source. Use the port status sensor as the preferred truth source for the dashboard.

## OnStar / Buick
onstar2mqtt has recurring access denied / MFA / TOTP issues.

## Apple Watch Home Assistant
Watch configuration did not populate entities/actions correctly. Deferred for later.

## Kaylie Location Reliability
Kaylie’s phone has delayed or unreliable Home Assistant location updates. iOS settings appear similar to Dustin’s phone, so this remains under observation. Terry automation now uses `person.kaylie` and a 15-minute away window to reduce false/early triggers, but future diagnostics may be needed if `device_tracker.kaylies` stops updating for long periods.

## Home Occupied Template
`binary_sensor.home_occupied` is intentionally used as a safety guard for babysitter/guest scenarios so Terry does not start while someone else is home. It previously blocked Terry even when Dustin and Kaylie were away, so its template/source logic should be reviewed if Terry still does not run as expected.

## New NVMe Drive
New NVMe/hat replacement experienced HAOS boot/image issues. Old SSD with new hat appears stable.

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

### 2026-07-13 Research Notes

Current local observation: Home Assistant exposes the OnStar2MQTT add-on update entity, but very few OnStar MQTT entities are present. This is consistent with the add-on failing authentication before it can publish normal discovery/state topics.

Relevant upstream findings:

- BigThunderSR OnStar2MQTT requires username, password, PIN, VIN, unique device UUID, MQTT config, and a valid TOTP key.
- As of the newer OnStarJS authentication flow, the GM account MFA method should be **Third-Party Authenticator App**. The docs note this option may not appear on mobile and may need to be configured from a desktop browser.
- Valid system time/NTP is required for TOTP to work.
- The OnStar API is rate-limited and temperamental. Polling below the default 30 minutes can trigger rate limits.
- Open upstream issues match this installation's symptoms:
  - `#1299 Access Denied Response` — access denied after password stage.
  - `#1740 Authentication denied for second vehicle` — access denied despite app/web login still working.
  - `#1552 Did not capture auth code after submit` — MFA submit occurs but authorization code is not captured.
- PR `#1685 fix: harden MFA login in HA add-ons` reduced MFA/TOTP retry-loop problems and bumped add-ons to `2.8.5`; this installation is on `2.9.0`, so it should include that class of fix.

Recommended recovery path:

1. Stop the OnStar2MQTT add-on to avoid repeated login attempts while troubleshooting.
2. Confirm the GM/myBuick account can log in from a desktop browser.
3. Confirm the account has Third-Party Authenticator App MFA enabled, not SMS/email-only MFA.
4. Re-copy the raw TOTP secret/key, not a one-time six-digit code.
5. Confirm Home Assistant system time is correct via NTP.
6. Keep `ONSTAR_REFRESH` at the default 30 minutes or longer.
7. Confirm token persistence is configured so tokens survive restarts.
8. If access denied continues, wait before retrying to avoid lockout-style behavior.
9. If the add-on was upgraded from API v2-era versions, clean stale retained MQTT topics and ghost entities per the upstream v2 migration notes.
10. Capture sanitized add-on logs from startup through the failed auth stage before opening/updating an upstream issue.

### 2026-07-13 Live UI Retest

Manual GM account login from a normal browser succeeded. The GM Security page showed:

- Text/SMS Authentication: disabled
- Email Authentication: disabled
- Third-Party Authenticator App: enabled

A single controlled OnStar2MQTT start was performed at approximately 14:23 CDT and then stopped when repeated retries continued. Findings:

- Add-on version: `2.9.0`
- Token/cache path `/ssl/vehicle1` is being used successfully; the add-on loaded cached unit data from `/ssl/vehicle1/.unit_cache_kl4mmgsl7mb154117.json`.
- The add-on launches its automated GM/Microsoft authentication browser successfully under Xvfb.
- The failure occurs after the add-on enters the email and proceeds into the password submission flow.
- The log reports `[ACCESS DENIED]` from GM's `SelfAsserted` endpoint before the flow reaches TOTP/MFA.
- Because the flow does not reach TOTP/MFA, regenerating the authenticator key is unlikely to fix this specific failure by itself.

Current working theory: GM is blocking or denying the automated/headless/mobile-app-style login flow even though manual browser login works. Avoid repeated starts because the add-on performs multiple internal retry attempts per start and may worsen rate-limit/security-block behavior.

## Apple Watch Home Assistant
Watch configuration did not populate entities/actions correctly. Deferred for later.

## Kaylie Location Reliability
Kaylie’s phone has delayed or unreliable Home Assistant location updates. iOS settings appear similar to Dustin’s phone, so this remains under observation. Terry automation now uses `person.kaylie` and a 15-minute away window to reduce false/early triggers, but future diagnostics may be needed if `device_tracker.kaylies` stops updating for long periods.

## Home Occupied Template
`binary_sensor.home_occupied` is intentionally used as a safety guard for babysitter/guest scenarios so Terry does not start while someone else is home. It previously blocked Terry even when Dustin and Kaylie were away, so its template/source logic should be reviewed if Terry still does not run as expected.

## New NVMe Drive
New NVMe/hat replacement experienced HAOS boot/image issues. Old SSD with new hat appears stable.

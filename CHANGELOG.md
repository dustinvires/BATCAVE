# Changelog

## Unreleased

- Added and installed the live BATCAVE Operations Center dashboard in Home Assistant.
- Documented dashboard deployment, rollback, and maintenance procedures.
- Updated Home Assistant Core from `2026.7.1` to `2026.7.2`.
- Updated ESPHome Device Builder from `2026.6.4` to `2026.6.5`.
- Updated Shark2MQTT from `1.0.4` to `1.0.6`.
- Updated Orbit B-hyve BLE from `v0.0.8` to `v0.1.0`.
- Documented B-hyve BLE stale switch-state issue and preferred post-update status entity.
- Simplified camera dashboard cards to one live-friendly stream per physical camera, preferring Reolink `fluent` streams for lower-latency viewing.
- Added B-hyve outdoor spigot dashboard toggle while keeping actual spigot status as the displayed truth source.
- Documented OnStar2MQTT authentication/TOTP/access-denied research and recovery checklist.
- Added live OnStar2MQTT UI retest notes showing manual GM login succeeds but add-on automation fails with access denied before reaching TOTP/MFA.
- Renamed the Infrastructure dashboard processor temperature gauge to Alfred CPU Temperature.
- Added RockAI handoff documenting BATCAVE Home Assistant dashboard standards, workflow, safety rules, and design logic.
- Added source-controlled Terry early rescue and guarded emergency unstick automation/script drafts, including cliff-sensor recovery as an allowed stuck-style error.
- Added Dadvan / Vehicles dashboard view with Uconnect freshness, vehicle health, tire pressure, location, refresh actions, and deliberately grouped vehicle commands.
- Added standalone `dadvan-command-center.yaml` dashboard source and Dadvan SVG placeholder image.

## v0.1.0
- BAT-001 initialized.

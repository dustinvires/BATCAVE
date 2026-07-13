# Home Assistant Dashboard Handoff for RockAI

**Prepared:** 2026-07-13 17:13 CDT
**System:** BATCAVE Home Assistant / BATCAVE Operations Center
**Repository branch:** `feature/home-assistant-dashboards`
**Live dashboard:** `/batcave-operations-center/overview`

## Purpose

This handoff explains the dashboard design standards and operating logic used for the BATCAVE Home Assistant dashboards so RockAI can continue the work without creating conflicting dashboards or drifting from the source of truth.

The current preferred dashboard is the existing **BATCAVE Operations Center** dashboard. Do not create a new competing command center unless Dustin explicitly asks for one. Improve the existing dashboard instead.

## Source of Truth

Dashboard source files are maintained in GitHub:

- `home_assistant/dashboards/batcave-operations-center.yaml`
- `home_assistant/dashboards/batcave-command-center.yaml`
- `home_assistant/dashboards/README.md`
- `docs/technical_manual/Home_Assistant_Dashboards.md`
- `docs/owner_manual/BATCAVE_Command_Center.md`
- `CHANGELOG.md`

The live Home Assistant dashboard is currently storage-backed and has been synced manually through the Home Assistant UI/raw Lovelace configuration editor or frontend websocket calls. There is not yet a permanent Git-to-Home-Assistant deployment pipeline.

When changing dashboard behavior:

1. Update the GitHub YAML/source file.
2. Update technical/owner documentation as appropriate.
3. Update `CHANGELOG.md`.
4. Commit to the active branch.
5. Sync the live Home Assistant dashboard.
6. Verify the live dashboard config/state.

## Design Philosophy

The dashboard follows BATCAVE operating principles:

> Safe • Reliable • Comfortable • Efficient • Maintainable • Understandable

And Dustin's documentation rule:

> If it changes how the home is operated, document it.

Dashboards should be practical, readable, and family-safe. The goal is not to expose every possible entity; the goal is to expose the right operational information with clear names.

## Dashboard Structure

The **BATCAVE Operations Center** is organized into views:

- **Overview** — family-facing home status, weather, comfort, security, Terry, and important updates.
- **Infrastructure** — BATCAVE/Alfred/network/backup/system health.
- **Security** — cameras and security sensors.
- **Environment** — climate, humidity, comfort, Henry humidifier.
- **Utilities** — water/B-hyve, backups, and utility status.
- **Automations** — key automations grouped by function.
- **Engineering** — GitHub/source-of-truth/documentation references and health helpers.

Prefer adding new cards to the most semantically appropriate existing view rather than creating new tabs.

## Naming Standards

Use real-world names over technical entity names.

Good examples:

- `Outdoor Spigot` instead of `Port 1 Toggle`
- `Spigot Status` instead of `Port 1 Actual Status`
- `Watering Duration` instead of `Port 1 Run Time`
- `Alfred CPU Temperature` instead of `Pi Temperature`
- `Hose Timer Battery` instead of raw B-hyve battery label

Entity IDs can remain technical in YAML, but user-visible names should describe the real-world thing Dustin interacts with.

Avoid showing irrelevant implementation details. Example: the current B-hyve device only has one output, so the output-port count was removed from the dashboard.

## Safety Standards

Use native Home Assistant cards first. Avoid custom-card complexity unless there is a clear reason.

Avoid exposing risky controls broadly:

- Locks
- Alarms
- Water valves/spigots
- HVAC changes
- Vacuum starts
- Vehicle commands

If a risky control is added, pair it with clear status/truth-source cards and document the decision.

### B-hyve / Outdoor Spigot Pattern

For the B-hyve hose timer, the dashboard intentionally separates command from truth:

- **Outdoor Spigot** — `switch.bhyve_ble_44_67_55_86_26_9d_port_1`; command/control surface.
- **Spigot Status** — `sensor.outside_bhyve_ble_44_67_55_86_26_9d_port_1_status`; preferred actual state/truth source.
- **Watering Duration** — `number.outside_bhyve_ble_44_67_55_86_26_9d_port_1_run_time`.

This exists because the older integration could show the command switch as `on` even when the physical hose timer was not actually watering.

## Camera Standards

Show one useful stream per physical camera whenever possible.

Current camera approach:

- Prefer Reolink `fluent` streams for live dashboard responsiveness.
- Keep the Ring front door live view separate because it is a distinct physical/source feed.
- Avoid showing both `clear` and `fluent` versions of the same Reolink camera on the main dashboard unless Dustin asks for a diagnostic view.

Current retained camera examples:

- `camera.front_fluent`
- `camera.front_door_live_view`
- `camera.malachi_room_fluent`

## Infrastructure Standards

Infrastructure should show system health without overwhelming the user.

Examples:

- BATCAVE / network health
- eero WAN status
- External IP
- Raspberry Pi / host power status
- CPU usage
- Memory usage
- **Alfred CPU Temperature** via `sensor.system_monitor_processor_temperature`
- Backup manager state
- Last/next backup timestamps
- ESPHome / Bluetooth proxy diagnostics
- Update entities needing attention

Use gauges for continuous health metrics when thresholds are meaningful. Use tiles for binary/status values.

## Climate and Humidity Logic

The thermostat can report `hvac_action: cooling` even when the cooling setpoint is higher than current temperature. This may be thermostat-side humidity/dehumidification behavior rather than a Home Assistant automation.

Do not assume the HA automation caused cooling without checking:

- `climate.dining_room`
- `sensor.dining_room_temperature`
- `sensor.dining_room_humidity`
- `automation.humidity_too_high_in_house`
- `input_boolean.vacation_mode_on_off`
- `binary_sensor.home_occupied`

Current preferred logic direction:

- Dustin wants Home Assistant humidity policy to be explicit and understandable.
- Avoid cooling the house to 74°F when nobody is home just because humidity is around 55%.
- If HA humidity control is refined later, consider thresholds like occupied vs away/vacation, and use higher away humidity protection thresholds.

## OnStar2MQTT Status

OnStar2MQTT is currently not reliable.

Observed 2026-07-13:

- Manual GM login works.
- GM account uses Third-Party Authenticator App MFA.
- Add-on version was `2.9.0`.
- Add-on loads `/ssl/vehicle1` cache/token path.
- Automated login fails after email/password submission with GM `ACCESS DENIED` before reaching TOTP/MFA.
- Repeated starts can worsen GM security/rate-limit blocking.

Do not keep restarting the add-on repeatedly. If continuing this work, research/manual token generation is preferred over repeated add-on auth attempts.

Related notes are documented in:

- `projects/BAT-002_Asset_Inventory/Known_Issues.md`

## Entity Selection Logic

When adding dashboard cards:

1. Prefer live entities confirmed through Home Assistant states.
2. Prefer stable/status entities over transient/debug entities.
3. Prefer actual state sensors over command switches when there is a difference.
4. Prefer friendly labels that match household language.
5. Remove duplicate or low-value cards.
6. Keep dashboards useful on mobile/tablet.

Examples:

- For B-hyve, use the status sensor as the truth source.
- For cameras, use one responsive stream per camera.
- For system temperature, label it as Alfred if that is the real host being monitored.

## Card Type Guidelines

Use these defaults:

- `tile` — status, helpers, switches, sensors, updates.
- `gauge` — CPU, memory, temperature, battery-like metrics with thresholds.
- `weather-forecast` — weather summary.
- `thermostat` — primary thermostat control.
- `picture-entity` or camera-friendly native cards — camera views.
- `markdown` — explanatory blocks, GitHub/documentation links, roadmap notes.
- `heading` — group cards clearly within section views.

Avoid over-customizing unless a native card cannot communicate the operational status clearly.

## Documentation Expectations

Every meaningful dashboard change should update at least one of:

- `docs/technical_manual/Home_Assistant_Dashboards.md`
- `docs/owner_manual/BATCAVE_Command_Center.md`
- `home_assistant/dashboards/README.md`
- `projects/BAT-002_Asset_Inventory/Known_Issues.md`
- `CHANGELOG.md`

For small label fixes, `CHANGELOG.md` plus the technical dashboard manual may be enough.

For operational behavior changes, update owner-facing docs too.

## Git Workflow

Current active branch:

```text
feature/home-assistant-dashboards
```

Keep main stable. Use commits with clear messages and include the Craft Agent co-author trailer when Craft Agent performs the work:

```text
Co-Authored-By: Craft Agent <agents-noreply@craft.do>
```

Do not merge to `main` without Dustin's approval.

## Current Known Gaps

- No persistent automated deployment path from GitHub YAML to Home Assistant storage dashboard.
- Live dashboard sync is still manual/UI/websocket-based.
- SSH to Home Assistant previously failed.
- Samba, Studio Code Server, Git pull add-on, or other config access could be explored later.
- OnStar2MQTT authentication remains unresolved.
- Humidity/thermostat dehumidification behavior needs policy refinement.

## Recommended Next Improvements

1. Build a stable Git-to-HA dashboard deployment workflow.
2. Refine humidity policy so HA controls when humidity-driven cooling is allowed.
3. Continue trimming duplicate dashboard entities.
4. Add issue/status notes for unavailable entities that matter.
5. Continue improving mobile/tablet readability.

## Summary for RockAI

Continue improving the existing **BATCAVE Operations Center** dashboard. Use GitHub as the source of truth, sync carefully to live Home Assistant, and document every meaningful change. Prefer clear real-world labels, safe native cards, and truth-source status sensors. Do not expose risky controls casually. When in doubt, make the dashboard more understandable, not more crowded.

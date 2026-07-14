# BAT-005 Verification Checklist

## Uconnect integration

- [x] Confirm Uconnect integration exists.
- [x] Confirm integration version is current.
- [x] Confirm default scan interval.
- [x] Enable command entities.
- [x] Confirm command entities were created.
- [x] Test Update Data command.
- [x] Test Refresh Location command.
- [x] Add stale-data alert automation.
- [x] Verify stale-data alert automation is enabled.
- [x] Research T-Mobile SyncUP DRIVE / OBD-II reporting behavior.
- [x] Research Home Assistant-friendly alternatives.

## Remaining validation

- [ ] Drive Dadvan and check if telemetry updates after trip completion.
- [ ] Compare Home Assistant values with official Chrysler/Uconnect app and, if applicable, T-Mobile/T-Life SyncUP DRIVE app.
- [ ] Check SyncUP DRIVE LED state while vehicle is outside and running: solid green expected for cellular/GPS connection.
- [ ] Reseat/restart SyncUP DRIVE OBD-II device if data does not refresh after the next drive.
- [ ] Confirm connected services/subscription status.
- [ ] Determine whether PIN setup is needed for command refresh behavior.
- [ ] Decide whether command entities should be exposed on dashboards.
- [x] Add vehicle freshness/staleness card to dashboard source.
- [x] Add standalone Dadvan command center dashboard source.
- [x] Add Dadvan view to Operations Center source dashboard.
- [x] Sync Vehicles/Dadvan dashboard changes into the live Home Assistant dashboard UI.
- [x] Verify Dadvan dashboard renders correctly on desktop.
- [ ] Verify Dadvan dashboard renders correctly on mobile.
- [ ] Install `/config/www/batcave/dadvan.svg` or replace with a real Dadvan photo, then optionally re-enable the picture card.

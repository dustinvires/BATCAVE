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

## Remaining validation

- [ ] Drive Dadvan and check if telemetry updates after trip completion.
- [ ] Compare Home Assistant values with official Chrysler/Uconnect app.
- [ ] Confirm connected services/subscription status.
- [ ] Determine whether PIN setup is needed for command refresh behavior.
- [ ] Decide whether command entities should be exposed on dashboards.
- [ ] Add vehicle freshness/staleness card to dashboard.

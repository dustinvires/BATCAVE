# Presence Automations

Last updated: Monday, July 13, 2026 at 1:47 PM CDT

## Terry Working

Automation export:

- `home_assistant/automations/terry_working_presence_cleaning.yaml`

### Intent

Terry should start cleaning after Dustin and Kaylie have both been away from home for 15 minutes, but only when the home is otherwise unoccupied.

The `binary_sensor.home_occupied` condition is intentionally retained as a safety check for cases where someone else is in the house, such as a babysitter, so Terry does not start unexpectedly and scare Malachi.

### Current logic

Terry starts only when all of the following are true:

- `person.dustin` has been `not_home` for 15 minutes, or `person.kaylie` has been `not_home` for 15 minutes and the other person is already away.
- `person.dustin` is `not_home`.
- `person.kaylie` is `not_home`.
- `binary_sensor.home_occupied` is `off`.
- Terry is docked.
- Terry battery is above 90%.
- Time is between 8:00 AM and 5:00 PM.

Vacation mode no longer blocks Terry. This allows cleaning while the house is in vacation mode.

### Previous failure patterns found in traces

Recent Terry Working traces showed that the automation was triggering, usually from Kaylie's phone leaving the home zone, but often stopped because:

- The trigger occurred outside the configured 8:00 AM–5:00 PM window.
- `binary_sensor.home_occupied` was still `on` even though both phone trackers were away.

### Kaylie location reliability notes

Kaylie's Home Assistant mobile app tracker is a GPS tracker from the `mobile_app` integration. At inspection time, Kaylie's tracker was updating less frequently than Dustin's, even though both appeared to have similar iOS settings.

If location reliability remains an issue, next diagnostic steps:

1. Compare Kaylie's `sensor.kaylies_last_update_trigger` and `device_tracker.kaylies` timestamps over several days.
2. Check whether iOS Low Power Mode or Focus modes suppress Home Assistant background activity.
3. Add an alert when `device_tracker.kaylies` has not updated for more than a chosen threshold, such as 60–90 minutes.
4. Consider supplementing GPS with network-based presence if a reliable router/Wi-Fi tracker becomes available.

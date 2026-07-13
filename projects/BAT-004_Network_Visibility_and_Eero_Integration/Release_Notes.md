# BAT-004 Release Notes

## v0.1 Started — July 13, 2026

### Added / changed

- Started BAT-004 for Network Visibility and Eero Integration.
- Researched Home Assistant options for Eero network/device visibility.
- Selected `schmittx/home-assistant-eero` custom integration.
- Installed the custom integration into Home Assistant at `/config/custom_components/eero`.
- Restarted Home Assistant to load the integration.
- Verified that Home Assistant now exposes the `eero` config flow handler.

### Completed after login

- Completed Eero account login/config flow.
- Submitted Eero integration option screens with default selections.
- Verified new Eero entities in Home Assistant.
- Documented Eero entity inventory in `Eero_Entity_Inventory.md`.

### Pending

- Build network dashboard cards/entities.
- Decide which Eero control entities should be exposed in dashboards versus kept hidden/read-only.
- Evaluate whether Eero Plus activity metrics are available/useful.

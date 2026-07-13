# BAT-004 Release Notes

## v0.1 Started — July 13, 2026

### Added / changed

- Started BAT-004 for Network Visibility and Eero Integration.
- Researched Home Assistant options for Eero network/device visibility.
- Selected `schmittx/home-assistant-eero` custom integration.
- Installed the custom integration into Home Assistant at `/config/custom_components/eero`.
- Restarted Home Assistant to load the integration.
- Verified that Home Assistant now exposes the `eero` config flow handler.

### Pending

- Complete Eero account login/config flow.
- Handle any Eero OTP/verification challenge.
- Determine whether Dustin’s Eero account uses Amazon login or standard Eero login.
- Verify created Eero entities.
- Build network dashboard cards/entities.

# BAT-004: Network Visibility and Eero Integration

## Objective

Improve BATCAVE network visibility by integrating Eero with Home Assistant so router/WAN state, Eero devices, connected clients, and possible activity metrics can be surfaced in dashboards and automations.

## Status

Started — July 13, 2026

## Current understanding

Dustin has Frontier/Verizon-provided internet with Eero hardware/service support. Eero is owned by Amazon, but ISP-provided Eero systems still generally use Eero cloud account authentication. The Home Assistant custom integration talks to the Eero cloud/API, not directly to Frontier.

Important caveat: the custom Eero integration does not support Amazon-account login directly. If Dustin’s Eero account uses “Sign in with Amazon,” the likely workaround is to create a separate non-Amazon Eero account and add it as an admin on the Eero network.

## Integration selected

Custom HACS integration:

- Repository: `schmittx/home-assistant-eero`
- URL: `https://github.com/schmittx/home-assistant-eero`
- Home Assistant domain: `eero`

## Current progress

- Current Home Assistant Eero entities before this stage:
  - `binary_sensor.eero_wan_status`
  - `sensor.eero_external_ip`
- HACS panel did not render correctly in the embedded browser, so the integration was installed directly into `/config/custom_components/eero` using the running Studio Code Server add-on.
- Home Assistant was restarted.
- Home Assistant now exposes the `eero` config flow handler.
- Eero setup flow has been started and is waiting for the account `login` field.

## Expected capabilities

Based on the integration documentation, possible capabilities include:

- Multiple Eero networks
- Guest network controls
- Eero Plus / Eero Labs feature controls
- Pause access for profiles and clients
- Content filters for profiles
- Device tracker entities for clients and profiles
- Sensors for network/resource metrics
- Firmware update entities
- QR code image entities for joining Wi-Fi
- Activity data sensors if Eero Plus is active

## Next steps

1. Provide Eero account login email/phone for the setup flow.
2. Complete any Eero verification challenge or OTP.
3. Confirm whether the account is Amazon-authenticated or standard Eero login.
4. Verify created Eero entities in Home Assistant.
5. Identify useful client/device trackers.
6. Build network visibility dashboard section/cards.
7. Document final entity list and dashboard design.

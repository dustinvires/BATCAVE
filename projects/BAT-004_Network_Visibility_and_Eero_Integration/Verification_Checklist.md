# BAT-004 Verification Checklist

## Installation

- [x] Identify existing Eero entities in Home Assistant.
- [x] Research available Eero integrations/add-ons.
- [x] Select `schmittx/home-assistant-eero` custom integration.
- [x] Install custom component files to `/config/custom_components/eero`.
- [x] Restart Home Assistant.
- [x] Verify `eero` appears as a config flow handler.

## Account setup

- [ ] Enter Eero account login email/phone.
- [ ] Complete any Eero verification/OTP challenge.
- [ ] Confirm whether account is Amazon-login or standard Eero-login.
- [ ] If Amazon-login blocks setup, create/add non-Amazon Eero admin account.

## Entity verification

- [ ] Confirm Eero network entities are created.
- [ ] Confirm Eero node/device entities are created.
- [ ] Confirm client/device trackers are created.
- [ ] Confirm whether traffic/activity metrics are available.
- [ ] Determine if Eero Plus is required for desired metrics.

## Dashboard follow-up

- [ ] Add WAN status and external IP to infrastructure dashboard.
- [ ] Add Eero nodes and important connected clients.
- [ ] Add offline/online status for critical devices.
- [ ] Add traffic/activity cards if available.

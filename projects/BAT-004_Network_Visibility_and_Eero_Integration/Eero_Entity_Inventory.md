# Eero Entity Inventory

Last updated: Monday, July 13, 2026 at 2:28 PM CDT

## Summary

The `schmittx/home-assistant-eero` custom integration is installed and configured. Home Assistant now exposes Eero network, node, profile/client, QR code, speed test, and feature-control entities.

## Key network entities

| Entity | State / Unit | Purpose |
|---|---:|---|
| `sensor.batcave_status` | connected | Overall Eero network status |
| `sensor.batcave_public_ip` | `50.127.39.34` | Public IP |
| `sensor.batcave_gateway_ip` | `192.168.4.1` | LAN gateway IP |
| `sensor.batcave_wan_router_ip` | `50.127.38.1` | WAN router IP |
| `sensor.batcave_download_speed` | `2649.63 Mbit/s` | Last Eero speed test download result |
| `sensor.batcave_upload_speed` | `2637.05 Mbit/s` | Last Eero speed test upload result |
| `sensor.batcave_connected_clients` | `0 clients` | Main network connected clients as reported by Eero network summary |
| `sensor.batcave_connected_guest_clients` | `0 clients` | Guest network connected clients |
| `binary_sensor.eero_wan_status` | `on` | Original Eero WAN connectivity status |
| `sensor.eero_external_ip` | `50.127.39.34` | Original Eero external IP sensor |

## Eero nodes

| Entity | State | Notes |
|---|---:|---|
| `sensor.garage_garage_batcave_garage_status` | green | Garage Eero node status |
| `sensor.garage_garage_batcave_garage_connected_clients` | 12 clients | Garage node client count |
| `light.garage_garage_batcave_garage_status_light` | on | Garage Eero status light |
| `update.garage_garage_batcave_garage_firmware` | off | Garage Eero firmware update status |
| `sensor.office_office_batcave_office_status` | green | Office Eero node status |
| `sensor.office_office_batcave_office_connected_clients` | 11 clients | Office node client count |
| `light.office_office_batcave_office_status_light` | on | Office Eero status light |
| `update.office_office_batcave_office_firmware` | off | Office Eero firmware update status |

## Feature controls

| Entity | State | Notes |
|---|---:|---|
| `switch.batcave_guest_network` | off | Guest network control |
| `switch.batcave_upnp` | on | UPnP control |
| `switch.batcave_ipv6_enabled` | on | IPv6 control |
| `switch.batcave_thread_enabled` | on | Thread control |
| `switch.batcave_backup_internet_enabled` | on | Backup internet setting |
| `switch.batcave_advanced_security` | on | Eero security feature |
| `switch.batcave_ad_blocking` | off | Network ad blocking |
| `switch.batcave_wpa3` | off | WPA3 control |
| `switch.batcave_band_steering` | on | Band steering control |
| `switch.batcave_smart_queue_management` | off | SQM control |
| `switch.batcave_local_dns_caching` | off | Local DNS caching |
| `switch.batcave_dynamic_dns` | off | Eero dynamic DNS |

## Useful buttons/images

| Entity | Purpose |
|---|---|
| `button.batcave_run_speed_test` | Trigger Eero speed test |
| `button.batcave_reboot` | Reboot Eero network |
| `button.batcave_run_internet_backup_test` | Test backup internet |
| `image.batcave_qr_code` | Main network QR code |
| `image.batcave_guest_network_qr_code` | Guest network QR code |

## Notes

- Eero setup produced a profile/client group named `Unassigned BATCAVE Unassigned`, including content filter controls and a device tracker.
- Activity/traffic data availability may depend on Eero Plus and what the integration exposes after additional refresh cycles.
- Dashboard work should prioritize status/read-only entities first before exposing controls like reboot or content filters.

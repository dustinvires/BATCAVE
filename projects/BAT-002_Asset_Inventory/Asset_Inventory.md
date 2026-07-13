# BATCAVE Asset Inventory

## Network

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| NET-001 | Frontier Fiber ONT | Garage | Active | Main internet service entry point. |
| NET-002 | Eero Gateway | Garage | Active | Main router near ONT. |
| NET-003 | Eero Satellite | Guest room / spare bedroom area | Active | Wi-Fi coverage near B-hyve/ESP test area. |
| NET-004 | TP-Link PoE Switch | Garage | Active | Powers/links cameras and network gear. |

## Servers

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| SRV-001 | Raspberry Pi 5 Home Assistant Server | Garage | Active | Primary Home Assistant OS server. |
| SRV-002 | Alfred Windows PC | Office / main PC location | Active | SMB backup target for Home Assistant; static IP `192.168.4.96`; hosts `\\ALFRED\HomeAssistantBackups`. |
| STR-001 | SSD/NVMe boot media | Garage | Active | Old SSD stable after new NVMe/image issues. |
| STR-002 | Alfred Home Assistant backup share | Alfred | Active | Stores daily Home Assistant backups with 20-day retention. |

## ESPHome Nodes

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| ESP-001 | sump-esp | Spare bedroom now; future crawl space | Active | ESP32 Bluetooth proxy, Wi-Fi diagnostics, uptime, internal temp. |
| ESP-002 | garage-esp | Garage | Planned | Future Pi watchdog and network monitor. |

## Cameras

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| CAM-001 | Reolink RLC-820A | Front garage gable/soffit | Active | PoE camera integrated with HA/Reolink. |
| CAM-002 | Reolink E1 Wi-Fi | Interior/test | Active/Partial | Snapshots available; streaming issues noted. |
| CAM-003 | Crawl Space Camera | Crawl space | Planned | Future water/animal/maintenance visibility. |

## Climate

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| CLM-001 | Google Nest Thermostat | Main house | Active | Vacation Mode uses heat/cool range. |
| SNS-001 | Govee BLE Temp/Humidity Sensor | Garage | Active | Climate monitoring. |
| SNS-002 | Govee BLE Temp/Humidity Sensor | Master/house | Active | Climate monitoring. |
| SNS-003 | Govee BLE Temp/Humidity Sensor | Malachi Bedroom | Active | Area display issue previously noted. |

## Water / Plumbing

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| WTR-001 | Main Water Shutoff | TBD | Planned documentation | Future smart shutoff candidate. |
| WTR-002 | Outdoor Hose Valve 1 | Crawl space | Manual | Future motorized actuator. |
| WTR-003 | Outdoor Hose Valve 2 | Crawl space | Manual | Future motorized actuator. |
| WTR-004 | Sump Pump | Crawl space/sump area | Active | Future float switch and leak detection. |
| WTR-005 | Orbit B-hyve Hose Timer | Outdoor spigot | In progress | BLE integration testing with ESP32 proxy. |

## Vacuum

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| VAC-001 | Shark IQ Robot Vacuum “Terry” | Living areas | Active | Controlled by shark2mqtt. Away-cleaning automation uses Dustin/Kaylie presence, `home_occupied`, docked state, and battery >90%. |

## Entertainment / TVs

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| ENT-001 | LG OLED65B9PUA | Living Room | Active | Full webOS control. |
| ENT-002 | Pioneer Fire TV | TBD | Active | Added via ADB. |
| ENT-003 | Hisense Roku TV | Garage | Active | Roku network control enabled. |

## Vehicles / Integrations

| ID | Asset | Location | Status | Notes |
|---|---|---|---|---|
| VEH-001 | 2017 Chrysler Pacifica | Driveway/Garage | Active | Uconnect integration working. |
| VEH-002 | 2021 Buick Encore | Driveway/Garage | Problematic | OnStar/onstar2mqtt recurring auth issues. |
| VEH-003 | 2021 Kawasaki Vulcan Vaquero 1700 | Garage | Planned presence use | Future garage automation trigger. |

## Helpers / Modes

| ID | Helper | Status | Notes |
|---|---|---|---|
| HLP-001 | Vacation Mode | Active | Used for thermostat behavior; no longer blocks Terry cleaning. |
| HLP-002 | Babysitter Mode | Planned/Active | Intended to prevent Terry/Away automations when someone is watching Malachi. |
| HLP-003 | House Occupied | Active | Aggregate occupancy logic; intentionally blocks Terry if someone else appears to be home. |
| HLP-004 | AlfredBackups | Active | Home Assistant network backup storage mount targeting Alfred SMB share. |

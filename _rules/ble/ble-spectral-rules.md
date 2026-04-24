---
categories:
- ble
description: Spectral linting rules defining API design standards and conventions for BLE.
layout: rules
name: BLE API Rules
provider_name: BLE
provider_slug: ble
rule_count: 5
rules:
- description: GATT service and characteristic UUIDs should follow Bluetooth SIG format
  given: $.components.schemas[*].properties.uuid
  name: ble-uuid-format
  severity: warn
- description: RSSI values must be within valid BLE range (-127 to 0 dBm)
  given: $.components.schemas.AdvertisingPacket.properties.rssi
  name: ble-rssi-range
  severity: warn
- description: GATT characteristic properties must use defined values
  given: $.components.schemas[*].$defs.GattCharacteristic.properties.properties.items
  name: ble-characteristic-properties-enum
  severity: warn
- description: BLE device MAC address must follow XX:XX:XX:XX:XX:XX format
  given: $.components.schemas.AdvertisingPacket.properties.address
  name: ble-address-format
  severity: warn
- description: GATT service definitions must include a UUID
  given: $.components.schemas.GattService
  name: ble-service-uuid-required
  severity: warn
rules_file: rules/ble-spectral-rules.yml
rules_url: https://raw.githubusercontent.com/api-evangelist/ble/refs/heads/main/rules/ble-spectral-rules.yml
severity_counts:
  error: 0
  hint: 0
  info: 0
  warn: 5
slug: ble-spectral-rules
tags:
- BLE
- Bluetooth
- Embedded
- IoT
- Protocols
- Standards
- Wireless
- Spectral
- Linting
- API Governance
---

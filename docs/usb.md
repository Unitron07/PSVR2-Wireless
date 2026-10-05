# Android PSVR2 USB investigation

**Planned process only:** no project descriptors or sensor captures exist. No interface or endpoint numbers are assumed. Refer to [research](../RESEARCH.md) and the [Android USB host API](https://developer.android.com/develop/connectivity/usb/host) during implementation.

## Discovery and access plan

1. Record phone/dock/headset/adapter versions and power/link state.
2. Compare enumeration with the supported wired PC baseline.
3. Use Android USB host discovery to list actual connected devices; distinguish adapter, headset, hub, and unrelated devices where evidence permits.
4. Record vendor/product IDs and device descriptors from capture rather than an assumed identity filter.
5. Request user permission for the intended device; handle denial, detach, and reconnect.
6. Enumerate configurations, interfaces/alternate settings, and endpoints through available APIs/raw descriptors. Record class/subclass/protocol, transfer type, direction, packet size, and interval as captured.
7. Determine which interfaces Android permits the app to access and which are owned by kernel drivers. Document privileges and API limits; do not assume every transfer type is available to an ordinary app.
8. Start with descriptor inspection. Attempt sensor reads only after identifying initialization and transfer behavior from evidence; avoid arbitrary vendor writes.
9. Log timestamps, transfer errors, lengths, frequency, and loss; compare display-off/on and simultaneous SuperSpeed operation.

## Captured descriptors

**TODO:** add sanitized raw descriptor excerpts with test ID, exact setup, capture method, and timestamp. This section intentionally contains no invented identifiers.

## Interface and endpoint inventory

**TODO:** populate from actual captures. Include interface/alternate-setting number, endpoint address, transfer type/direction, access status, and evidence reference.

## Initialization and sensor packets

**TODO / VERIFY:** required startup sequence, sensor format, byte order, units, calibration, timestamps, coordinate frames, and display dependencies. Independently validate parsing against recorded data before forwarding poses. IMU data alone is not full positional tracking.

## USB/IP experiment

**TODO / VERIFY:** Android/kernel support, permissions, Windows receiver/driver compatibility, required transfer types, latency, and disconnect handling. Compare raw forwarding with local sensor parsing and compact samples as described in [architecture](../ARCHITECTURE.md). Do not finalize the transport from enumeration success alone.

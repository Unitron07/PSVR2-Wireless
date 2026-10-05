# Planned Android client

Reserved for implementation after [hardware bring-up](../docs/testing.md). No Android application, Gradle project, or modules exist yet.

| Proposed module | Responsibility |
| --- | --- |
| USB device discovery | Enumerate devices/descriptors, request permissions, track detach/reconnect |
| PSVR2 sensor parser | Decode verified packets, units, calibration, timestamps, coordinate frames |
| Network transport | Send tracking/input and receive video/control with measured latency |
| Video decoder | Investigate hardware codecs, buffers, and low-latency decode behavior |
| External display renderer | Discover modes and present decoded video on the headset display |
| Diagnostics UI | Export versioned reports; show USB/display/network/power limitations |

Start with descriptor and external-mode reporting, including permission-denied and disconnected states. Do not claim lane rate/DSC/FEC from ordinary mode listings; report inaccessible information explicitly. Access to all sensor interfaces and native headset timings is **TODO / VERIFY**. Root/kernel/vendor requirements are unresolved.

See [USB](../docs/usb.md), [DisplayPort](../docs/displayport.md), and [architecture](../ARCHITECTURE.md).

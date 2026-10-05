# Planned Windows host

Reserved for future implementation. No host executable, driver, SDK dependency, or build system exists yet.

| Proposed component | Responsibility |
| --- | --- |
| SteamVR driver / OpenXR runtime integration | Expose verified headset behavior to a selected VR runtime |
| Video capture/render integration | Obtain frames with correct stereo/pose association |
| Hardware encoder | Measure codec, bitrate, queueing, and encoding latency |
| Tracking receiver | Receive timestamped samples; handle clock mapping, loss, and prediction |
| Controller/input integration | Investigate actual connectivity and map verified inputs |
| Diagnostics | Record timing, network health, configuration, and recovery |

SteamVR device drivers and OpenXR application/runtime integration are distinct choices; the final integration boundary remains unresolved. The first host component should be a small measurement-oriented tracking receiver after Android sensor access is proven, before a full runtime driver.

See [architecture](../ARCHITECTURE.md), [roadmap](../ROADMAP.md), and [protocol goals](../protocol/README.md).

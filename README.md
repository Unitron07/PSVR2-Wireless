# PSVR2-Wireless

An experimental open-source project investigating wireless PC use of the PlayStation VR2 headset, with an Android phone as a wearable client and bridge.

> **Early research only. This project is NOT currently a finished wireless PSVR2 solution.** No working wireless VR prototype has been demonstrated by this project. This repository contains documentation and future implementation areas, with no application code or build system yet.

## Proposed architecture

A Windows gaming PC would send encoded video over Wi-Fi to a Samsung Galaxy S24. The phone would decode it and drive the headset through a USB-C dock and the official Sony PSVR2 PC Adapter. Tracking and input would return to the PC through Android.

```text
Windows gaming PC
       |
       | Wi-Fi (video down; tracking/input up)
       v
Galaxy S24
       |
       +-- USB-C dock/hub
              +-- native DisplayPort --> Sony adapter DP input
              +-- USB 3.x -----------> Sony adapter USB connection
              +-- USB-C PD <---------- Portable power bank

Portable power bank
       +-- regulated, verified supply --> Sony adapter DC IN

Sony PSVR2 PC Adapter
       +-- USB-C (display/data/power) --> PSVR2 headset
```

This is a proposed topology, not a validated wiring recipe. The Sony adapter keeps headset-side USB-C, DisplayPort, power, orientation handling, and USB behavior in existing hardware rather than requiring an initial custom board. Its presence does not guarantee compatibility with Android.

Sony documents direct PC DisplayPort and USB connections; the proposed phone/dock path is outside that supported configuration. See [research and sources](RESEARCH.md) and the [hardware plan](HARDWARE.md).

## Goals

- Establish whether the phone can drive a usable PSVR2 display mode while accessing its USB devices.
- Build measurement-based display, USB, network, tracking, and power diagnostics.
- Investigate low-latency video and timestamped sensor transport.
- Eventually integrate stereo rendering, tracking, and controls with PC VR runtimes.

## Non-goals for this stage

- A complete streaming system, installable client, or production VR driver.
- Guaranteed hardware compatibility, native VR timing, or latency targets.
- Replacing the Sony adapter with custom electronics.
- Promising eye tracking, foveation, or other untested capabilities.

## Current hardware target

PSVR2, official Sony PSVR2 PC Adapter, Galaxy S24, a USB-C dock with native DisplayPort and simultaneous USB 3.x, a DisplayPort cable, and portable regulated power. An Anker 565 / A8388 dock and roughly 90 Wh USB-C PD bank are candidates only; compatibility is **to be verified**. See [HARDWARE.md](HARDWARE.md) before selecting or connecting components.

## Status and development phases

Documentation bootstrap; no project hardware test results are recorded. All hardware and software milestones remain unverified.

| Phase | Focus |
| --- | --- |
| 0 | Repository structure, research, architecture, risks, references |
| 1 | Physical display and USB connection proof |
| 2 | Android USB and external-display diagnostics |
| 3 | Sensor parsing and Windows tracking receiver |
| 4 | Encoded video, Android decoding, external-display rendering |
| 5 | SteamVR/OpenXR integration, stereo geometry, prediction, controls |
| 6 | Latency, recovery, battery, and optional advanced-feature optimization |

The [roadmap](ROADMAP.md) defines experiments and evidence required for progress.

## Known blockers and unknowns

- Exact S24 output mode, lane allocation, HBR3, DSC, and FEC availability.
- Dock transparency and simultaneous DisplayPort/USB operation.
- Android access to every required USB interface and native headset display timing.
- Headset initialization and the split of tracking processing between headset, phone, and PC.
- End-to-end motion-to-photon latency and generic USB/IP viability.
- Regulated portable power delivery, real consumption, and battery runtime.

Ordinary DeX output, USB enumeration, and native VR operation are separate proof points. A successful desktop image alone would not establish working VR.

## Documentation and implementation areas

- [Architecture](ARCHITECTURE.md), [hardware](HARDWARE.md), [research](RESEARCH.md), [roadmap](ROADMAP.md).
- [Bring-up checklist](docs/testing.md), [USB](docs/usb.md), [DisplayPort](docs/displayport.md), [power](docs/power.md).
- Planned [Android client](android/README.md), [Windows host](windows/README.md), [wire protocol](protocol/README.md), and [diagnostic tools](tools/README.md).

## Reference projects

- [Swyter/psdaptwor](https://github.com/Swyter/psdaptwor): experimental PSVR2 adapter and hardware research.
- [unterschall/psvr2-linux-adapter](https://github.com/unterschall/psvr2-linux-adapter): USB, display, and runtime research to investigate independently.
- [OpenXR](https://www.khronos.org/openxr/) and [SteamVR/OpenVR](https://github.com/ValveSoftware/openvr): potential runtime integration references.
- [Sunshine](https://github.com/LizardByte/Sunshine) and [Moonlight](https://moonlight-stream.org/): possible early video-path experiments, not the final VR architecture.

References do not imply endorsement, affiliation, or demonstrated compatibility with this project.

## Contributing and license

Reproducible measurements, hardware reports, and carefully sourced research are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md); include exact versions, logs, and clear distinctions between observations and assumptions. Project contributions use the [MIT License](LICENSE). Referenced projects retain their own licenses.

This is an unofficial community project, unaffiliated with Sony, PlayStation, Samsung, Valve, or other hardware/software vendors. Trademarks belong to their respective owners.

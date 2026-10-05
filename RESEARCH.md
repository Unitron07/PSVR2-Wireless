# Research ledger

Initial source review: **2026-10-05**. No project hardware measurements exist. Vendor specifications establish only the stated model/configuration; upstream research is not independently validated here. Pin upstream commit/file references when adding experimental findings.

## Evidence vocabulary

| Label | Meaning |
| --- | --- |
| Confirmed specification | Vendor documentation, not a project test |
| Confirmed observation | Reproduced on identified hardware with attached evidence |
| Reported by reverse-engineering projects | External claim; project reproduction pending |
| Likely / inferred | Reasoned expectation; not measured |
| To be verified / TODO / VERIFY | Unresolved hypothesis or experiment |

## PSVR2 USB

**Reported by reverse-engineering projects:** PSVR2 carries DisplayPort and USB data over USB-C; [psdaptwor](https://github.com/Swyter/psdaptwor) investigates separating those paths and power.

**TODO / VERIFY:** capture actual device/interface/endpoint descriptors on Android, determine permission and transfer access, identify initialization, and measure useful sensor traffic. Enumeration alone does not prove reliable data access. Do not copy assumed endpoint numbers into implementation. See [USB plan](docs/usb.md).

## DisplayPort

**Research hypothesis / TODO / VERIFY:** a two-DP-lane plus USB SuperSpeed topology equivalent to USB-C DP Alt Mode Pin Assignment D is suggested by reverse-engineering discussions. The reviewed overview sources do not establish its exact applicability here; locate a precise code/capture reference and measure negotiation before treating it as a finding. Phone-to-dock and adapter-to-headset links must be distinguished.

**Reported by reverse-engineering projects:** [Linux adapter display notes](https://github.com/unterschall/psvr2-linux-adapter/blob/main/docs/display.md) describe DP 1.4, DSC/FEC enablement, and a reported VR display mode. **Likely / inferred:** high-bandwidth link features are central to native operation. This is not proof that the S24 can emit the required combination.

**TODO / VERIFY:** lane count, link rate/HBR3, DSC, FEC, EDID/timing, Android mode exposure, and native VR scanout. See [display test matrix](docs/displayport.md).

## Sony PC Adapter

**Confirmed specification:** Sony documents separate DP/USB/power connections and headset USB-C output in the [adapter manual](https://www.playstation.com/content/dam/global_pdc/en/corporate/support/manuals/psvr2-docs/ps-vr2-pc-adapter/EN_FR_AMER_PC_Adaper_Instruction_Man_Web.pdf). Its [published supply rating](https://direct.playstation.com/en-gb/buy-accessories/playstationvr2-pc-adaptor) is approximately 5.1 V / 2.8 A.

**Confirmed supported-setup restriction:** [Sony's PC guide](https://www.playstation.com/en-us/support/hardware/pc-prepare-ps-vr2/) calls for direct PC DP/USB, excludes USB hubs, and excludes DP over USB-C. The Android/dock plan is outside that supported configuration; these restrictions are not a measurement of this proposed topology.

**TODO / VERIFY:** interoperability, startup behavior, and regulated portable supply compatibility. The adapter remains part of the initial design to avoid rebuilding headset-side routing and negotiation.

## Android / Galaxy S24

**Confirmed specification:** [Samsung's S24 specifications](https://www.samsung.com/ie/business/smartphones/galaxy-s/galaxy-s24-onyx-black-128gb-sm-s921bzkdeub/) list USB 3.2 Gen 1 and DeX. Wired external-display/USB-C DP Alt Mode support is a starting point, not evidence of native PSVR2 operation.

**Likely / inferred:** USB 3.x should provide enough initial data capacity; actual throughput and interface access remain unmeasured.

**TODO / VERIFY:** wired native DP behavior for the exact regional variant, HBR3/DSC/FEC exposure, simultaneous USB, display mode selection, decoder-to-display timing, thermal throttling, and whether app APIs suffice or kernel/vendor support is required.

## USB-C hubs

**Design requirement:** native DP, simultaneous USB 3.x, PD input, and transparent handling of required display features. DP 1.4 branding alone is insufficient evidence.

**TODO / VERIFY:** Anker 565 / A8388 is one candidate; no compatibility claim is made. Inspect specifications, chipset/revision, actual negotiated links, DSC/FEC behavior, and power-role stability. See [hardware requirements](HARDWARE.md).

## Networking

**Design target:** Wi-Fi 6E or better; validate actual band availability. Compare UDP, QUIC, and custom transport for latency, congestion behavior, loss, and recovery. Sunshine/Moonlight may be useful for early video-path tests, not as a final VR design.

**TODO / VERIFY:** encode/decode/network/presentation budgets, cross-device clock mapping, motion-to-photon latency, and concurrent tracking/video performance.

## Tracking

**Reference only:** [psvr2-linux-adapter](https://github.com/unterschall/psvr2-linux-adapter) describes sensor and runtime work. Its capabilities must not be advertised as this project's capabilities.

**TODO / VERIFY:** available data, packet formats, calibration, on-device versus host processing, positional tracking needs, controller transport, and initialization dependencies. Compare USB/IP experimentation with local Android parsing and compact timestamped packets; no final protocol is selected.

Power draw and battery runtime are also **TODO / VERIFY**; see [power measurements](docs/power.md).

## References

- [psdaptwor](https://github.com/Swyter/psdaptwor) - experimental adapter research; upstream hardware licensing applies.
- [psvr2-linux-adapter](https://github.com/unterschall/psvr2-linux-adapter) - USB/display/runtime research; upstream software licensing applies.
- [OpenXR](https://www.khronos.org/openxr/) - potential application/runtime interface.
- [SteamVR/OpenVR](https://github.com/ValveSoftware/openvr) - potential driver integration reference.
- [Sunshine](https://github.com/LizardByte/Sunshine), [Moonlight](https://moonlight-stream.org/) - video-path experimentation references.
- [Android USB host documentation](https://developer.android.com/develop/connectivity/usb/host) - discovery and permission API reference to review before implementation.

Links imply neither endorsement nor affiliation. No upstream/vendor files or binaries are included.

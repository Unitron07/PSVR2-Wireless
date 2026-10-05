# Intended software architecture

**Design proposal only.** No component is implemented and no timing budget is established. Feasibility depends on the [hardware gates](HARDWARE.md) and [research unknowns](RESEARCH.md).

## Division of responsibilities

| Area | Windows host (planned) | Android client (planned) |
| --- | --- | --- |
| Video | Render/capture integration; low-latency hardware encoding | Hardware decoding; external-display presentation |
| Tracking | Receive samples; transform coordinates; prediction and runtime poses | USB discovery/access; parse and timestamp sensor data; forward samples |
| Input | Runtime controller/input integration | Discover accessible controls and forward events |
| Timing | Clock mapping, frame/pose association, synchronization | Capture/decode/presentation timestamps and diagnostics |
| Session | Capability negotiation, configuration, reconnect | Connection UI, permissions, thermal/power/display/USB health |

OpenXR is an application/runtime interface; it does not itself provide a generic headset driver. Investigate a SteamVR driver (OpenVR driver interfaces) and/or an OpenXR runtime integration separately. The concrete runtime and driver boundary is **TODO / VERIFY**.

## Video path

```text
PC GPU -> render/capture -> encoder -> Wi-Fi -> Android hardware decoder
       -> Android external-display renderer -> dock native DP
       -> Sony adapter -> PSVR2
```

Begin with an image/video-path proof. A desktop stream is not VR correctness: stereo layout, lens/display geometry, native timing, pose-to-frame association, and presentation control must be verified later. Android may not expose a suitable direct-display path through ordinary app APIs.

Sunshine/Moonlight may help isolate an early encode/network/decode experiment. Their use would not establish the final VR architecture or motion-to-photon performance.

## Tracking path

```text
PSVR2 sensors -> USB via Sony adapter/dock -> Android USB host
             -> sensor/tracking parser -> timestamped network samples
             -> Windows receiver -> pose processing/prediction
             -> SteamVR driver and/or OpenXR runtime integration
```

**TODO / VERIFY:** which data the headset actually exposes, how it initializes, whether pose processing happens on headset/Android/Windows, and whether camera processing is required. IMU samples alone do not establish positional tracking. Controller connectivity and transport require separate investigation; do not assume all controller traffic shares headset USB.

## USB/IP versus sensor transport

Generic USB/IP may be useful for exploratory forwarding and comparing behavior with a PC baseline. Android kernel support, permissions, endpoint transfer types, driver expectations, and timing must be measured.

For final latency-sensitive tracking, reading sensors locally and sending compact samples is a preferred hypothesis: it may reduce USB round trips and irrelevant traffic and make timestamps/drop handling explicit. It also requires correct parsing, initialization, calibration, and clock mapping. USB/IP could remain useful for some interfaces; no final choice is made.

## Networking and timing

Target Wi-Fi 6E or better initially, subject to actual device/AP/regional support. UDP, QUIC datagrams, and a custom transport are candidates; benchmark before selection. Separate tracking/control/video flows where beneficial, avoid stale tracking queues, and define reliable behavior for configuration and session state.

Measure capture, encode, network, decode, presentation, sensor, and pose-update stages. Cross-device one-way latency needs clock synchronization with uncertainty recorded. Establish end-to-end motion-to-photon measurements independently; network RTT alone cannot represent VR latency. See [protocol goals](protocol/README.md) and [testing](docs/testing.md).

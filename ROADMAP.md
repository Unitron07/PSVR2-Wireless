# Experimental roadmap

All tasks are unchecked until reviewed evidence supports completion. Documentation exists as an initial draft; Phase 0 is not claimed complete. Phases may overlap for independent experiments, but hardware feasibility gates streaming integration.

## Phase 0 - Repository / research

- [ ] Review architecture and initial repository structure.
- [ ] Document known hardware behavior with evidence labels.
- [ ] Collect and inspect reverse-engineering references.
- [ ] Review risks, unknowns, and reproducible test plan.

Evidence: reviewed documentation with source provenance and explicit unresolved claims.

## Phase 1 - Physical connection proof

- [ ] Establish a working supported wired-PC baseline.
- [ ] Test Galaxy S24 -> USB-C dock -> DP -> Sony adapter -> PSVR2.
- [ ] Determine whether the headset displays any Android/DeX output.
- [ ] Connect the adapter USB path to the S24; enumerate PSVR2 devices.
- [ ] Verify display and USB together; record negotiation and failures.

Evidence: exact setup, logs, display observations, descriptors, and repeatable connection steps. Any desktop image is only a display proof; failure is a useful result and may require revising hardware.

## Phase 2 - Diagnostics

- [ ] Create a basic Android diagnostics app.
- [ ] Enumerate devices, interfaces, endpoints, and permissions.
- [ ] Export USB descriptors without inventing interface identifiers.
- [ ] Inspect external displays/modes; report resolution and refresh rate.
- [ ] Investigate DP link state through Android/kernel interfaces where available.
- [ ] Measure relevant sensor USB traffic and document access limitations.

Evidence: sanitized diagnostic reports and captures; unavailable metrics labeled unavailable.

## Phase 3 - Tracking prototype

- [ ] Read accessible IMU/sensor data and identify packet formats.
- [ ] Validate units, coordinate frames, initialization, and timestamps.
- [ ] Forward timestamped samples to a small Windows receiver.
- [ ] Characterize latency, jitter, loss, duplicates, and clock uncertainty.
- [ ] Determine tracking-processing placement and USB/IP viability.

Evidence: independently validated parser samples and receiver measurements. Do not equate IMU forwarding with full 6DoF tracking.

## Phase 4 - Video prototype

- [ ] Stream a low-latency PC-rendered image/video to Android.
- [ ] Use Android hardware decoding.
- [ ] Render to the PSVR2 external display if hardware gates permit.
- [ ] Record encode/decode/presentation latency and sustained operation.

Evidence: video-path proof with settings and measurements; full VR correctness is deferred.

## Phase 5 - VR integration

- [ ] Select and implement SteamVR/OpenXR runtime integration boundary.
- [ ] Implement stereo rendering and validated lens/display geometry.
- [ ] Integrate pose prediction and frame/pose synchronization.
- [ ] Investigate and integrate controller input/connectivity.
- [ ] Select low-latency transport based on measurements.
- [ ] Measure end-to-end motion-to-photon latency and tracking accuracy.

Evidence: repeatable VR tests with correctness and latency limits documented.

## Phase 6 - Optimization

- [ ] Investigate eye tracking and foveation only if access is practical.
- [ ] Tune encoders and reduce network latency/jitter.
- [ ] Improve prediction and investigate reprojection.
- [ ] Measure and optimize battery, power, and thermals.
- [ ] Implement reconnect, disconnect, and recovery behavior.

Evidence: comparable before/after measurements and failure-recovery tests.

## Recommended next implementation task

After the [Phase 1 bring-up experiments](docs/testing.md), build a minimal Android diagnostics app that exports a versioned report of USB descriptors/access status and external display modes. Handle permission denial and disconnects; label DP link details unavailable when inaccessible. Defer streaming and drivers until this evidence supports the chosen hardware path.

# Hardware bring-up checklist

**No tests have been run by this project.** Use the [hardware plan](../HARDWARE.md) and [power guidance](power.md). Perform early checks on a bench before wearable use. Distinguish unsupported topology failures from a known-good supported PC baseline.

## Record the setup

- [ ] Record date, test ID, exact wiring, and intended experiment.
- [ ] Record PSVR2/adapter models and firmware where available.
- [ ] Record S24 model/region/chipset, Android, One UI, kernel, and build.
- [ ] Record dock revision, DP/USB cables and lengths, power supply/bank and output ratings.
- [ ] Record PC OS/GPU/driver/runtime and AP/band/channel if used.
- [ ] Identify unavailable version fields explicitly; do not guess.

## Power and baseline

- [ ] Inspect connections, connector polarity, ratings, and cable condition.
- [ ] Establish the supported wired PC setup using the supplied Sony supply.
- [ ] Power everything according to vendor instructions; start with appropriate regulated supplies.
- [ ] Avoid unsupported voltages on the headset or adapter; do not treat a PD trigger as verified regulation.
- [ ] Stop for overheating, unstable power, unexpected resets, or damaged connections.
- [ ] Validate any portable power path separately before headset use.

## Display independently

- [ ] Test S24/dock output on a known-good ordinary external display first.
- [ ] Attempt the proposed DP path to the Sony adapter/PSVR2, varying only one factor at a time.
- [ ] Inspect Android external display enumeration, active/supported modes, resolution, refresh rate, and presentation access.
- [ ] Record any visible Android/DeX image or failure; do not assume a desktop mode is available on the headset.
- [ ] Record EDID/link evidence where accessible; mark unavailable HBR3/DSC/FEC data as unknown.

Independent display testing may reveal a USB initialization dependency. If USB is needed to light the panel, record that dependency instead of assuming a dead DP path. See [DisplayPort](displayport.md).

## USB independently

- [ ] Connect the adapter USB path to the phone/dock and inspect enumeration without assuming the display is active.
- [ ] Inspect permission requests and device/interface/endpoint descriptors.
- [ ] Record negotiated speed where observable, denied access, kernel-bound interfaces, and errors.
- [ ] Save sanitized raw descriptors and diagnostic logs under an identified test ID.
- [ ] Record whether sensor traffic needs initialization or an active DP link.

See [USB capture plan](usb.md). Enumeration is not proof of usable sensor transfers.

## Both simultaneously

- [ ] Connect native DP and USB 3.x together with validated power.
- [ ] Repeat descriptor/display checks; look for lane/speed changes and resets.
- [ ] Observe stability, temperature, and sustained operation; record duration.
- [ ] Repeat connection/disconnection and cold-start checks; save failures.
- [ ] Record system draw separately from charging; do not infer battery runtime from capacity alone.

## Result record

```text
Test ID / date:
Hardware and software versions:
Topology / power source:
Steps / baseline:
Observed display mode / USB access:
Evidence file paths / timestamps:
Measurements (units, count, duration, uncertainty):
Failure / unavailable information:
Observation versus inference:
Next experiment:
```

Save logs before changing the setup. Keep local bulk captures out of Git by default; publish sanitized excerpts with provenance when useful. Later latency tests should distinguish RTT, one-way estimates with clock uncertainty, and directly measured motion-to-photon latency.

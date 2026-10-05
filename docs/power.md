# Power architecture and measurement

**Proposal only.** Portable electrical compatibility, consumption, and runtime are unverified.

```text
Portable bank -- USB-C PD --> dock --> phone / dock peripherals
Portable bank -- separately verified regulated supply --> Sony adapter DC IN
Sony adapter -- negotiated headset connection --> PSVR2
```

## Known values and candidates

| Item | Value / requirement | Status |
| --- | --- | --- |
| Sony adapter official supply | Approximately 5.1 V / 2.8 A | Confirmed vendor rating; not measured draw |
| Portable bank candidate | Roughly 90 Wh; 5 V / 3 A and higher PD profiles | Under consideration; no model validated |
| Combined load, conversion losses, runtime | Not measured | TODO / VERIFY |

Source: [Sony adapter specifications](https://direct.playstation.com/en-gb/buy-accessories/playstationvr2-pc-adaptor). The rated supply capacity is not the system's continuous power consumption.

## Bring-up requirements

- Use the supplied Sony supply for the initial bench baseline.
- Use appropriate regulated power; verify voltage, polarity, connector, current capacity, regulation, and stability under load before connecting a replacement supply.
- Do not blindly apply alternate voltages to the headset or Sony adapter. Higher bank PD profiles are for compatible negotiated loads, not permission to apply them to adapter DC IN.
- A 5 V / 3 A output rating does not establish equivalence to the official 5.1 V supply. A PD trigger alone does not prove safe regulation or connector compatibility.
- Verify the bank can power the dock/phone and adapter simultaneously without output renegotiation causing resets.
- Avoid unverified cable rewiring or bypassing headset-side power negotiation.

## Measurement plan

**TODO:** measure voltage/current and energy for each output, total bank draw, idle/load transitions, phone charging versus steady-state operation, temperatures, and disconnect/reconnect behavior. Record meter placement, accuracy, duration, display mode, network load, and battery state.

Estimate runtime only after measuring average load and usable energy: `runtime_hours = usable_energy_Wh / average_power_W`. Nominal 90 Wh capacity does not equal delivered energy; conversion losses, cutoff limits, and phone battery contribution must be recorded. Publish measured runtime separately from estimates.

See [hardware](../HARDWARE.md) and [testing](testing.md).

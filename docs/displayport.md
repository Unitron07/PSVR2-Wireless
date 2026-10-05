# DisplayPort feasibility

**No project display tests exist.** Native DP output from the phone is a hypothesis for this topology. DeX support or a dock's advertised resolution is not proof of native PSVR2 timing.

## Evidence and boundaries

Sony specifies DP 1.4 for supported PC use; its direct-connection restrictions are recorded in [research](../RESEARCH.md). [Linux reverse-engineering display notes](https://github.com/unterschall/psvr2-linux-adapter/blob/main/docs/display.md) report DSC/FEC needs. Reproduce independently before claiming compatibility.

The two-lane DP plus USB SuperSpeed / Pin Assignment D model is an unresolved research hypothesis needing a precise source and negotiation evidence. Phone-to-dock upstream allocation and adapter-to-headset allocation are separate links; do not infer one from the other.

## Experimental matrix

| Question | Evidence to seek | Current status |
| --- | --- | --- |
| DP lane count | Negotiated allocation on each relevant link; concurrent USB speed | TODO / VERIFY |
| Link rate | Actual trained rate, not advertised DP version | TODO / VERIFY |
| HBR3 | Source, dock, and sink capability plus successful negotiation | TODO / VERIFY |
| DSC | Capability and actual enablement; dock transparency | TODO / VERIFY |
| FEC | Capability and actual link enablement | TODO / VERIFY |
| Native PSVR2 timings | EDID, selected mode, scanout/refresh evidence | TODO / VERIFY |
| Android external modes | Display IDs, advertised/active modes, resolution, refresh rate | TODO / VERIFY |
| Presentation access | Ability to render to headset at required timing without unwanted composition/scaling | TODO / VERIFY |

## Planned procedure

1. Establish supported wired-PC and ordinary phone external-display baselines.
2. Follow [bring-up tests](testing.md) with the Sony supply initially.
3. Save available EDID/mode information; distinguish advertised, selected, and measured modes.
4. Inspect Android diagnostics and kernel/vendor link information where accessible. Standard display mode enumeration may not expose lane/rate/DSC/FEC details; report inaccessible fields as unavailable.
5. Test DP and USB separately and together, recording any initialization dependency.
6. Repeat with controlled cable/dock changes and record firmware/variant differences.

## Captured modes and link state

**TODO:** attach raw evidence with test ID, setup, capture method, active mode, and limitations. No native timing is prescribed until verified on this path.

A visible desktop frame proves only that tested mode. VR readiness additionally requires stereo layout, geometry, synchronization, suitable timing, and latency measurements.

# Prototype hardware

**Status:** proposed hardware topology; no combination below has been validated by this project. See [testing](docs/testing.md) for the bring-up sequence.

## Topology

```text
PC -- Wi-Fi --> Galaxy S24 -- USB-C --> dock
                                         +-- DisplayPort 1.4 target --> Sony adapter DP IN
                                         +-- USB 3.x ---------------> Sony adapter USB
Power bank -- USB-C PD ------------------> dock PD input
Power bank -- verified regulated output -----------------------------> adapter DC IN
Sony adapter -- headset USB-C cable --> PSVR2
```

The adapter combines separate video, USB, and external power connections into the headset connection. It is retained to handle headset-specific USB-C negotiation, routing/orientation, and power behavior without an initial custom board. Actual phone interoperability remains **to be verified**.

## Components

| Component | Role / desired requirements | Evidence / status |
| --- | --- | --- |
| PSVR2 | Headset display, sensors, audio, and controls | USB/display behavior requires capture on this setup |
| Sony PSVR2 PC Adapter | Separate DP, USB, DC power; headset USB-C output | Vendor-documented PC interface; Android use unverified |
| Samsung Galaxy S24 | Wearable decoder, external-display source, USB host | Samsung specifies DeX and USB 3.2 Gen 1; exact DP capabilities unverified |
| USB-C hub/dock | Phone upstream, native DP output, simultaneous USB 3.x, USB-C PD input | DP 1.4 preferred; HBR3/DSC transparency highly desirable; FEC behavior must be checked |
| Portable power bank | Power phone/dock and separately supply adapter through a verified regulated path | Roughly 90 Wh; 5 V / 3 A and higher PD profiles considered; no confirmed model/runtime |
| DisplayPort cable | Dock native DP output to adapter DP input | DP 1.4-capable target; record length/model and actual negotiated mode |
| USB cable / adapter USB lead | Dock downstream USB to Sony adapter USB connection | Preserve USB 3.x; do not assume charge-only cables work |

An **Anker 565 / A8388** is being investigated as one dock candidate. Compatibility is **NOT confirmed**. Marketing resolution or DP version alone does not prove the needed lane allocation, DSC/FEC support, or operation alongside USB SuperSpeed. Do not substitute an HDMI conversion or USB graphics path for the proposed native DP experiment.

The S24 USB 3.x specification suggests adequate initial data capacity (**inferred**), but enumeration, sustained throughput, Android API access, and simultaneous display operation all require tests. Record the exact S24 regional variant rather than generalizing from another chipset or firmware.

## Power and supported baseline

The [Sony adapter specifications](https://direct.playstation.com/en-gb/buy-accessories/playstationvr2-pc-adaptor) list its official supply at **5.1 V / 2.8 A**. A bank's 5 V / 3 A rating alone does not prove electrical compatibility, connector polarity, regulation, or simultaneous output capacity. Use the supplied Sony supply for the initial baseline; validate portable delivery separately under [power guidance](docs/power.md).

Sony's [PC preparation guide](https://www.playstation.com/en-us/support/hardware/pc-prepare-ps-vr2/) specifies direct PC DP and USB, excludes USB hubs, and states that DP over USB-C is incompatible with its supported setup. The proposed dock path is experimental, regardless of community reports elsewhere. Establish the supported wired PC baseline before interpreting Android failures.

Sources and unresolved claims are tracked in [RESEARCH.md](RESEARCH.md).

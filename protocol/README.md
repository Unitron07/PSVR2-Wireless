# Wire protocol design goals

**No protocol is finalized.** There are no assigned packet IDs, binary layouts, ports, transport dependencies, or compatibility promises.

- Low latency and bounded queues; avoid delivering stale tracking/video work.
- Explicit sample/frame timestamps, units, clock domains, and synchronization uncertainty.
- Sequence numbers for gap, duplicate, and reordering detection.
- Packet-loss tolerance appropriate to each stream; reliable configuration and session state where needed.
- Separate tracking, control, and video transport where measurement shows a benefit.
- Versioned packet format and capability negotiation before accepting incompatible peers.
- Defined disconnect/reconnect behavior, input validation, resource limits, and session identity.

**TODO / VERIFY:** compare UDP, QUIC datagrams, and custom transport; decide loss/retransmission policies, clock mapping, coordinate conventions, codec framing, and authentication appropriate to the deployment. No transport is selected yet.

Use captured sensor samples and a small Windows receiver to validate timing and loss behavior before defining a stable format. See [architecture](../ARCHITECTURE.md) and [Phase 3](../ROADMAP.md).

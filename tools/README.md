# Future diagnostic tools

This directory reserves space for useful tools; none are implemented yet.

- USB descriptor dumping and sanitized capture export.
- Latency measurement with explicit clock domains and uncertainty.
- Packet capture analysis for rate, loss, jitter, and ordering.
- Display-mode and available DP link-state diagnostics.

Keep tools small and tied to reproducible experiments. Include exact setup/version metadata, units, timestamps, and access limitations in reports. Avoid dependencies until a concrete tool needs them; do not add empty source files to fill this directory.

Use [testing](../docs/testing.md) for test records and [contribution guidance](../CONTRIBUTING.md) for evidence/provenance requirements.

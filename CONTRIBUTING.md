# Contributing

PSVR2-Wireless is experimental. Help establish feasibility before adding a large streaming stack. Start with the [roadmap](ROADMAP.md) and [bring-up checklist](docs/testing.md).

## Issues and research reports

Include hardware model/revision, phone region and chipset, Android/One UI/kernel/build versions, headset/adapter firmware where obtainable, dock revision, cable details, power supply, and network setup where relevant. Windows reports should include OS build, GPU/driver, and VR runtime versions.

Prefer measurements over expectations. Include reproducible steps, baseline setup, expected and observed outcomes, timestamps, units, sample counts, logs, and limitations. Report failures too. Separate:

- **Confirmed observation:** directly measured on the stated setup; attach evidence.
- **Confirmed specification:** published by the vendor; link the source and identify the model.
- **Reported by reverse-engineering projects:** externally reported; link the exact file/commit and do not claim project verification.
- **Likely/inferred:** explain the evidence and reasoning.
- **To be verified / TODO / VERIFY:** hypothesis or unanswered question.

Redact serial numbers, credentials, personal data, and unrelated device traffic from logs. Keep useful descriptor and timing information intact. Do not upload large raw captures by default; describe an appropriate sanitized excerpt first.

## Pull requests

Keep changes focused and explain the problem, resulting behavior, and validation. Use relative documentation links and concise technical Markdown. Do not mark roadmap items complete without supporting evidence. There is no build or test suite yet; documentation changes should check links, formatting, consistency, and claim provenance.

Discuss dependencies, privileged Android/kernel access, and runtime integration choices before committing to a large implementation. Future code should document permissions, disconnect handling, and measurements needed to evaluate it.

## Interoperability and provenance

Keep reverse-engineering work focused on interoperability. Do not submit proprietary Sony firmware/software, copyrighted binary blobs, extracted vendor assets, or materials you lack permission to distribute. Link public references instead. Preserve attribution and review upstream licenses before reusing code or hardware designs; this repository's MIT license does not relicense external work.

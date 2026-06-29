# Portfolio Notes

## Skills demonstrated

- Embedded firmware configuration with ZMK on Zephyr RTOS
- nRF52840 and nice!nano v2 platform planning
- Bluetooth Low Energy HID workflow design and validation
- Keyboard matrix, diode, keymap, and layer reasoning
- GitHub Actions-based firmware builds and artifact handling
- Structured hardware bring-up and evidence-driven testing
- Schematic capture, PCB layout, and BOM planning in Altium Designer
- Technical documentation that separates completed work from hardware-dependent claims
- Risk reduction through a focused MVP before a larger wireless 65% product

## How to present the project

### GitHub

- Keep the README status checklist aligned with actual evidence.
- Link each milestone to a dated development-log entry.
- Add selected images to `images/` with descriptive filenames and concise captions in the README or relevant document.
- Tag a release only after a firmware build has been flashed and tested on the stated hardware.
- Preserve build-critical ZMK paths so visitors can reproduce the CI workflow.

### Upwork

- Present the project as an embedded product-development workflow, not only as a keyboard customization.
- Lead with the validated path: firmware configuration, CI build, artifact generation, controller bring-up, BLE HID, matrix prototype, and PCB design.
- Explain how the 3x4 MVP reduces risk for the future 65% keyboard.
- Distinguish completed evidence from planned work. Avoid claiming BLE, battery, or PCB validation before the corresponding test passes.
- Use a short demonstration video and a compact architecture image as primary evidence, then link to the repository for implementation detail.

## Evidence checklist

- [ ] Screenshot of a successful GitHub Actions run, including commit and job result
- [ ] Screenshot of the downloadable firmware artifact and its filename
- [ ] Clear photos of the nice!nano v2 and controller wiring
- [ ] Video showing Bluetooth pairing and host-visible key events
- [ ] Video showing the wire-based matrix test across all twelve positions
- [ ] Screenshots of the Altium schematic with readable net and component labels
- [ ] 2D or 3D PCB render showing placement and board outline
- [ ] Photos of the assembled PCB when available
- [ ] Idle, active, and sleep current measurements when suitable equipment is available
- [ ] Development-log entries that map each item to a date, procedure, and result

Crop screenshots to remove unrelated account information, browser tabs, device identifiers, or secrets before publishing them.


# Wireless Macropad MVP

Wireless Macropad MVP is a 3x4 wireless mechanical macropad built as a focused ZMK and Zephyr RTOS bring-up platform. It uses the existing `boardsource3x4` shield configuration with a nice!nano v2-compatible nRF52840 target and produces firmware through GitHub Actions.

## Project objective

The MVP validates the complete development path before committing to a custom wireless 65% keyboard: firmware configuration, automated builds, bootloader flashing, Bluetooth HID, switch-matrix behavior, keymaps, layers, and basic power behavior. The smaller matrix keeps hardware bring-up and fault isolation manageable while the same engineering lessons feed directly into the future 65% design.

## Technical stack

- ZMK firmware
- Zephyr RTOS
- nice!nano v2 / Nordic nRF52840
- Bluetooth Low Energy HID
- 3x4 keyboard matrix (`boardsource3x4` shield)
- GitHub Actions firmware builds
- Altium Designer for the planned custom PCB

## Current status

- [x] ZMK configuration created
- [x] GitHub Actions build working
- [x] Firmware artifact generated
- [ ] nice!nano v2 acquired
- [ ] Firmware flashed to hardware
- [ ] BLE pairing validated
- [ ] Matrix wiring tested
- [ ] Custom PCB designed

Hardware-dependent items remain pending because the nice!nano v2 has not been acquired.

## Roadmap

### Phase 1 — Firmware baseline

- Create the ZMK user configuration.
- Build the `boardsource3x4` shield for the configured nice!nano v2 target.
- Confirm that GitHub Actions publishes the firmware artifact.

### Phase 2 — Controller bring-up

- Acquire the nice!nano v2.
- Flash the generated UF2 firmware.
- Verify USB-powered startup and BLE pairing.

### Phase 3 — Matrix prototype

- Wire a diode-protected 3x4 switch matrix by hand.
- Validate every key position, keymap binding, and layer transition.
- Check USB, battery, sleep, and wake behavior.

### Phase 4 — Macropad PCB

- Capture the schematic in Altium Designer.
- Lay out, review, manufacture, and assemble the custom macropad PCB.
- Repeat firmware, matrix, BLE, and power validation on the PCB.

### Phase 5 — Wireless 65% keyboard

- Reuse the validated firmware workflow and hardware lessons.
- Define the 65% matrix, power architecture, schematic, and PCB.
- Prototype and validate the complete keyboard.

## Repository structure

```text
.
|-- .github/workflows/      GitHub Actions firmware build
|-- config/                 ZMK keymap, configuration, and west manifest
|-- docs/                   Architecture, test plan, log, and portfolio notes
|-- firmware_notes/         Hardware bring-up observations and firmware notes
|-- hardware/
|   |-- bom/                Bill of materials
|   |-- pcb/                Future Altium PCB outputs
|   `-- schematic/          Future Altium schematic outputs
|-- images/                 Portfolio screenshots, photos, and renders
|-- build.yaml              ZMK build matrix
`-- README.md
```

`config/`, `build.yaml`, and `.github/workflows/build.yml` are build-critical. Their names and locations should remain unchanged unless the ZMK build contract is deliberately updated.

## Build firmware with GitHub Actions

The repository uses `.github/workflows/build.yml`, which calls ZMK's reusable user-config build workflow.

1. Push a commit that changes `config/`, `build.yaml`, or the build workflow, or open the repository's **Actions** tab.
2. Select **Build ZMK firmware**.
3. For a manual build, choose **Run workflow**, select the branch, and confirm.
4. Wait for the build job to finish successfully.

The active target is defined in `build.yaml`. This project intentionally preserves the currently working board and shield values.

## Download the firmware artifact

1. Open the successful **Build ZMK firmware** workflow run.
2. Scroll to **Artifacts** on the run summary page.
3. Download the firmware artifact ZIP.
4. Extract the ZIP and identify the `.uf2` file produced for the configured target.

Keep generated firmware artifacts out of Git; they can be downloaded from the corresponding workflow run when needed.

## Flash the nice!nano v2

Perform these steps after the controller is available:

1. Connect the nice!nano v2 with a USB-C cable that supports data.
2. Enter the UF2 bootloader, normally by pressing reset twice in quick succession.
3. Confirm that a removable bootloader drive appears on the host computer.
4. Copy the extracted `.uf2` file to that drive.
5. Wait for the controller to reboot automatically.
6. Pair the macropad from the host's Bluetooth settings and validate the keymap.

If the bootloader drive does not appear, stop and verify the cable, controller documentation, and bootloader state before attempting recovery. Do not flash a file built for a different board target.

## MVP scope

This macropad is a controlled validation platform for firmware, BLE HID, matrix scanning, and the development workflow. It reduces bring-up risk before the larger wireless 65% keyboard introduces a bigger matrix, a custom PCB, battery integration, and broader mechanical constraints.

## Documentation

- [Architecture](docs/architecture.md)
- [Testing plan](docs/testing_plan.md)
- [Development log](docs/development_log.md)
- [Portfolio notes](docs/portfolio_notes.md)
- [Hardware plan](hardware/README.md)
- [Bill of materials](hardware/bom/macropad_bom.csv)


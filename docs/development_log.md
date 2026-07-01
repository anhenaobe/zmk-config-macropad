# Development Log

Use this file to preserve decisions and observable evidence. Add one entry per meaningful change or test result.

## Entry template

### YYYY-MM-DD — Short title

- **Date:** YYYY-MM-DD
- **Change:** What changed.
- **Reason:** Why the change was needed.
- **Result:** What was observed, including links to evidence when available.
- **Next step:** The next concrete action.

---

## Initial project history

### Date not recorded — ZMK CLI project created

- **Date:** Not recorded
- **Change:** Created the ZMK user-configuration project and generated the `config/` files.
- **Reason:** Establish a reproducible firmware baseline for the wireless macropad MVP.
- **Result:** The repository contains the ZMK keymap, configuration, and west manifest.
- **Next step:** Select the MVP shield and controller target.

### Date not recorded — boardsource3x4 selected as MVP shield

- **Date:** Not recorded
- **Change:** Selected `boardsource3x4` as the 3x4 macropad shield.
- **Reason:** Use a small matrix to validate the ZMK workflow before developing the custom 65% keyboard.
- **Result:** The shield is declared in `build.yaml`, and matching configuration files exist in `config/`.
- **Next step:** Select the controller target.

### Date not recorded — nice!nano v2 selected as controller

- **Date:** Not recorded
- **Change:** Selected the nice!nano v2 / nRF52840 family as the wireless controller target.
- **Reason:** Provide BLE HID capability in a Pro Micro-compatible form factor suitable for keyboard prototyping.
- **Result:** The current board target is declared in `build.yaml`. Hardware compatibility was later validated with a pin-compatible Pro Micro nRF52840.
- **Next step:** Configure the automated firmware build.

### Date not recorded — GitHub Actions firmware build configured

- **Date:** Not recorded
- **Change:** Added the **Build ZMK firmware** workflow using ZMK's reusable user-config build workflow.
- **Reason:** Make firmware generation repeatable and independent of a local Zephyr toolchain.
- **Result:** GitHub Actions completes the firmware build successfully.
- **Next step:** Download and inspect the generated artifact.

### Date not recorded — Firmware ZIP downloaded successfully

- **Date:** Not recorded
- **Change:** Downloaded the firmware artifact ZIP from a successful GitHub Actions run.
- **Reason:** Confirm that the CI output is accessible for future flashing.
- **Result:** The artifact download path was validated. The generated UF2 was later flashed successfully to a pin-compatible Pro Micro nRF52840.
- **Next step:** Execute and document controller bring-up and matrix validation.

### Date not recorded — Pro Micro nRF52840 hardware validation completed

- **Date:** Not recorded
- **Change:** Flashed the generated nice!nano v2-compatible UF2 firmware to a Pro Micro nRF52840 and manually tested all twelve positions of the `boardsource3x4` matrix.
- **Reason:** Validate the complete 3x4 proof-of-concept path on real hardware before designing a larger or custom shield.
- **Result:** The controller advertised over Bluetooth as `boardsource3x4`, paired successfully with the host, and produced the expected `1`, `2`, `3`, `4`, `Q`, `W`, `E`, `R`, `A`, `S`, `D`, and `SPACE` outputs in Notepad. Each position was tested individually with a diode in the configured `col2row` direction: column to anode, row to cathode, with the diode stripe toward `ROW`. All twelve single-key tests passed.
- **Limitation:** Multi-key rollover and simultaneous keypress behavior remain pending because only one diode was available during the test. The recorded evidence does not yet establish ghosting or masking behavior for concurrent inputs.
- **Next step:** Assemble enough diode-protected positions to test representative simultaneous FPS key combinations while preserving the current 3x4 proof-of-concept scope.

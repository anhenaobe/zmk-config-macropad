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
- **Result:** The current board target is declared in `build.yaml`; physical controller validation remains pending.
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
- **Result:** The artifact download path was validated; flashing remains pending until the nice!nano v2 is available.
- **Next step:** Acquire the controller, record the exact artifact filename, and execute the bootloader flashing test.


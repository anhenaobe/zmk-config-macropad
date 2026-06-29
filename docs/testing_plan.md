# Testing Plan

Statuses use **Passed**, **Failed**, **Blocked**, or **Not started**. A test should move to **Passed** only when its expected result has been observed and the evidence has been recorded in `docs/development_log.md`.

## 1. Firmware build test

- **Objective:** Confirm that the committed ZMK configuration compiles for the board and shield declared in `build.yaml`.
- **Procedure:** Run the **Build ZMK firmware** GitHub Actions workflow and inspect the reusable ZMK build job for errors or warnings that require action.
- **Expected result:** The workflow completes successfully and proceeds to artifact packaging for the configured target.
- **Status:** Passed — the current configuration has built successfully in GitHub Actions.

## 2. Firmware artifact download test

- **Objective:** Confirm that the generated firmware can be retrieved from a completed CI run.
- **Procedure:** Open a successful workflow run, download its artifact ZIP, extract it, and verify that it contains the expected `.uf2` firmware file.
- **Expected result:** The ZIP downloads without corruption and exposes a UF2 file for the configured target.
- **Status:** Passed — a firmware ZIP has been downloaded successfully.

## 3. Bootloader flashing test

- **Objective:** Verify that the nice!nano v2 accepts and starts the generated firmware.
- **Procedure:** Connect the controller with a data-capable USB cable, enter the UF2 bootloader, copy the target `.uf2` file to the bootloader drive, and observe the reboot.
- **Expected result:** The file transfer completes, the bootloader drive disconnects, and the controller restarts without returning immediately to the bootloader.
- **Status:** Blocked — nice!nano v2 not yet available.

## 4. BLE pairing test

- **Objective:** Verify Bluetooth advertising, pairing, reconnection, and HID transport.
- **Procedure:** Flash the firmware, select a clean Bluetooth profile if needed, pair from the host, press representative keys, power-cycle the controller, and verify reconnection.
- **Expected result:** The host pairs successfully, receives the intended HID events, and reconnects after a power cycle.
- **Status:** Blocked — controller hardware and flashing are pending.

## 5. Matrix short test using wires

- **Objective:** Validate each logical matrix position before installing all switches or designing the PCB.
- **Procedure:** With the powered controller secured against accidental shorts, momentarily bridge only the documented row and column pair for each position using insulated jumper wires. Record the host-visible output for all twelve positions.
- **Expected result:** Every row/column pair produces exactly the binding assigned to its keymap position, with no adjacent or repeated phantom events.
- **Status:** Blocked — controller and manual matrix wiring are pending.

## 6. Keymap validation test

- **Objective:** Verify that every binding in the default layer matches the intended action.
- **Procedure:** Exercise all twelve physical or wire-simulated positions and compare host-visible output with `config/boardsource3x4.keymap`, including media keys and arrow keys.
- **Expected result:** Every position produces its documented key or consumer-control action exactly once per actuation.
- **Status:** Blocked — matrix hardware is pending.

## 7. Layer test

- **Objective:** Verify toggle, momentary, and layer-tap behavior across all configured layers.
- **Procedure:** Exercise the layer controls and then test every reachable position on the number, lower, and raise layers. Verify return to the default layer after momentary controls are released.
- **Expected result:** Each layer activates by its configured behavior, exposes the expected bindings, and returns or toggles predictably without trapping the device on an unintended layer.
- **Status:** Blocked — matrix hardware is pending.

## 8. USB powered test

- **Objective:** Verify stable startup and operation while powered from USB.
- **Procedure:** Connect the flashed controller through a known-good USB data cable, repeat several cold starts and resets, and exercise representative keys over BLE.
- **Expected result:** The controller starts consistently, remains connected, and processes keys without resets or intermittent behavior.
- **Status:** Blocked — controller hardware and flashing are pending.

## 9. Battery powered test

- **Objective:** Verify safe and stable operation from the intended 3.7 V LiPo battery and power switch.
- **Procedure:** After confirming battery polarity and connector compatibility, connect the battery with USB disconnected, switch the device on, pair it, and exercise the full matrix.
- **Expected result:** The controller starts and operates reliably from battery power with no unexpected heating, resets, or disconnects.
- **Status:** Blocked — controller, battery integration, and flashing are pending.

## 10. Sleep and power behavior test

- **Objective:** Verify idle, sleep, wake, and reconnect behavior and collect power evidence when measurement equipment is available.
- **Procedure:** Pair the battery-powered device, leave it idle through the configured power-management intervals, observe connection state and current if possible, then press a key to wake it.
- **Expected result:** The device enters the expected low-power state, wakes from a key event, reconnects when required, and resumes correct HID input without a manual reset.
- **Status:** Blocked — complete battery-powered hardware is pending.


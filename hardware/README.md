# MVP Hardware

## Target

The hardware target is a twelve-key wireless macropad built around a nice!nano v2-compatible nRF52840 controller and the `boardsource3x4` ZMK shield configuration. The electrical prototype uses MX-compatible switches, one 1N4148 diode per switch, a 3x4 row/column matrix, and optional 3.7 V LiPo battery power after USB-powered bring-up succeeds.

The repository configuration remains the source of truth for firmware compatibility. Pin assignments and diode direction must be confirmed against the selected shield and controller documentation before wiring or schematic capture.

## Manual prototype

Initial validation will use manual wiring on a breadboard or prototyping board. This stage isolates controller flashing, BLE HID, matrix positions, keymap behavior, and power operation before PCB-specific faults are possible.

Bring-up order:

1. Inspect the controller and verify the USB data cable.
2. Flash and test the controller over USB power with no matrix attached.
3. Validate matrix positions with controlled row/column wire shorts.
4. Add switches and diodes, then repeat the complete keymap and layer tests.
5. Add battery power only after polarity, connector compatibility, and power-switch wiring are verified.

## Altium PCB phase

After the manual prototype passes, the schematic and PCB will be designed in Altium Designer. The design should capture the proven matrix topology, diode orientation, controller socket footprint, power switch, battery connection, mechanical switch footprints, mounting constraints, and accessible reset/bootloader operation.

Source design files should live in `hardware/schematic/` and `hardware/pcb/`. Manufacturing exports should be clearly separated from editable Altium sources when they are added.

## Relationship to the wireless 65% keyboard

The completed macropad PCB is an intermediate engineering stage for the planned wireless 65% keyboard. It validates the controller, firmware workflow, BLE behavior, matrix design rules, battery integration, fabrication outputs, and assembly process at lower cost and complexity. Those validated contracts can then be scaled deliberately rather than rediscovered during the 65% build.


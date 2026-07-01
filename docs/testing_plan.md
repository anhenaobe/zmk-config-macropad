# 3x4 Macropad Testing Plan

## Objective and validation status

This plan validates the **3x4 proof of concept** using the ZMK firmware generated for `nice_nano//zmk@2` and the `boardsource3x4` shield. Hardware validation was completed successfully with a Pro Micro nRF52840 that is pin-compatible with the nice!nano v2.

The generated UF2 firmware artifact was flashed to the controller, the Bluetooth device appeared as `boardsource3x4`, and BLE pairing completed successfully. All twelve single-key matrix coordinates produced the expected FPS key output in Notepad when tested with a diode between the corresponding column and row pins.

The current scope remains limited to the existing 3x4 matrix. It does not include changing the layout, creating a custom 4x5 or Valorant shield, or validating a final PCB.

## Validation setup

The validation used:

- Pro Micro nRF52840, confirmed pin-compatible with the nice!nano v2;
- USB-C data cable;
- generated `.uf2` firmware artifact for the configured target;
- one diode and jumper wires for manual matrix bridging;
- Bluetooth-capable host;
- Notepad for observing the received key output.

## Bring-up results

| Test | Procedure | Acceptance criterion | Result |
|---|---|---|---|
| UF2 flashing | Enter the controller bootloader and copy the generated `.uf2` file. | The file transfer completes and the controller starts the firmware. | OK |
| BLE advertising | Scan for the controller from the host. | A Bluetooth device named `boardsource3x4` appears. | OK |
| BLE pairing | Pair the `boardsource3x4` device with the host. | Pairing completes and the controller exposes HID keyboard input. | OK |
| 3x4 single-key matrix | Perform all twelve diode-assisted bridges listed below. | Each coordinate produces its expected key in Notepad. | OK |
| Multi-key rollover | Press or bridge multiple matrix positions simultaneously. | Every simultaneous keypress is reported correctly without ghosting or masking. | Pending |

BLE reconnection after a controller or host power cycle was not part of the recorded validation and remains pending.

## Diode orientation

The manual matrix test used a diode in the shield's configured `col2row` direction:

- column side to diode anode;
- row side to diode cathode;
- diode stripe, which marks the cathode, toward `ROW`.

Only one diode was available, so each coordinate was tested individually. The results establish correct single-key matrix scanning and keymap position mapping, but they do not establish multi-key rollover behavior.

## Single-key matrix results

With the firmware running and BLE connected, each specified column and row pair was connected through the correctly oriented diode. One coordinate was tested at a time, and the output was observed in Notepad.

| Key | Coordinate | Physical bridge | Expected output | Result |
|---|---|---|---|---|
| K1 | RC(0,0) | P1.15 ↔ P0.09 | 1 | OK |
| K2 | RC(0,1) | P1.15 ↔ P0.10 | 2 | OK |
| K3 | RC(0,2) | P1.15 ↔ P1.11 | 3 | OK |
| K4 | RC(0,3) | P1.15 ↔ P1.13 | 4 | OK |
| K5 | RC(1,0) | P0.02 ↔ P0.09 | Q | OK |
| K6 | RC(1,1) | P0.02 ↔ P0.10 | W | OK |
| K7 | RC(1,2) | P0.02 ↔ P1.11 | E | OK |
| K8 | RC(1,3) | P0.02 ↔ P1.13 | R | OK |
| K9 | RC(2,0) | P0.29 ↔ P0.09 | A | OK |
| K10 | RC(2,1) | P0.29 ↔ P0.10 | S | OK |
| K11 | RC(2,2) | P0.29 ↔ P1.11 | D | OK |
| K12 | RC(2,3) | P0.29 ↔ P1.13 | SPACE | OK |

## Validation conclusion

The 3x4 proof of concept has been successfully validated on real hardware. The Pro Micro nRF52840 accepted the nice!nano v2-compatible ZMK firmware, advertised and paired over BLE as `boardsource3x4`, and resolved every single-key `ROW/COL` coordinate to the expected FPS key.

The remaining matrix-specific test is simultaneous keypress and multi-key rollover validation using enough diodes to connect multiple positions at the same time. This must be completed before drawing conclusions about rollover, ghosting, or masking under gaming input combinations.

## Evidence record

The observed hardware results are recorded in `docs/development_log.md`. Future testing should record the firmware artifact, host, test date, simultaneous key combinations, observed output, and any ghosting or masking behavior.

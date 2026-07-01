# 3x4 Matrix Pinout

## Scope

This document records the logical and physical mapping of the ZMK **3x4 proof of concept** based on the `boardsource3x4` shield and the nice!nano v2 pinout. The active configuration uses the `nice_nano//zmk@2` target, a three-row by four-column matrix, and the FPS keymap defined in `config/boardsource3x4.keymap`.

The mapping was validated with a Pro Micro nRF52840 confirmed to be pin-compatible with the nice!nano v2. This proof of concept does not define a new shield or modify the layout. The `pro_micro` names belong to the pin abstraction used by the shield; the **nRF52840 GPIO** column identifies the corresponding physical GPIO.

## Logical matrix and FPS keymap

The matrix is read by rows, from left to right:

```text
           COL0       COL1       COL2       COL3
ROW0    K1 / 1     K2 / 2     K3 / 3     K4 / 4
ROW1    K5 / Q     K6 / W     K7 / E     K8 / R
ROW2    K9 / A    K10 / S    K11 / D    K12 / SPACE
```

| Key | Coordinate | Row | Column | Expected key |
|---|---|---|---|---|
| K1 | RC(0,0) | ROW0 | COL0 | 1 |
| K2 | RC(0,1) | ROW0 | COL1 | 2 |
| K3 | RC(0,2) | ROW0 | COL2 | 3 |
| K4 | RC(0,3) | ROW0 | COL3 | 4 |
| K5 | RC(1,0) | ROW1 | COL0 | Q |
| K6 | RC(1,1) | ROW1 | COL1 | W |
| K7 | RC(1,2) | ROW1 | COL2 | E |
| K8 | RC(1,3) | ROW1 | COL3 | R |
| K9 | RC(2,0) | ROW2 | COL0 | A |
| K10 | RC(2,1) | ROW2 | COL1 | S |
| K11 | RC(2,2) | ROW2 | COL2 | D |
| K12 | RC(2,3) | ROW2 | COL3 | SPACE |

`RC(row,col)` represents the matrix position resolved by ZMK. For example, `K7` corresponds to `RC(1,2)`, the intersection of `ROW1` and `COL2`, and must produce `E` on the FPS layer.

## Validated signal mapping

| Signal | Pro Micro pin | nice!nano v2 pin / nRF52840 GPIO | Purpose |
|---|---:|---|---|
| ROW0 | 18 | P1.15 | Row 0 |
| ROW1 | 19 | P0.02 | Row 1 |
| ROW2 | 20 | P0.29 | Row 2 |
| COL0 | 10 | P0.09 | Column 0 |
| COL1 | 16 | P0.10 | Column 1 |
| COL2 | 14 | P1.11 | Column 2 |
| COL3 | 15 | P1.13 | Column 3 |

For example, the complete resolution chain is `K1 -> RC(0,0) -> ROW0/COL0 -> pro_micro 18/10 -> P1.15/P0.09`.

## Diode direction

The shield declares the diode direction as `col2row`. The intended electrical orientation is therefore **column to row**: the diode anode connects to the column side and the cathode connects to the row side. This orientation must be preserved in the hand-wired prototype and any future PCB so that matrix scanning matches the shield configuration.

For the completed manual test, the diode stripe marked the cathode and faced `ROW`:

- `COL` → diode anode;
- diode cathode/stripe → `ROW`.

## Hardware validation summary

The pin mapping and all twelve single-key coordinates were successfully validated with the Pro Micro nRF52840. The generated UF2 firmware ran on the controller, BLE pairing succeeded under the device name `boardsource3x4`, and every diode-assisted `ROW/COL` bridge produced the expected FPS key in Notepad.

This result validates pin compatibility and single-key matrix behavior for the 3x4 proof of concept. Multi-key rollover and simultaneous keypress behavior remain pending because only one diode was available during the test. No custom 4x5 or Valorant shield is introduced at this stage.

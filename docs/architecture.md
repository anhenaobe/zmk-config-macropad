# System Architecture

## Block diagram

```text
+------------+    +---------------+    +-----------+    +--------------------+
| User input | -> | Switch matrix | -> | GPIO scan | -> | ZMK key processing |
+------------+    +---------------+    +-----------+    +----------+---------+
                                                                  |
                                                                  v
                                                     +------------+---------+
                                                     | BLE HID report       |
                                                     +------------+---------+
                                                                  |
                                                                  v
                                                     +------------+---------+
                                                     | Host computer        |
                                                     +----------------------+
```

System flow: **User input -> Switch matrix -> GPIO scan -> ZMK key processing -> BLE HID report -> Host computer**

## Block responsibilities

### User input

The user presses or releases a mechanical switch. This is the physical event that begins the input path.

### Switch matrix

The 3x4 matrix organizes twelve switches as row and column connections. Diodes provide a defined current direction and help prevent ghosting when multiple keys are pressed.

### GPIO scan

The controller drives and samples the matrix GPIO lines. ZMK's matrix scanner detects state transitions and applies its configured debounce behavior before reporting key events.

### ZMK key processing

ZMK maps each matrix position through `config/boardsource3x4.keymap`. Behaviors such as key presses, layer changes, Bluetooth profile selection, reset, and bootloader entry are resolved here.

### BLE HID report

For wireless operation, ZMK encodes the resolved input as a Bluetooth Low Energy HID report. The nRF52840 radio sends the report to the paired host.

### Host computer

The operating system receives the HID report and exposes it to applications as keyboard or consumer-control input. The host is the final observable boundary for end-to-end validation.

## Why validate with a macropad first

A 3x4 macropad exercises the same essential firmware and hardware interfaces as the planned wireless 65% keyboard while using fewer switches, traces, GPIO relationships, and mechanical parts. Matrix faults can be isolated one row or column at a time, BLE and bootloader behavior can be validated independently of a large PCB, and the GitHub Actions workflow can be proven before the design cost increases. The resulting test evidence and design decisions become inputs to the 65% architecture rather than assumptions made during the larger build.


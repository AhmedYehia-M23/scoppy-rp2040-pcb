# Board Assembly, Bring-Up and USB Debugging

## Assembly

After PCB fabrication, I assembled and hand-soldered the complete board, including the RP2040, USB-C interface, external flash, power circuitry, analog-front-end parts and passives.

## Initial symptom

The board powered up but did **not enumerate as a USB device**, including attempts to enter BOOTSEL mode.

## Bring-up sequence

| Check | Result / conclusion |
| --- | --- |
| 5 V input rail | Present |
| 3.3 V rail | Present |
| RP2040 1.1 V core rail | Present |
| RUN / BOOTSEL state | Checked during fault isolation |
| External-flash related circuitry | Checked |
| USB-C CC configuration | Checked |
| D+ / D- path | Continuity checked through the USB interface path |
| D+ / D- short | No short identified during the checks |
| RP2040 grounding / exposed pad | Inspected |
| 12 MHz crystal network | Investigated as a possible USB-startup cause |
| Physical MCU solder contact | Fault found |

The troubleshooting order was deliberately **power first, then boot/reset state, USB connectivity, grounding, clock and finally package-level assembly inspection**.

## Isolation work

During the investigation I desoldered the USB connector to isolate the USB section and continue checking the board independently of the connector assembly.

## Root cause

The final fault was an **assembly/soldering defect at the RP2040**. The MCU was not making complete electrical contact with the PCB.

## Resolution

Correcting the RP2040 solder/contact problem restored **USB enumeration**.

The important result is therefore not just that the board eventually worked, but that the failure was reduced from a broad digital symptom — "USB not detected" — to a physical assembly defect using measurements and continuity checks rather than random component replacement.

## Evidence boundary

This repository documents the diagnostic sequence and the resolved fault. It does not currently include oscilloscope captures, exact measured rail values or a USB-enumeration screenshot from the original bring-up session, so none are reconstructed after the fact.

If the board is characterized again, useful additions would be:

- measured 5 V, 3.3 V and 1.1 V rail values
- 12 MHz oscillator capture
- BOOTSEL / USB-enumeration screenshot
- assembled-board photographs
- basic analog-input functional measurements

## Main takeaway

The project covered the complete physical PCB workflow:

**layout → fabrication → manual assembly → bring-up → measurement → fault isolation → repair**

It also reinforced a practical debugging rule: a high-level symptom such as failed USB enumeration can still originate from a basic package-level soldering fault.

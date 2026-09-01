# Board Assembly, Bring-Up and USB Debugging

## Assembly

After PCB fabrication, I **assembled and hand-soldered all components on the board myself**. This included the RP2040, USB-C interface components, power circuitry, external flash, analog-front-end components and the remaining passive/support circuitry.

## Symptom

After assembly, the RP2040 board powered up but did **not enumerate as a USB device** on the computers used for testing, including attempts to enter BOOTSEL mode.

## Diagnostic Approach

I worked through the board from power and physical connectivity toward the USB/clock circuitry:

1. **Power validation**
   - Verified the main 5 V input rail.
   - Verified 3.3 V regulation.
   - Verified the RP2040 1.1 V core rail.

2. **RP2040 basic-state checks**
   - Checked RUN level and BOOTSEL behavior.
   - Checked external-flash related circuitry.

3. **USB-C path checks**
   - Verified the USB-C CC resistor values/configuration.
   - Checked the D+ and D- series path.
   - Performed continuity measurements from the connector through protection/filtering components to the RP2040 USB pins.
   - Checked that D+ and D- were not shorted.

4. **Grounding and assembly inspection**
   - Inspected the RP2040 package and ground/exposed-pad connections.
   - Rechecked solder joints and physical contact around the MCU.

5. **Clock checks**
   - Investigated the 12 MHz crystal and its load-capacitor network as a possible cause of failed USB startup.

6. **Isolation step**
   - Desoldered the USB connector during the investigation to isolate the USB section and continue the physical fault search.

## Root Cause

The final root cause was an **assembly/soldering defect at the RP2040**: the MCU was not making complete electrical contact with the PCB.

## Resolution

Correcting the RP2040 solder/contact problem resolved the USB-enumeration issue.

## What I Learned

The project provided experience across the complete physical PCB workflow: **layout -> fabrication -> manual assembly/soldering -> bring-up -> measurement -> fault isolation -> repair**.

The debugging process also reinforced that a digital symptom such as "USB not detected" can originate from a basic physical assembly fault. A structured bring-up sequence proved useful:

**power -> reset/boot state -> signal continuity -> grounding -> clock -> physical assembly**

It also provided practical experience using voltage and continuity measurements to eliminate possible causes rather than replacing parts at random.

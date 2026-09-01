# Custom RP2040 Mixed-Signal Measurement PCB

**4-layer RP2040 hardware · KiCad · mixed-signal PCB layout · USB-C · hand assembly · hardware bring-up**

A university PCB-layout and hardware-bring-up project based on **professor-provided electrical schematics** for a custom RP2040 measurement board associated with the Scoppy oscilloscope ecosystem. My responsibility was the **PCB implementation**: component placement, 4-layer stack-up and routing, internal plane implementation, fabrication preparation, complete hand assembly/soldering, board bring-up and hardware fault isolation.

| | |
|---|---|
| **Board** | 67 × 50 mm, 4 layers |
| **MCU** | RP2040 with W25Q128 QSPI flash |
| **Layout** | 64 footprints · 597 routed track segments · 58 vias |
| **Internal planes** | GND on In1.Cu · +3V3 on In2.Cu |
| **My scope** | placement · routing · fabrication preparation · assembly · bring-up · debugging |
| **Academic context** | Materials and Manufacturing of Electronics · Summer Semester 2026 |

![Scoppy RP2040 PCB 3D View](images/pcb-3d-view.png)

### Quick links

- [PCB layout source](hardware/Scoppy.kicad_pcb)
- [PCB layout image](images/pcb-layout.png)
- [Bring-up and debugging notes](docs/bring-up-and-debugging.md)
- [Source attribution and contribution statement](SOURCE_ATTRIBUTION.md)

> **Course design input:** the electrical schematics and circuit/component-level design were provided by the professor for the PCB-layout assignment.  
> **Public-repository scope:** those schematic source files are intentionally **not redistributed** here. This repository publishes my PCB implementation and my own portfolio documentation.

## Contribution Boundary

### Professor-provided design input

- Main electrical schematic
- Hierarchical **Analog**, **Digital** and **Power** schematic sheets
- Circuit and component-level electrical design represented by those schematics

These schematic files were used as the course design input for the PCB-layout assignment and are **not included in this public portfolio repository**.

### My work

- PCB stack-up and physical board implementation in KiCad
- Complete component/footprint placement
- **All routing of the 4-layer PCB**
- Internal plane implementation and mixed-signal physical-layout decisions
- Board outline and physical organization
- Design-rule checking and fabrication preparation
- **Complete component assembly and hand-soldering after PCB fabrication**
- Board bring-up and electrical measurements
- USB-enumeration fault investigation
- Systematic power, continuity, USB, boot and clock checks
- Root-cause isolation to incomplete RP2040 solder contact
- Correction of the assembly defect and restoration of USB enumeration

I do **not** claim authorship of the professor-provided electrical schematics. The engineering work presented here as mine is the PCB placement/layout/routing, physical assembly/soldering, bring-up and troubleshooting.

## PCB Layout

![Scoppy RP2040 PCB Layout](images/pcb-layout.png)

## Architecture

![Architecture](images/architecture.svg)

The supplied course design was organized into hierarchical **Power**, **Digital** and **Analog** schematic sheets. My task was to translate those circuit requirements into a manufacturable 4-layer PCB while managing placement, signal routing, return paths, power distribution and physical board constraints.

## Board Assembly, Bring-Up and Fault Resolution

After fabrication, I assembled and hand-soldered the complete board. The first assembled board powered up but failed to enumerate over USB, including attempts to enter BOOTSEL mode.

The bring-up sequence included checks of:

- **5 V, 3.3 V and 1.1 V power rails**
- RP2040 RUN/BOOTSEL behavior and flash-control circuitry
- USB-C **CC resistors** and D+/D- path
- Continuity from the connector through protection/filtering components to the RP2040 USB pins
- Shorts on the USB differential pair
- RP2040 grounding and exposed-pad connections
- **12 MHz crystal oscillator** and load-capacitor network

During the investigation I also desoldered the USB connector to isolate the USB section. Further physical inspection identified the root cause: **the RP2040 did not have complete solder contact with the PCB**. Correcting the RP2040 solder/contact problem **resolved the USB-enumeration failure**.

This provided practical experience with **manual PCB assembly, soldering, measurement-driven fault isolation, PCB assembly defects, continuity/voltage testing and structured hardware bring-up**.

A more detailed troubleshooting summary is available in [`docs/bring-up-and-debugging.md`](docs/bring-up-and-debugging.md).

## Public Project Files

The public portfolio contains the PCB implementation and supporting portfolio material. The professor-provided schematic source and schematic symbol/cache files are intentionally excluded.

```text
hardware/
├── Scoppy.kicad_pro
├── Scoppy.kicad_pcb          # my PCB placement and 4-layer layout/routing
├── fp-lib-table
└── LIB/
    └── footprints/
        └── DME_Template.pretty/
            ├── 436351045816.kicad_mod
            ├── 60711002241501.kicad_mod
            ├── 629722000214.kicad_mod
            ├── CAY16470J4LF.kicad_mod
            ├── RP2040-QFN-56.kicad_mod
            ├── WE-CBF_0603_L1.6W0.8H0.8_HC.kicad_mod
            ├── WE-CNSW_1206.kicad_mod
            ├── WE-TVS_SC70-6L.kicad_mod
            ├── WE-TVS_SOT23-6L.kicad_mod
            ├── WE-VE_0603.kicad_mod
            └── WL-SMSW_0603_L1.6W0.98H0.8.kicad_mod

docs/
└── bring-up-and-debugging.md

images/
├── architecture.svg
├── pcb-layout.png
└── pcb-3d-view.png
```

Per-user KiCad state files (`*.kicad_prl`), lock files, autosaves, backups and operating-system metadata are excluded because they are not part of the engineering deliverable and can contain local-machine state.

## Tools and Skills

`KiCad` · `RP2040` · `4-Layer PCB Layout` · `Component Placement` · `Manual PCB Assembly & Soldering` · `Mixed-Signal PCB Routing` · `Internal Power/Ground Planes` · `USB-C` · `Hardware Bring-Up` · `Fault Isolation` · `Continuity & Voltage Measurement`

## Attribution

### Course design material

The electrical schematics used for this university assignment were **provided by the professor as course/project material**. They served as the electrical design input for my PCB-layout work. I do not claim authorship of them, and their source files are intentionally **not redistributed in this public repository**.

### Scoppy ecosystem

**Scoppy** is a separate project maintained by **fhdm-dev**:

- https://github.com/fhdm-dev/scoppy
- https://oscilloscope.fhdm.xyz/

I did not develop the Scoppy Android application or its firmware. This repository presents my university PCB-layout, assembly and hardware-bring-up work and is **not affiliated with or endorsed by the original Scoppy maintainers**.

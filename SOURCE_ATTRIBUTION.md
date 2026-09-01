# Source Attribution and Contribution Statement

## Electrical Schematics

The electrical schematics used for this university project were **provided by the professor as course/project material**. They defined the circuit and component-level electrical design that served as the input to the PCB-layout assignment.

The supplied material included the main schematic and hierarchical **Analog**, **Digital** and **Power** sheets.

I do **not** claim authorship of those electrical schematics. Their source files are intentionally **not redistributed in this public portfolio repository**.

## My Contribution

My individual engineering work on this project was the complete PCB implementation, physical board assembly and subsequent hardware bring-up, including:

- PCB stack-up and physical board implementation in KiCad
- Complete component and footprint placement
- **All routing of the 4-layer PCB**
- Internal power/ground plane implementation
- Mixed-signal layout and physical-routing decisions
- Board outline and physical organization
- Design-rule checking and layout preparation
- **Complete component assembly and hand-soldering after PCB fabrication**
- Board bring-up and electrical measurements
- USB-enumeration fault investigation
- Systematic power, continuity, USB, boot and clock checks
- Root-cause isolation to incomplete RP2040 solder contact
- Correction of the assembly defect and successful restoration of USB enumeration

The public source in this repository therefore focuses on my **PCB layout/implementation** and my own bring-up/debugging documentation rather than republishing the course-provided schematic source.

## Scoppy Attribution

The broader **Scoppy** oscilloscope/logic-analyzer ecosystem is a separate open-source project maintained by `fhdm-dev`:

https://github.com/fhdm-dev/scoppy

I did not develop the Scoppy Android application or its firmware. This repository documents my university PCB-layout, board-assembly/soldering and hardware-bring-up work for a custom RP2040 hardware implementation associated with that use case.

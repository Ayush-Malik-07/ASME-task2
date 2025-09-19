Title: Task 2 – KiCad PCB Workflow
Project setup


Opened the project and checked the schematic for all parts and reference designators so they make sense before moving to PCB.


Noted the initial error from PCB update: a lot of components had “no footprint assigned,” so PCB couldn’t add them.


Footprint assignment (CvPcb)


Opened the Assign Footprints tool from the schematic.


For big ICs already had exact packages selected: TPS61022 (VQFN-7 2x2mm P0.5mm), TPS5403 (SOIC‑8 3.9x4.9mm P1.27mm), SSOP‑24, TQFP‑32, and DO‑41 diode.


Went through all “no footprint” parts and assigned reasonable library footprints:


Resistors R1–R6: Resistor_SMD R_0805_2012 (generic, easy to solder).


Capacitors: 10 µF as electrolytic SMD (CP_Elec_3x5.3), 0.1 µF as ceramic C_0603/C_0805.


Connectors J1–J5 (Conn_01x04): PinHeader_1x04_P2.54mm_Vertical (simple 4‑pin headers).


Inductors L1, L2: Inductor_SMD L_0805_2012 (placeholder size).


Test points TP1–TP3: TestPoint_Pad_D1.5mm (easy probe access).


Crystal Y1 (Crystal_GND24): Crystal_SMD_3225‑4Pin_3.2x2.5mm (common 4‑pad).


Motors M1, M2: PinHeader_1x02_P2.54mm_Vertical (as a 2‑pin motor connector).


PWR_FLAG: left schematic‑only (no PCB footprint).


Hit “Apply, Save Schematic & Continue,” then “OK” to close the assignment.


Update PCB from schematic


Opened PCB Editor and used Update PCB from Schematic.


Kept default options checked: “Replace footprints with those specified by symbols” and “Update footprint fields from symbols.”


Confirmed the change list showed components being added and no errors.


Clicked “Update PCB,” then “Close,” and placed the footprints onto the board canvas.


First placement pass


Everything dumped near the origin, so started arranging:


Put J1–J5 4‑pin headers together in a neat column near the board edge for easy wiring access.


Placed motor connectors (M1, M2) along an edge so cables can exit cleanly.


Positioned the battery area and diode D1 near power entry.


Kept the buck/boost power ICs (TPS5403/TPS61022) grouped with their input/output capacitors and the inductor to keep power loops short.


Placed the microcontroller and set its decoupling capacitors as close to VCC pins as possible.


Spread out test points so they can be probed without shorting.


Tidy placement and checks


Looked at the airwires (rat’s nest) and nudged parts to reduce crossings and shorten critical nets (power, clock, motor drive).


Ensured connectors weren’t too close to the PCB edge so the board house’s keepouts and drill tolerances are ok.


Kept some room between power parts so there’s space for wider traces and thermal relief.


Board outline and layers


Confirmed a rectangular outline exists (Edge.Cuts). If not, drew a simple rectangle around the placed area with extra margin for mounting holes later.


Verified the active layers (F.Cu, B.Cu, silkscreen, mask) are visible and that silkscreen text won’t overlap pads.


Ready for routing (next step)


With placement mostly stable, planned to route next:


Wider traces for power paths (from battery to buck/boost and to loads).


Short, direct decoupling capacitor connections to MCU VCC/GND.


Keep signal lines away from noisy switching nodes if possible.


After routing, the plan is to run DRC, add a ground pour (zone), tweak silkscreen, and finally generate Gerbers and drill files.


Notes and small lessons learned
The big blocker was “no footprint assigned” errors; once each symbol had a footprint, the PCB update worked smoothly.


“Apply, Save Schematic & Continue” is important—if only “OK” is pressed without applying, assignments can get lost.


For parts like PWR_FLAG, it’s normal to have no footprint (it’s for ERC in the schematic only).


For motors or weird parts, using a simple pin header or terminal block footprint is a practical workaround for early revisions.


Keeping power ICs tightly grouped with their passives reduces loop area and helps with noise and efficiency.


What I would improve next
Measure exact package sizes for the real components (e.g., actual inductor body and pad size) so footprints match BOM parts.


Add mounting holes and check mechanical keepouts.


Assign net classes for power vs. signal widths/clearances before routing.


Label connectors clearly on silkscreen so wiring is foolproof.


That’s the Task 2 build log. It shows the whole path from fixing footprint errors, assigning reasonable packages, updating the PCB, and arranging the board so it’s ready for routing.
https://www.kicad.org
https://docs.kicad.org/master/it/pcbnew/pcbnew_create_board.html
https://www.pcbway.com/blog/PCB_Design_Tutorial/KiCad_Tutorial___How_to_make_a_PCB____PCB_layout_design.html
https://rheingoldheavy.com/design-assembly-kicad/
https://www.youtube.com/watch?v=f-ubxwG5VTU
https://docs.kicad.org/8.0/en/getting_started_in_kicad/getting_started_in_kicad.html
https://www.kicad.org/discover/pcb-design/
https://forum.kicad.info/t/how-to-create-a-layout-template/35021
https://www.scribd.com/presentation/840063073/PCB-Design-with-KiCad
https://docs.kicad.org/9.0/en/pcbnew/pcbnew.html


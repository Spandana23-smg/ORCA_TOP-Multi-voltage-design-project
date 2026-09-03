 # ORCA_TOP-Multi-voltage-design-project
Physical design flow of ORCA_TOP using Synopsys ICC2

# Description

This project describes the Physical design flow of the ORCA_TOP, using Synopsys ICC2. It run in the training institute computing cluster, using Synopsys library. No proprietary files are shared here.
This is a multi voltage design which consists of 4 clocks and 40 hard macro's and over 52k standard cells. 

# Reports
 Area Report
| Metric | Value |
|--- | --- |
| Cell count | 52357 |
|cell area| 175722.023 um^2 |
| total core area | 586645.678 um^2 |

Clocks Report
| Clock name | Period | Frequency |
| --- | --- | --- |
|PCI Clock | 7.5 | 133 MHz |
| System Clock | 2.3 | 434.78 MHz |
|SDRAM Clock | 4.1 | 243.40 MHz |
|Ate Clock | 30 | 33.33 MHz|

# Floorplaning
At first invoke the icc2 then set a search path for ndm files which contains .lib, tf, lef files.
then we read the netlist and initialize the floorplan to create the core and die area in L shape below values.

| Metric | Value |
| --- | --- |
| Core Utilization | 0.75 |
|core offset | 5 |
| Aspect Ratio | 1:1 |
| Shape | L |

After creating the core and the die area I place the ports in the core boundary. To place ports I used M5 & M6 layers. I this design it has 4 clock ports, 91 input ports and 142 output ports.
Then create a voltage area because some macro's & the the std cells need more power than the other cells.

| VDD | VSS | VDDH |
| --- | ---| --- |
| 0.75 V| 0 V | 0.95 V |
| 0.95 V | 0 V | 1.16 V |

Then place the macro in the core region there are 40 macros in the design they are divided in 4 hierarchy. I place the macro's according to the flylines and give the the channel spacing b/w the macros and also b/w core & macros. After that create the soft placement blockages in the channel spacing.
After that place the physical only cells I placed the end cap & tap cells in the design.

# Power Planing
in this we used M7, M8, M2 layers as a Straps to create the mesh , M5 & M6 for macro rings, M1 as a rails to power the standard cells. 
the power plan contains pg pattern, Pg strategy, via rule and compile strategy by using this ascepts we create the power plan.
After that checked for connectivity violations, missing vias & pg drc violations and fixed all the violations.

# Placement 
Before coming to placement in pre-placement set some app options and did the pre placment mega check.
Mega check :- check_design -pre_placement_stage
By using app options set the values for fanout, advance legalizer, routing layers, max density etc..
After that we place the cells and legalize the placement to place cells on site row and reduce the overlap.Then check for max_tan and max_cap violations. After that do place_opt to reduce the violations.
| violations| Before place_opt | After place_opt |
|--- | --- | ---|
|max transition | 602| 0 |
|max capacitance | 1141 | 5| 

# Placement optimize methods 
1. Bounds:-
Soft Bound: A gentle suggestion to the tool. ICC2 will try to place the specified cells within the boundary, but it can place them outside if necessary to resolve timing or congestion issues. There is no hard physical barrier.
Hard Bound: A strict rule. All specified cells must be placed inside the boundary. No cells belonging to that bound are allowed to leak out. However, other random cells from the rest of the design can still be placed inside the empty spaces of this region.
Exclusive Bound: The most restrictive type. Only the specified cells can be placed inside the region, and no other cells from the design can enter.

2. Path grouping :-  Is a technique used to organize the timing paths of a design into distinct categories called clock groups or path groups.By default, the optimization engine focuses heavily on the worst-case timing violation in the entire chip WNS. Path grouping prevents a single bad path in one part of your design from starving the rest of your design of optimization effort.

# CTS 




 















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
After that 










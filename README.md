
# ADVANCED PHYSICAL DESIGN USING OPENLANE/SKY130




## CONTENTS
## DAY 1
Inception of open-source EDA, OpenLANE and Sky130 PDK
* How to talk to computers
    * Introduction to QFN-48 Package,chip,pads,core,die and IPs
    * Introduction to RISC-V
    * From software Applications to Hardware
* SoC design and OpenLANE
    * Introduction to all components of open-source digital asic design
    * Simplified RTL2GDS flow
    * Introduction to OpenLANE and strive chipsets
    * Introduction to OpenLANE detailed ASIC design flow
* Get familiar to open-source EDA tools
    * OpenLANE Directory structure in detail
    * Design Preparation Step
    * Review files after design prep and run synthesis
    * Steps to characterize synthesis results
## DAY 2
Good vs Bad floorplan and introduction to library cells
* Chip floorplanning considerations
    * Utilization factor and aspect ratio
    * Concept of pre-placed cells
    * De-coupling capacitors
    * Power planning
    * Pin placement and logical cell placement blockage
    * Steps to run floorplan using OpenLANE
    * Review floorplan files and steps to review floorplan
    * Review floorplan layout in Magic
* Library Binding and Placement
    * Netlist binding and initial place design
    * Optimize placement using estimated wire-length and capacitance
    * Final placement optimization
    * Need for libraries and characterisation
    * Congestion aware placement using Replace
* Cell design and characterization flows
    * Inputs for cell design flow
    * Circuit design Step
    * Layout design Step
    * Typical characterzation flow
* General timing characterization parameters
    * Timing threshold definitions
    * Propagation delay and transition time
## DAY 3
Design library cell using Magic layout and ngspice characterization
* Labs for CMOS inverter ngspice simulations
    * IO place revision
    * SPICE deck creation for CMOS inverter
    * Switching Threshold Vm
    * Lab steps to git clone vsdstdcelldesign
* Inception of layout and CMOS fabrication process
    * Create active regions
    * Formation of N and P well 
    * Formation of gate terminal
    * Lightly doped drain formation
    * Source and drain formation 
    * Local interconnect formation
    * Higher level metal formation
    * Lab introduction to Sky130 basic layers layout and LEf using inverter
    * Lab steps to create std cell layout and extract spice Netlist
* Sky130 tech File Labs
    * Labs to create final SPICE deck using Sky130 tech
    * Lab steps to characterize inverter using sky130 model files
    * Lab introduction to Magic tool options and DRC rules
    * Lan introduction to Sky130 pdk's and steps to download Labs
    * Lab introduction to Magic and steps to load Sky130 tech-rules
    * Lab exercise to fix poly.9 error in Sky130 tech-file 
    * Lab exercise to implement poly resistor to diff and tap 
    * Lab challenge to describeDRC error as geometrical construct 
    * Lab challenge to find missing or incorrect rules and fix them
## DAY 4
Pre-layout timing analysis and importance of good clock tree
* Timing modeeling using delay tables
    * Lab steps to convert grid  info to track info
    * Lab steps to convert magic layout to std cell LEF 
    * Introduction to timing libs and steps to include new cell in synthesis
    * Introduction to delay tables
    * Delay table usage
    * Lab steps to configure synthesis settings to fix slack and include vsdinv
* Timing analysis with ideal clocks using openSTA
    * Setup timing analysis and introduction to flip-flop setup time
    * Introduction to clock jitter and uncertainity
    * Clock Tree Synthesis
* Clock tree synthesis TritonCTS and signal integrity
    * Clock tree routing and buffering using H-tree algorithm
    * Crosstalk and clock net shielding
    * Lab steps to run CTS using TritonCTS
    * Lab steps to verify CTS runs
* Timing analysis with real clocks using openSTA
    * Setup timing analysis using real clocks
    * Hold timing analysis using real clocks
    * Lab steps to analyze timing with real clocks using OpenSTA
    * Lab steps to execute OpenSTA with right timing libraried and CTS assignment
    * Lab steps to observe impact of bigger CTS buffers on setup and hold timing
## DAY 5
Final steps for RTL2GDS using tritonroute and OpenSTA
* Routing and desgin rule check
    * Introduction to Maze Routing A� LeeA�s algorithm
    * LeeA�s Algorithm conclusion
    * Design Rule Check
* Power distribution Network and routing
    * Lab steps to build power distribution network
    * Lab steps from power straps to std cell power
    * Basics of global and detail routing and configure TritonRoute
* Tritonroute features
    * TritonRoute feature 1 - Honors pre-processed route guides
    * TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing
    * TritonRoute method to handle connectivity
    * Routing topology algorithm and final files list post-route
## DAY 1
## Inception of open-source EDA, OpenLANE and Sky130 PDK
### How to talk to computers
#### Introduction to QFN-48 Package,chip,pads,core,die and IPs
* Take the example of an Arduino board, it is a small computer chip that processes instructions and controls the behavior of electronics
Block diagram of the board:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20130614.png)
The IC:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20130736.png)
Parts:
* PADs : the metal points on the bottom of the chipthat are used to connect the chip to a circuit through signal can be sent into the chip.
* Core : central part that processes the information.Its a place where all our Digital logical sits like the AND gate,OR gate,MUXs.
* Die : a tiny, flat piece of silicon that contains the actual electronic circuits and defines the size of the chip, its manufactured on a Silicon wafer.
* The SRAM,ADC,DAC,PLL are known As Foundry IP's.
* The SoC and the SPI are basically called as Macros.

#### Introduction to RISC-V
* "RISC-V intruction set architecture" popularly known as "ISA".Its a language of the computer,a way through which we are able to talk and communicate with the computers.
* For a C program to run on a computer hardware it is first compiled in its assembly language program which is nothing but the RISC-V assembly language program.
* This  is then converted into machine language program aka the binary language program(ie: 1's and 0's) which is understood by the hardware of the computer.
* Aafter converting these bits gets finnaly executed in the layout and get the required output.

#### From software Applications to Hardware
1. Apps: A computer software that is designed to perform specific tasks or functions for end-users.

2. System software: Refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. 

3. Operating System: The operating system is a fundamental piece of software that controls memory management, process scheduling, file system management, and user interface interaction.

4. Compiler: A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. Assembler: An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. RTL: RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

7. Hardware: Hardware refers to the physical components of a computer system or any electronic device. 

### SoC design and OpenLANE
#### Introduction to all components of open-source digital asic design
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20132452.png)
To implement Digital ASIC design we require certain elements these elements:
* PDK is a set of files provided by semiconductor manufacturers to help designers use their fabrication process to create integrated circuits (ICs). It contains a comprehensive set of information, models, and files that enable designers to develop and verify their designs using the specific process technology offered by the manufacturer.
* EDA tools refer to a category of software applications and tools used in the design and development of electronic systems, including integrated circuits (ICs), printed circuit boards (PCBs), and other electronic components.EDA tools are essential for designing and testing electronic hardware and ensuring that it functions correctly before it is manufactured.
* Register-Transfer Level tools:  a level of abstraction used in digital circuit design and describes how data moves between registers and how operations are performed on that data.In RTL design, the behavior of the digital system is defined by describing how data is transferred between registers and how operations are performed on that data. 

#### Simplified RTL2GDS flow
RTL to GDSII Flow:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20132350.png)
* Synthesis - Converts RTL to a ciruit, out of compomments from the standard cell library.
* Floor and Power Planning - Obejctive here is to plan the silicon area and create robust power distribution network to power the chip.
* Chip Floor Planning - Partition the chip die between different system building blocks and place the I/O pads.
* Macro Floor Planning - We define the macro dimensions, pin locations and rows are defined.
* Power Planning - The power distribution network is contructed.
* Placement - Placing the cells on the floorplan rows, aligned with the sites. There are 2 steps: Global and Detailed.
* Clock Tree Synthesis - To deliver the clock to all sequential elements.
* Routing - Implement the interconnect using the available metal layers.
* Sign Off - Perform physical verification such as DRC(Design Rule Check) and LVS(Layout vs Synthesis). Also perform STA(Static Timiing Analysis).

#### Introduction to OpenLANE and strive chipsets
OpenLane is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow framework.esigned to automate the process of designing and fabricating digital integrated circuits. OpenLane aims to make custom ASIC design more accessible to a broader range of engineers and researchers.

#### Introduction to OpenLANE detailed ASIC design flow
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20134121.png)

### Get familiar to open-source EDA tools
#### OpenLANE Directory structure in detail
The detailed directory structure can be seen here:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/VirtualBox_vsdworkshop_16_09_2023_21_38_06.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/VirtualBox_vsdworkshop_16_09_2023_21_38_28.png)

#### Design Preparation Step
To work on Openlane type docker in the openlane directory.
Also type:
```bash
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/VirtualBox_vsdworkshop_16_09_2023_21_44_46.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/VirtualBox_vsdworkshop_16_09_2023_21_46_21.png)

#### Review files after design prep and run synthesis
To view details of different files:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/review.png)
To run synthesis:
```bash
run_synthesis 
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/synth.png)
#### Steps to characterize synthesis results
The flop ratio can be calculated by using:
No. of flops/No. of cells = 1613/14876 = 0.108

Netlist is generated in the runs folder
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20221427.png)

## DAY 2
Good vs Bad floorplan and introduction to library cells
### Chip floorplanning considerations
#### Utilization factor and aspect ratio
Define Width and height of core and die: The die refers to the entire semiconductor chip, including the core, I/O pads, and any additional features.
Utilisation factor plays an important role in floor planning. It is given by: Area occupied by netlist/area of the core
Aspect ratio=Height/Width
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20230909.png)
#### Concept of pre-placed cells
We split the circuit into two parts, block 1 and block 2 
We extend the I/O pins and black box the boxes.
Now we separate the boxes and the get their respective I/O ports.
The use of doing this is that the users can use the blocks multiple times and form the required final circuit with ease.
They only need to implement the design once and it can be reused.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20231215.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20231222.png)

#### De-coupling capacitors
Everytime the circuit switches it draws current from the decoupling capacitor, whereas the outer network with the power supply and other componets is used to re-charge the capacitor
Decoupling capacitors store and discharge electrical energy quickly or decoupling capacitors absorb excess charge to filter out high- frequency noise and transient voltage fluctuations.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20231829.png)

#### Power planning
When a transition occurs on a net, charge associated with coupling capacitors may be dumped to ground. If there are not enough ground taps charge will accumulate at the tap and the ground line will act like a large resistor, raising the ground voltage and lowering our noise margin. To bypass this problem a robust PDN with many power strap taps are needed to lower the resistance associated with the PDN.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20232356.png)

#### Pin placement and logical cell placement blockage
Pin placement is an essential part of floorplanning to minimize buffering and improve power consumption and timing delays we use the HDL netlist to determine where a specific pin should be placed in the circuit. We join the common pins and try to keep the connections as effecient as possible.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20232842.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-16%20232903.png)

#### Steps to run floorplan using OpenLANE
Go to the directory:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/configuration
```
```bash
less README.md
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/openlaner.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/openlanerr.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/openlanerrr.png)

Now to run floorplan, in openlane:
```bash
run_floorplan
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/floorplan.png)

#### Review floorplan files and steps to review floorplan
Go to runs folder and check logs folder 
The design config.tcl would have overwritten system defaults.
To view the flooplan:
go to:
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_10-53/results/floorplan
```
open the def file
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/floorplan2.png)

Then we type the command:
```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/magic1.png)

#### Review floorplan layout in Magic
Click s and v to bring it to center
Left and right click to create a box
Click z to zoom
Click s and type what in the tkcon window to know the cell
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/magic2.png)

### Library Binding and Placement
#### Netlist binding and initial place design
Library consists of various kinds of cells which have different shapes and sizes, flavours and different timing information.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20170605.png)

#### Optimize placement using estimated wire-length and capacitance
The components of the netlist are placed in the core area according to the convenience of distance from the pins.
Signal integrity is maintained by repeaters
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20170925.png)

#### Final placement optimization
Based on timing analysis we check if the placements meets the given specifications.
The placements include thr buffers(repeaters) and other blocks of the design.
(Setup timing analysis)

#### Need for libraries and characterisation
Typical IC design flow:
Logic synthesis
Floorplan(from the netlist of logic design)
Placement(so that initial timing is reduced)
CTS: Clock tree synthesis(clock should reach at the same time)
Routing
STA: static timing analysis

One thing common among all stages: Gates or Cells.

#### Congestion aware placement using Replace
Global and detailed placement
For global placement we run the run_placement command
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/placement.png)
Then type
```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![Alt text]https://github.com/aishwarya-2511/pes_pd/blob/main/images/placement2.png)

### Cell design and characterization flows
#### Inputs for cell design flow
Cell design flow refers to the process of creating and optimizing individual digital logic cells that are part of a standard cell library. These libraries contain a set of pre-designed, characterized, and reusable logic gates, flip-flops, and other basic building blocks used in the design of integrated circuits. These libraries include PDK, DRC and LVS rules, SPICE models, libraries, user-defined specifications. User derfined specifications like Pin location, drawn gate lenght are added to the libarary by the library developer.

Cell design flow:
Inputs -> Process design kits(PDKs) : DRC and LVS rules, SPICE models, library and user-defined specs.
Design Steps -> Circuit Design, Layout Design(Euler Path and Stick Diagram), Characterization.
Outputs -> CDL(Circuit Description Language), GDSII, LEF, extracted spice netlist(.cir)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20175056.png)
#### Circuit design Step
Implement function using NMOS and PMOS and then derive the network graph. Derive the Euler's path and stick diagram from the graph.
Model the circuit based on requirements
Output is a CDL(circuit description language) file

#### Layout design Step
Convert stick diagram according to the DRC rules Extraction of parasitics,extracted spice list


#### Typical characterzation flow
Timing ,noise power.libs functions Read in the models and tech files and generate extracted spice Netlist. Read the subcircuits and attach power sources. 

### General timing characterization parameters
#### Timing threshold definitions
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20175553.png)

#### Propagation delay and transition time
Propagation delay=time(out_fall_thr)-time(in_rise_thr)
Choice of threshold should be so that delay is positive

Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)
Fall transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)
## DAY 3
Design library cell using Magic layout and ngspice characterization
### Labs for CMOS inverter ngspice simulations
#### IO place revision
If we want to change the input output pin placement
Originally, the IO pins were equi spaced
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/original%20io.png)
To change, execute this in openlane:
```bash
set ::env(FP_IO_MODE) 3
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20181829.png)

#### SPICE deck creation for CMOS inverter
Component connectivity
Component values
Identify nodes
Name nodes
Spice deck contains the netlist description of the nodes (D,G,S,S) in between which the component lies, and its W/L ratio.
!{Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20183321.png)

#### Switching Threshold Vm
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-17%20183751.png)
CMOS is a robust device.
Switching threshold is a point where Vin=Vout
Both nmos and pmos are in saturation

#### Lab steps to git clone vsdstdcelldesign
```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign
```
then 
```bash
magic -T sky130A.tech sky130_inv.mag &
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/git.png)

### Inception of layout and CMOS fabrication process
#### Create active regions
16 mask process:
* Slect a substrate(p or n type) based on resistivity and doping level
* Create active region for transistors: to isolate the active regions for transistors SiO2 and Si3N2 deposited. Pockets created using photoresist and lithography.

#### Formation of N and P well 
* P-well formation involves photolithography and ion implantation of p-type Boron material into the p-substrate.N-well is formed similarly with n-type Phosphorus material.Drive in diffusion by placing it in a high temperature furnace.

#### Formation of gate terminal
* A polysilicon layer is deposited and photolithography techniques are applied to create NMOS and PMOS gates.

#### Lightly doped drain formation
LDD done to avoid hot electron effect and short channel effect.

#### Source and drain formation 
Thin oxide layers are added to avoid channel effects during ion implantation.N+ and P+ implants are performed using Arsenic implantation and high-temperature annealing.

#### Local interconnect formation
Thin screen oxide is removed through etching in HF solution.Titanium deposition through sputtering is initiated. Heat treatment results in chemical reactions, producing low-
resistant titanium silicon dioxide for interconnect contacts and titanium nitride for top-level connections, enabling local communication.

#### Higher level metal formation
To achieve suitable metal interconnects, non-planar surface topography is addressed.Chemical Mechanical Polishing (CMP) is utilized by doping silicon oxide with Boron or Phosphorus to achieve surface planarization.

#### Lab introduction to Sky130 basic layers layout and LEf using inverter
To look at the layout of a CMOS inverter, we type the command
```bash
magic -T sky130A.tech sky130_inv.mag &
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20092311.png)

Pressing 's' three times will show what parts are connected to the selected part.

#### Lab steps to create std cell layout and extract spice Netlist
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20103458.png)

Commands:
```bash
ext2spice cthresh 0 rthresh 0 -> this is done to copy the parasitic capacitances
ext2spice
```

### Sky130 tech File Labs
#### Labs to create final SPICE deck using Sky130 tech
We can use 'g' on the keyboard to activate the grid and after selecting a grid by right clicking on the mouse, we type box in tkcon window to check the minimum value of the layout window.

![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20183213.png)

open the spice file using the command
```bash
gedit sky130_inv.spice
```

#### Lab steps to characterize inverter using sky130 model files
To plot the graph for output vs input sweeping the time
```bash
ngspice sky130_inv.spice
```
In the ngspice shell we use the command
```bash
plot y vs time a
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20183444.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20183458.png)
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20183504.png)

Rise Time = 0.006675e-09 s
Propogation Delay = 0.06379e-09 s

#### Lan introduction to Sky130 pdk's and steps to download Labs
To download:
```bash
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
Move the file to desktop using:
```bash
mv drc_tests.tgz Desktop/
```
Extract the file using
```bash
tar xfz drc_tests.tgz 
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/downloadandmove.png)
To open it
```bash
magic -d XR
````
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/openmagic.png)

#### Lab introduction to Magic and steps to load Sky130 tech-rules
open the 'met3.mag' file.
If we select an area and type drc why in the tkcon wndow, it will show us the DRC error.

#### Lab exercise to fix poly.9 error in Sky130 tech-file
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20184631.png)

Now open the tkcon window and type
```bash 
load tech sky130A.tech
drc check 
```

#### Lab challenge to describeDRC error as geometrical construct 
We open the nwell.mag file
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20184755.png)

this is displayed
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20184808.png)

#### Lab challenge to find missing or incorrect rules and fix them
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20184854.png)

make these changes:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20184906.png)

Now we select the nwell.4 and type the following commands
```bash
tech load sky130A.tech
drc check
drc style drc(full)
drc check
```
error is still there.
Fix :
Select the existing nwell.4 and make a copy of it by selecting it and clicking 'c'.
Now select a small area on the nwell.4 and add an 'nsubstratecontact' by hovering over it and clicking middle mouse button.


## DAY 4
Pre-layout timing analysis and importance of good clock tree

### Timing modelling using delay tables
Place and routing (PnR) is performed using an abstract view of the GDS files generated by Magic. The PnR tool will use the abstract view information, formally defined as LEF information, to perform interconnect routing. From PnR POV, We have to follow certain guidelines to get standard cell set

Input and output ports must lie on the intersection of vertical and horizontal tracks Width of the standard cell should be odd multiples of the track pitch and height should be odd multiple of vertical track pitch

#### Lab steps to convert grid  info to track info
Path to track info
```bash
Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130fd_sc_hd
```
Now we open the track.info file: The tracks.info file is used during routing. Routes are the metal traces. 1st numeric column indicates the offset and 2nd indicates the pitch along provided direction

Set the grid values:
%grid 0.46um 0.34um 0.23um 0.17um

We converge the grid definition in the layout to track definition
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191016.png)
![alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191035.png)
From the above pic, its confirmed that the pins A and Y are at the intersection of X and Y tracks. So the first condition is met. The next requirement is that the width of the cell should be the odd multiple of xpitch which is '0.46' as seen in the tracks.info file.

#### Lab steps to convert magic layout to std cell LEF 
To generate the cell LEF file from Magic first we save the modified layout and then we open the file and extract LEF we type the command in the tkcon window
```bash
save sky130_vsdinv.mag
```
Now in the terminal we type
```bash
magic -T sky130A.tech sky130_vsdinv.mag
lef write
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191139.png)

#### Introduction to timing libs and steps to include new cell in synthesis
We copy the lef file created and the sky130 library that to the src folder of picorv32a folder.

Modify config file to include the libraries and lef file
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191240.png)

Next in openlane:
```bash
prep -design picorv32a -tag 18-09_05-15 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191337.png)

And then ```run_synthesis```

#### Lab steps to configure synthesis settings to fix slack and include vsdinv
Slack violations refer to timing violations in digital designs. These violations occur when the signal arrives at its destination too early or too late, violating the specified setup or hold time constraints.

When referring to pre clock tree synthesis STA analysis we are mainly concerned with setup timing in regards to a launch clock. STA will report problems such as worst negative slack (WNS) and total negative slack (TNS). These refer to the worst path delay and total path delay in regards to our setup timing restraint. Fixing slack violations can be debugged through performing STA analysis with OpenSTA, which is integrated in the OpenLANE tool. The desired value of slack is above or equal to 0.

Ways to fix slack

* Changing synthesis strategy in OpenLANE

Enalbed CELL_SIZING
Enabled SYNTH_STRATEGY with parameter as DELAY 1
![ALt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191739.png)

Slack still isnt in the required range.

The sdc file used is my_base.sdc defined in pre_sta.conf using the command sta pre_sta.conf
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191811.png)

The delay is high when the fanout is high. Therefore we can re-run synthesis by changing the value of SYNTH_MAX_FANOUT variable

* Enable cell buffering

* Perform manual cell replacement on our WNS path with the OpenSTA tool Net is driving most outputs and replace the driver cell with larger form of its own kind
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191836.png)

* Optimize the fanout value with OpenLANE tool

Now since synthesised the core using our vsdinv cell too and as it got successfully synthesized. We go ahead with the floorplan

```bash
init_floorplan
run_placement
```
On zooming:
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20191912.png)

#### Introduction to delay tables

Delay tables, also known as delay models or delay tables, are essential components in digital circuit design and analysis. They provide a way to model and understand the propagation delays of logic gates and interconnects within a digital integrated circuit (IC). These tables play a crucial role in ensuring that the circuit meets its timing requirements, such as setup and hold times, and they are fundamental to the design of synchronous digital systems. Here's an introduction to delay tables:

Purpose of Delay Tables:
Delay tables are used to represent the delays encountered by signals as they pass through various components of a digital circuit. The primary purposes of delay tables are as follows:

Timing Analysis: They are essential for performing timing analysis, ensuring that signals meet their timing constraints, and identifying potential violations.

Synchronization: They help in synchronizing different parts of a digital system to ensure that data is sampled or latched correctly.

Power Estimation: Delay tables are used for estimating power consumption in digital circuits since power dissipation is directly related to signal transitions.

Components of Delay Tables:
Delay tables typically include the following components:

Input Conditions: These conditions specify the input signal values or transitions that trigger the delay calculation. Inputs can include input signal values, load conditions, and transition times.

Gate Delays: Delay tables include information about the propagation delays of various logic gates, such as AND, OR, NAND, NOR, XOR, and others. These delays depend on the gate's technology, fan-out, and input conditions.

Interconnect Delays: They account for the delays introduced by the wires and routing between logic gates. Interconnect delays depend on the physical characteristics of the wires, including length, resistance, and capacitance.

Output Loads: The output load conditions specify the capacitive load that the gate must drive, which affects the output delay.


### Timing analysis with ideal clocks using openSTA
#### Setup timing analysis and introduction to flip-flop setup time
Setup Timing Analysis:

Setup timing analysis is a critical aspect of digital circuit design and verification. It focuses on ensuring that data signals meet the required setup time constraints at the inputs of sequential elements (e.g., flip-flops) in a digital system. The primary goal of setup timing analysis is to ensure that data is stable and valid before it is clocked into a flip-flop or other storage elements.

Introduction to Flip-Flop Setup Time:

The setup time (Ts) for a flip-flop is a critical parameter that determines when a data input signal must be stable before the arrival of the clock edge to guarantee proper data capture. It is defined as the minimum amount of time the data input must be held at a valid logic level before the active clock edge (e.g., rising edge) for reliable storage.

#### Introduction to clock jitter and uncertainty
Clock Jitter:

Clock jitter refers to the short-term variations or fluctuations in the timing of a clock signal's edges. It is a critical parameter in digital systems and communication systems, as it can affect the overall system's performance, especially in high-speed or sensitive applications. Clock jitter can be caused by various factors and can manifest as random or deterministic variations in the clock signal's timing.

Clock Uncertainty:

Clock uncertainty, also known as clock skew, is related to the variation in the arrival times of clock signals at different points within a digital system. It is distinct from clock jitter but can also impact system performance and timing. Clock uncertainty can arise due to factors such as clock distribution network delays, routing delays, and variations in clock path lengths.

#### Clock Tree Synthesis
After all the above steps of fixing slack violations. A a mapped.v file is generated in synthesis results. Therefore we write this netlist using write_verilog and replace the openlane generated mapped file ie., picorv32a.synthesis.v

now in the openlane flow, continue with
```bash
run_flooorplan 
run_placement 
run_cts
```


### Clock tree synthesis TritonCTS and signal integrity
#### Timing Analysis with Real CLocks using OpenSTA
To run CTS we need to type the command ```run_cts```

#### Post CTS- STA Analysis
OpenSTA is an open-source static timing analysis tool that is commonly used in digital circuit design. STA is a critical step in the design and verification of digital circuits, ensuring that the circuit meets its timing requirements. OpenSTA is part of the larger OpenROAD open-source RTL-to-GDSII flow, which provides a complete ASIC design environment.
Steps:
Launch OpenRoad.
Read lef file from tmp folder of runs
Read def file from results of cts
Create and save the .db file =
Load the .db file =
Read the cts generated verilog file
read both the minimum and maximum liberty files.
set the clocks.
Generate timing reports
```bash
read_lef /openLANE_flow/designs/picorv32a/runs/18-09_06-26/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/18-09_06-26/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/16-09_19-58/results/synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -max $::env(LIB_FASTEST)
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20232925.png)

![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20232932.png)

The timing results wont meet our expectations due to the utilization of minimum and maximum library files which OpenRoad does not currently support for multi-corner optimization. Hence we do it using only typical corner lib

We perform it again for a more accurate result

Final report
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20192818.png)



## DAY 5
### Power Distribution Network and Routing
#### Build Power Distribution Network
To do this first we type ```gen_pdn```

To check for DRC errors we need to check the 'tritonRoute.drc' folder
To extract the parasitics we use the SPEF Extraction.
![Alt text](https://github.com/aishwarya-2511/pes_pd/blob/main/images/Screenshot%202023-09-18%20233546.png)

#### SPEF Extraction
SPEF (Standard Parasitic Exchange Format), is a standard file format used in the semiconductor industry to represent parasitic information for integrated circuits. Parasitic elements, such as resistance and capacitance, can significantly affect the performance of a circuit, so accurate modeling and extraction of these parasitics are crucial for designing and optimizing electronic devices.After routing has been completed interconnect parasitics can be extracted into a SPEF file. 

To use this engine we need to go to
```bash 
cd Desktop/work/tools/SPEF_Extractor
```
Next we need to use this command
```bash
python3 /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-09_19-58/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-09_19-58/results/routing/picorv32a.def
```
SPEF file is created in :
```bash
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-09_19-58/results/routing/
```

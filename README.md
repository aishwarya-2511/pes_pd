
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
    * Concept of pre-places cells
    * De-coupling capacitors
    * Power planning
    * Pin placement and logical cell placement blockage
    * Steps to run floorplan using OpenLANE
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
    * SPICE simulation lab for CMOS inverter
    * Switching Threshold Vm
    * Static dynamic simulation of CMOS inverter
    * Lab steps to git clone vsdstdcelldesgin
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
    * Lab steps to configure OpenSTA for post-synth timing analysis
    * Lab steps to optimize synthesis to reduce steup violations
    * Lab steps to do basic timing ECO
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

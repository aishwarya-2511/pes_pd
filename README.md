# pes_pd


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
    * OpenLANE Project Link Description
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

# Digital VLSI SoC Design and Planning Training

## Overview
This repository showcases my work related to System-on-Chip (SoC) design, adhering to the methodologies provided in the NASSCOM VSD SoC Design Program.

### Internship Details
- **Provider:** VLSI System Design  
- **Duration:** September 17, 2024 – October 2, 2024  

### Acknowledgments
- **Kunal Ghosh** – Co-founder, VSD Corp. Pvt. Ltd.  
- **Nickson P Jose** – Technical Lead at HCLTech | Formerly at Intel  
- **R. Timothy Edwards** – Senior Vice President of Analog and Design, efabless Corporation

## Tools Used
- **Verilog** – RTL design  
- **OpenROAD** – Physical design  
- **Magic** – Layout design  
- **Sky130 PDK**  

## Workflow
1. RTL Design  
2. Synthesis  
3. Floorplanning  
4. Placement & Routing  
5. GDSII Generation  

## Physical Design Flow

In the RTL to GDS flow, physical design is critical. During this process, the synthesized netlist, design constraints, and standard cell libraries are inputs to create a layout (GDS file) following foundry rules. This layout is then submitted for chip fabrication. The conversion of a gate-level netlist into a layout is known as physical design.

Physical design involves several stages, each requiring specific checks, analyses, and verifications. Below is a detailed description of the process:

### PD Flow

#### 1. Import Design or NetlistIn
The first stage involves importing all the necessary design and constraint files, such as the netlist, SDC (Synopsys Design Constraints), UPF (Unified Power Format), DEF (Design Exchange Format), technology files, logical and physical libraries, and TLU+ files.

#### 2. Floorplanning (Chip Planning)
Floorplanning is essential in physical design. It translates the netlist (a logical description) into a physical layout by positioning blocks or macros within the core area of the chip. Tasks in this stage include:
- Defining the width and height of the core and die.
- Identifying the locations of predefined cells/macros.
- Planning the placement of I/O pins.
- Designing the pad ring for the chip.

The goals are to minimize area and delay.

#### 3. Placement
Placement involves arranging standard cells on the die. It optimizes area, timing, and power while minimizing timing DRCs and ensuring the placement is routable.

#### 4. Clock Tree Synthesis (CTS)
CTS ensures uniform distribution of clock signals across sequential elements. It involves adding buffers or inverters to reduce skew and ensure minimal insertion delay.

#### 5. Routing
Routing defines the precise pathways for connections between cells. It uses metal and vias to create the necessary interconnections, ensuring timing constraints are met and avoiding LVS and DRC errors.

Routing involves:
- Global Routing
- Detailed Routing
- Track Assignment
- Search and Repair

#### 6. Physical Verification and Signoff
After routing, the design undergoes verification checks such as LVS (Layout vs. Schematic), DRC (Design Rule Check), and ERC (Electrical Rule Check). These ensure the layout adheres to design and fabrication rules.

---

 ## RTL2GDS OpenLANE ASIC Flow Practical Implementation

### Day 1 Labs: Linux Command Overview

Below are essential Linux commands used throughout the labs:

- **pwd:** Displays the current working directory.
- **cd:** Navigates through directories.
- **ls:** Lists files and subdirectories in the current directory.
- **mkdir:** Creates a new directory.
- **rmdir:** Deletes an existing directory.
- **rm:** Deletes files.
- **help:** Provides details on how to use a command.
- **clear:** Clears the terminal.

### Key Files and Directories in OpenLANE

- **libs.ref:** Contains design libraries (standard cells, IO cells).
  - **lef:** Layout description files.
  - **lib:** Liberty files for timing/power analysis.
  - **gds:** GDSII layout files.
  - **verilog:** Verilog models of the cells.

- **libs.tech:** Technology files for specific EDA tools.
  - **magic:** Technology files for Magic.
  - **klayout:** Layer properties for KLayout.
  - **ngspice:** SPICE models for simulations.
  - **drc/lvs/pex:** Design rule check, layout versus schematic, and parasitic extraction files.

### Running OpenLANE in Interactive Mode

 1. Start Interactive Mode in OpenLANE
Open a terminal and run the following command to enter OpenLANE's interactive mode:


![1](https://github.com/user-attachments/assets/28637a4c-a2ea-4106-ae12-a561659c1904)

To run in interactive mode (step by step mode)

    bash-4.2$ ./flow.tcl -interactive
    
    
`Package import and check`

    % package require openlane

`Prepare design`

To prepare and setup the design

    % prep -design picorv32a

![opnln](https://github.com/user-attachments/assets/2cbf45b0-cdf0-4e1b-912d-f452391947fe)


` Synthesis `
   % run_synthesis
   
![8](https://github.com/user-attachments/assets/b78542eb-ae3d-4df6-90ba-b60ceeae8284)
![7](https://github.com/user-attachments/assets/6a2ff209-4b96-43cd-b651-b7d4d662c3c2)
![6](https://github.com/user-attachments/assets/b900efee-4544-4cb8-bef5-218e92835267)
![5](https://github.com/user-attachments/assets/9114098e-a8f0-4924-a738-f5acba38d175)
 
---

## Day 2 Assignment: Chip Floorplanning and Library Cells

## Introduction
In this assignment, we will explore the concepts of good versus bad floorplans and introduce library cells in chip design. Key considerations in chip floorplanning include the utilization factor and aspect ratio.

## Chip Floorplanning Considerations

### Core Area
The **Core Area** is defined as the section of the chip where all logic cells and components are placed. This area is critical for performing logic operations.

### Die Area
The **Die Area** surrounds the core area and is primarily used for placing input/output (I/O) components. The dimensions of the die are contingent upon the core dimensions.

### Utilization Factor
The **Utilization Factor** is a measure of efficiency in the core area, defined as:

`Utilization Factor = (Area occupied by netlist / Total core area)`
​
 
*Aspect Ratio:*
The aspect ratio is the ratio of the core’s height to its width. If the aspect ratio is 1, the core is square-shaped; otherwise, it will be rectangular.

`Aspect Ratio = (Height of the core / Width of the core)`
​
## Task-1: Run 'picorv32a' Design Floorplan Using OpenLANE.
Steps for running floorplan
1. Open the terminal and navigate to the directory where the design is saved.
2. Execute the command to generate the floorplan: ` run_floorplan`
3. The generated floorplan will be saved in the `floorplan` directory.
4. Open the floorplan in the Magic tool to visualize the design:`magic floorplan`
 
![1](https://github.com/user-attachments/assets/2b6b717e-b9ce-4c65-b1df-0904d3a9e7a0)


## Task-2: Calculate Die Area in Microns

#### Die Area Calculation:
```Die area = (Die width x Die height)```
```math
Die\ width\ in\ microns = \frac{550064}{1000} = 550.064\ Microns
```
```math
Die\ height\ in\ microns = \frac{567120}{1000} = 567.120\ Microns
```
```math
Area\ of\ die\ in\ microns = 550.064 * 567.120 = 311952.29568\ Square\ Microns
```
![2](https://github.com/user-attachments/assets/8af078cb-0e2e-4a5b-bc94-6c389f3303fc)



## Task-3: Load the floorplan in Magic tool
### Launching MAGIC:
To load the floorplan in MAGIC, use the following command:
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/28-09_14-14/results/floorplan/
```
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

```
 ![3](https://github.com/user-attachments/assets/3b7bc64f-8a70-45e0-900d-e6516daaddfe)

### Visualizing in MAGIC:
Once the MAGIC GUI opens:

We can now use the visualization tools in MAGIC (zoom, center, select cells, etc.) to inspect and analyze the floorplan.

- Center the design: Press `S` to select the entire design and `V` to align it vertically on the screen.

- Zoom in: Left-click and drag to select a specific area, then press `Z` to zoom in on that region.

 ![4](https://github.com/user-attachments/assets/745baa0b-b874-4fe5-b9c7-a67e72597445)


### Task-4: Run placement and run plcement def in magic tool

#### Placement in VLSI Design Overview
Placement in VLSI design is the process of determining where to physically place standard cells within a chip, consisting of:

1. Global Placement: Assigns rough locations to cells, allowing some overlap

2. Detailed Placement: Refines locations to ensure there is no overlap and that cells are placed on legal sites.
```
run_placement
```

![5](https://github.com/user-attachments/assets/86766346-a362-4c61-9792-d7aa8a71fc41)
 ![6](https://github.com/user-attachments/assets/7769a3a6-9bb7-43d3-92ce-bff876515b1c)

#### Running the Placement DEF in Magic Tool:
Use the following command to run the placement def in magic tool

1. Navigate to the Directory
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/28-09_14-14/results/placement/

```
2. Load the Placement DEF File in MAGIC
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```
 

#### Inputs and Outputs in the Design Process
#### Inputs
- **Process Design Kits (PDKs):** Technology-specific information for chip design.
- **Design Rule Check (DRC) and Layout vs. Schematic (LVS)**: Ensure compliance with layout and functional requirements.
- **SPICE Models:** Used for circuit simulation.
- **Library & Custom Specifications:** Specific design libraries and user-defined parameters.

Outputs:

- **CDL (Circuit Description Language):** A text-based representation of the circuit.
- **GDSII:** The layout file for fabrication.
- **LEF (Library Exchange Format):** Contains cell size, pin location, and other details.
- **SPICE Netlist:** Extracted parasitic information for circuit simulation.
- T**iming, Noise, and Power Libraries:** Generated during characterization.


 

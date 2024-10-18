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
 


 

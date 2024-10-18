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

To execute OpenLANE in step-by-step mode:

```bash
bash-4.2$ ./flow.tcl -interactive
Package Import and Setup
tcl
 
% package require openlane
% prep -design picorv32a
![2](https://github.com/user-attachments/assets/d6681fa7-02fc-4856-b1f9-4a7e3ca30960)

This will generate a new directory in the runs folder for storing the design’s results and reports.

Running Synthesis
tcl
 
% run_synthesis
After synthesis, review the results, and proceed to the next steps, such as placement and routing.
![6](https://github.com/user-attachments/assets/52a134b3-e43c-42ff-b535-e6e96f5f6aa5)


bash
 
# Review configuration:
config.tcl: Contains OpenLANE configurations.
src: Contains Verilog and constraints files.

![opnln](https://github.com/user-attachments/assets/1bf8e465-4d1a-42e9-8138-2e1b7a0a4346)
![8](https://github.com/user-attachments/assets/a8decaf9-b71f-4fa0-9e67-3d64c3d8e729)
![7](https://github.com/user-attachments/assets/7f7afd84-965c-4641-99c0-551436d87fd2)
![6](https://github.com/user-attachments/assets/8ee7dd70-fac7-47ae-be6a-12e863a51a20)
![5](https://github.com/user-attachments/assets/f8e73f46-0426-4c74-a1d4-543fd16f7269)
![3](https://github.com/user-attachments/assets/06300983-ab3f-43bd-a902-a75275fd88cf)
![2](https://github.com/user-attachments/assets/2c93efdc-fced-42bf-9a37-cf793c0fe10b)
![1](https://github.com/user-attachments/assets/ba7c1c7b-34a8-4bf8-a6e2-96f3f1825f46)

 

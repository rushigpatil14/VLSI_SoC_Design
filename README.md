![1](https://github.com/user-attachments/assets/358da013-7097-4a3c-9bbe-f6b454d3c734)# Digital VLSI SoC Design and Planning Training

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



## Day 3: Design library cell using Magic Layout and Ngspice characterization

## Overview
In this assignment, we focused on designing a CMOS inverter layout using the MAGIC tool and characterizing it with Ngspice. This process involved cloning the necessary files, performing SPICE extraction, and analyzing the results.

## Steps to Complete the Assignment

Start by cloning the repository containing the inverter layout:

1. Clone the Custom Inverter Layout
``` 
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
 
![1](https://github.com/user-attachments/assets/dc383429-5ade-404c-b4bf-189ea524e974)

2. Navigate to the Inverter Layout Directory
Change to the directory where the layout files are located:

```
cd vsdstdcelldesign
cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
```
 
![2](https://github.com/user-attachments/assets/9f9e1e2f-354f-4960-b86a-6b3a2e29bd50)

3. Open the Inverter Layout in MAGIC
To open the inverter layout in MAGIC, use the following command:
```
magic -T sky130A.tech sky130_inv.mag &
```
![3](https://github.com/user-attachments/assets/5d5b14eb-001c-48de-b9fe-f92d758e1708)

 

4. Perform SPICE Extraction in MAGIC
Extract the SPICE netlist from the layout by executing these commands in MAGIC:

```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
 ![3](https://github.com/user-attachments/assets/cfb202c5-3957-4c7a-b8d5-da263defcbaa)
![4](https://github.com/user-attachments/assets/cb4e991f-25d8-4961-a2b9-1417a9f7ec05)

![5](https://github.com/user-attachments/assets/6fc22ae9-f688-4043-a921-451255a705dc)

5. Load the SPICE File for Ngspice Simulation and Create a Plot

    Run Ngspice to simulate the SPICE netlist and plot the results:
```
ngspice sky130_inv.spice
plot y vs a
```
![6](https://github.com/user-attachments/assets/be432015-11ae-4c04-b0a6-3877bd77fe7e)

 ![7](https://github.com/user-attachments/assets/eff569bc-7967-438b-96fa-31eb2bfcbfaf)

## Create a LEF file
### Examples of DRC Errors

- **M3.1** Metal Width DRC Violation:
     -  Violation: The width of the metal trace does not meet the minimum requirement.
     -   Impact: Higher resistance or failure during fabrication.

 - **M3.2** Metal Spacing DRC Violation:

    - Violation:Distance between adjacent metal traces is below required spacing.
    - Impact: Possible short circuits or    reliability issues.

- **M3.5** Via Overlapping DRC Violation:

   -  Violation: Overlapping vias that do not meet minimum spacing.
    - Impact: Connectivity issues and structural problems.
- **M3.6** Minimum Area DRC Violation:

    - Violation: Enclosed area does not meet the minimum threshold.
    -Impact: Insufficient current-carrying capacity and reliability concerns.

These DRC violations need to be addressed to ensure the design is manufacturable and reliable.

## Opening the MAGIC Tool
To open the Magic Tool use this command

```
magic -d XR &
```
 
![6](https://github.com/user-attachments/assets/1a1496ce-75ed-4b4c-9b98-ddc5427eac23)

## Open the MET3 Layout File in MAGIC
Open the met3.mag file:

 
![7](https://github.com/user-attachments/assets/b5f6f128-7e3c-456e-b814-a6cbeaf2df27)

#### Steps for Poly.9 Rule Correction:

1. **Check Poly Spacing:** Ensure spacing meets the minimum distance defined by the design rules.
2. **Adjust Poly Width:** Confirm polysilicon lines meet minimum width requirements.

3. **Correct Poly-to-Diffusion Overlap:** Ensure proper overlap between polysilicon and diffusion regions..

4. **Check Poly Over Gate Region:** Ensure the poly layer extends appropriately over the active area.

5. **Run DRC:** Re-run the DRC after corrections to check for violations.

6. **Adjust Layout as Needed:** Further tweak layout dimensions to meet design rules.
<img width="614" alt="Screenshot 2024-09-30 154232" src="https://github.com/user-attachments/assets/87dcb36c-8723-4893-9fff-142aab08bd0c">

 
<img width="634" alt="loadpoly" src="https://github.com/user-attachments/assets/6513d62b-60a1-4c1b-9703-2cd86effef34">
<img width="650" alt="Screenshot 2024-09-30 154602" src="https://github.com/user-attachments/assets/c272e143-e9b0-4164-ad26-39c9db56aad6">

### Updating the DRC
To update the DRC, insert the following commands in the file:
 
 <img width="638" alt="Screenshot 2024-09-30 160129" src="https://github.com/user-attachments/assets/0d0e8fca-2bab-4489-bd89-d8d77dbc9baf">

### To update the DRC, insert the following commands in the file:
```
 # Loading updated tech file
   tech load sky130A.tech

 # Must re-run drc check to see updated drc errors
  drc check

 # Selecting region displaying the new errors and getting the error messages 
  drc why
```
Here are the snapshots of DRC checks

 
<img width="644" alt="poly9check" src="https://github.com/user-attachments/assets/546af532-8b6e-41a6-b8a1-f9f88eb227ae">
<img width="644" alt="drc_check" src="https://github.com/user-attachments/assets/e1ae06b5-af6e-415d-a4e9-3191f5c19aa2">
<img width="638" alt="drc_ckeck" src="https://github.com/user-attachments/assets/46d311f7-8570-49f4-b945-3cff518542cc">


## Day 4 Pre-layout Timing Analysis and Importance of 
## Steps Overview
 
 
![photo_2024-10-18_23-41-44](https://github.com/user-attachments/assets/2e57dec9-9082-43ee-8992-3694ed38ec47)

### 1. Open the Custom Layout for Analysis
 - First, navigate to the layout directory and open the design in MAGIC.

```
#Navigate to the layout directoryn
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Open the design in MAGIC
magic -T sky130A.tech sky130_inv.mag &
```

- Move to the tracks information directory:
```
cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd
```

### 2. Set Grid Tracks for Local Layer in tkcon Window
In the tkcon terminal, use the following grid settings to align with the tracks:

```
help grid
grid 0.46um 0.34um 0.23um 0.17um
```
 ![photo_2024-10-18_23-43-54](https://github.com/user-attachments/assets/7fc122d0-5b60-48a7-872b-b4d2eff0e3d1)
![4](https://github.com/user-attachments/assets/44b2c09f-92af-42b8-8c0b-e53f96f1ed86)

### 3. Save Layout and Generate .lef File
To save the layout in .lef format:
```
save sky130_vsdinv.mag
```
 ![5](https://github.com/user-attachments/assets/fa7488bf-d8ff-4061-a2fb-1af82c1a0af1)

 ![6](https://github.com/user-attachments/assets/97071204-3ae5-4baa-9d5a-a8f24b8e18a2)

```
lef write
```
 ![4](https://github.com/user-attachments/assets/44b2c09f-92af-42b8-8c0b-e53f96f1ed86)


Snapshot of .lef file
 ![6](https://github.com/user-attachments/assets/5e55e87e-56b7-4772-98e6-4141e6ee2fc2)

### 4. Copy the .lef File to Source Directory
Now, copy the .lef file into the source directory of your design:
```
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
 ![5](https://github.com/user-attachments/assets/1fff3e2f-f345-4a4d-97bb-96d0f7305211)

### 5. Add the .lef File in OpenLane Flow Configuration
Modify the config.tcl file to include your custom .lef in the OpenLane flow:

```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

```
### 6. Synthesize the Design

To start the synthesis process, run:
```
# Run synthesis
run_synthesis
```
![9](https://github.com/user-attachments/assets/8056a68a-0af1-47c4-8a92-94a6be9b157f)

 
#### We will use following commands to  improve timing and run synthesis


```
prep -design picorv32a -tag 30-09_04-44 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
```

`run_synthesis`

![9](https://github.com/user-attachments/assets/8056a68a-0af1-47c4-8a92-94a6be9b157f)

#### now run floorplan using `run_floorplan`
But it fails. Instead we can use these commands to run floorplan
```
init_floorplan
place_io
tap_decap_or

```
Now run placement using `run_placement`
 ![10](https://github.com/user-attachments/assets/9317247d-4ea7-44b4-8f5a-1c2627d1d052)
![11](https://github.com/user-attachments/assets/0dbe9c3e-0a9e-4535-a4f6-b9c746d18e61)
![12](https://github.com/user-attachments/assets/3def3675-e6bd-4cd1-8bfb-59f95744c04b)
```
# Command to view internal connectivity layers in tkcon window
expand
```

![13](https://github.com/user-attachments/assets/0a617c4a-7580-442c-a59f-18c42663b9d1)

 
 
 

## Day 5 Task- To generate Power Distribution Network (PDN) and load the layout and Perform detailed routing

1. Generate PDN (Power Delivery Network)
Power distribution is critical to ensure VDD and VSS are well connected across the design. Begin by invoking OpenLane:

#### Steps to Generate PDN in OpenLane
1. Invoke the OpenLane flow: If you haven't already, start by invoking OpenLane in interactive mode:
``cd Desktop/work/tools/openlane_working_dir/openlane
``
2. Set the design and configuration
```
prep -design picorv32a
```
![d7](https://github.com/user-attachments/assets/c8044c0a-f13e-4443-86d4-e674a06616c7)

3. Addiitional commands to include newly added lef to openlane flow merged.lef
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
4. Generate PDN
``` 
gen_pdn
```
 

####  Perform Detailed Routing
Detailed routing connects the placed standard cells using metal layers according to the routing constraints, ensuring that signal and power nets are properly wired without design rule violations.
Steps 

1. Ensure you have the placement and CTS completed: Before starting routing, make sure the placement and clock tree synthesis (CTS) steps are successfully completed. If not, run:
```
run_placement
run_cts
```
 
### 2. run detailed routing
Before routing, make sure the placement and CTS steps are complete. If not, run:
```
run_routing
```
<img width="811" alt="Screenshot 2024-10-03 005835" src="https://github.com/user-attachments/assets/264ff18d-5994-4cec-8356-a3cee98f0108">
<img width="811" alt="Screenshot 2024-10-03 005956" src="https://github.com/user-attachments/assets/4ad77108-c78f-4c7f-ac1d-e21ac622fd9d">

 <img width="380" alt="Screenshot 2024-10-03 010633" src="https://github.com/user-attachments/assets/926ec86e-f895-41a4-834d-a8f62d5f92b9">

### post routing STA

 

<img width="913" alt="Screenshot 2024-10-03 010409" src="https://github.com/user-attachments/assets/4b23097b-289b-4b4c-8927-ff12a421f002">

<img width="926" alt="Screenshot 2024-10-03 010433" src="https://github.com/user-attachments/assets/c87b86df-1c64-4ba3-892f-f92b46763b8c">






 

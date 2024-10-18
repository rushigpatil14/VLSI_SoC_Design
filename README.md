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
![image](./images/clonerepo.png)
![image](./images/repo.png)

2. Navigate to the Inverter Layout Directory
Change to the directory where the layout files are located:

```
cd vsdstdcelldesign
cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
```
![alt text](cplibfilestosrc-1.png)
3. Open the Inverter Layout in MAGIC
To open the inverter layout in MAGIC, use the following command:
```
magic -T sky130A.tech sky130_inv.mag &
```
![image](./images/magicinverter.png)
![image](./images/selctnmosregion.png)

4. Perform SPICE Extraction in MAGIC
Extract the SPICE netlist from the layout by executing these commands in MAGIC:

```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
![image](./images/extractall.png)

![image](./images/Screenshot%202024-09-29%20233428.png)

![alttext](./images/spicefile.png)

5. Load the SPICE File for Ngspice Simulation and Create a Plot

    Run Ngspice to simulate the SPICE netlist and plot the results:
```
ngspice sky130_inv.spice
plot y vs a
```
![alt text](./images/fatalerror.png)

![alt text](./images/plot.png)

![image](./images/Screenshot%202024-09-30%20131732.png)

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
![openmagictool](./images/openmagictool.png)

## Open the MET3 Layout File in MAGIC
Open the met3.mag file:


![metal3](./images/openm3magfile.png) 
![alt text](./images/Screenshot%202024-09-30%20152355.png)

#### Steps for Poly.9 Rule Correction:

1. **Check Poly Spacing:** Ensure spacing meets the minimum distance defined by the design rules.
2. **Adjust Poly Width:** Confirm polysilicon lines meet minimum width requirements.

3. **Correct Poly-to-Diffusion Overlap:** Ensure proper overlap between polysilicon and diffusion regions..

4. **Check Poly Over Gate Region:** Ensure the poly layer extends appropriately over the active area.

5. **Run DRC:** Re-run the DRC after corrections to check for violations.

6. **Adjust Layout as Needed:** Further tweak layout dimensions to meet design rules.

![alt text](./images/Screenshot%202024-09-30%20154232.png) 
![alt text](./images/loadpoly.png) 
![alt text](./Screenshot%202024-09-30%20154602.png) 

### Updating the DRC
To update the DRC, insert the following commands in the file:
![updatedrc](./images/Screenshot%202024-09-30%20160129.png)

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

![alt text](./images/poly9check.png)
![alt text](./images/drc_check.png)
![alt text](./images/drc_ckeck.png)




## Day 4 Pre-layout Timing Analysis and Importance of 
## Steps Overview

![trackfile](./images/opentrackfile.png)


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
![alt text](./images/Screenshot%202024-10-01%20130045.png)
![alt text](./images/Screenshot%202024-10-01%20130633.png)


### 3. Save Layout and Generate .lef File
To save the layout in .lef format:
```
save sky130_vsdinv.mag
```
![leffile](./images/Screenshot%202024-10-01%20131806.png)

![leffile](./images/Screenshot%202024-10-01%20131919.png)

 
```
lef write
```
![alt text](<Screenshot 2024-10-01 131723-2.png>)

Snapshot of .lef file

![alt text](<Screenshot 2024-10-01 131919-1.png>)
![alt text](<Screenshot 2024-10-01 131806-1.png>)

### 4. Copy the .lef File to Source Directory
Now, copy the .lef file into the source directory of your design:
```
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
![image](./images/cplibfilestosrc.png)

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

![images](./images/runsynthesis.png)
![images](./images/Screenshot%202024-10-01%20145736.png)

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

![images](./images/chiparea.png)
![images](./images/Screenshot%202024-10-01%20152614.png)
![images](./images/Screenshot%202024-10-01%20153620.png)

#### now run floorplan using `run_floorplan`
But it fails. Instead we can use these commands to run floorplan
```
init_floorplan
place_io
tap_decap_or

```
Now run placement using `run_placement`

![images](./images/Screenshot%202024-10-01%20190308.png)
![images](./images/placementzoom.png)

```
# Command to view internal connectivity layers in tkcon window
expand
```
![images](./images/Screenshot%202024-10-01%20191608.png)

### Perform post-synthesis timing analysis using the OpenSTA tool 

mybase.sdc
```
```
This is a presta snapshot
![images](./images/presta.png)

Now slack is reduced
![images](./images/reduceslack.png)

Again `run_synthesis`

![images](./images/Screenshot%202024-10-02%20011848.png)

After Slack MET run floorplan and placement

![images](./images/Screenshot%202024-10-02%20012043.png)



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
3. Addiitional commands to include newly added lef to openlane flow merged.lef
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
4. Generate PDN
``` 
gen_pdn
```
![alt text](<Screenshot 2024-10-02 011848-1.png>)

####  Perform Detailed Routing
Detailed routing connects the placed standard cells using metal layers according to the routing constraints, ensuring that signal and power nets are properly wired without design rule violations.
Steps 
1. Ensure you have the placement and CTS completed: Before starting routing, make sure the placement and clock tree synthesis (CTS) steps are successfully completed. If not, run:
```
run_placement
run_cts
```
c:\Users\ankit\OneDrive\Desktop\dhanvanti\nasscon_sep\Screenshot 2024-10-02 161229.png c:\Users\ankit\OneDrive\Desktop\dhanvanti\nasscon_sep\Screenshot 2024-10-02 160632.png c:\Users\ankit\OneDrive\Desktop\dhanvanti\nasscon_sep\Screenshot 2024-10-02 155618.png

### 2. run detailed routing
Before routing, make sure the placement and CTS steps are complete. If not, run:
```
run_routing
```
![routing](./images/Screenshot%202024-10-03%20005835.png)
![routing](./images/Screenshot%202024-10-03%20005956.png)
![routing](./images/Screenshot%202024-10-03%20010633.png)

### post routing STA

![routing](./images/Screenshot%202024-10-03%20010409.png)
![routing](./images/Screenshot%202024-10-03%20010433.png)








 

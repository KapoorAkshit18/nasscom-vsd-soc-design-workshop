# NASSCOM–VSD SoC Design Workshop
## 2 weeks workshop on Digital VLSI using Sky130 PDK
## 📑 Table of Contents  
- [Introduction](#-introduction)
- [Magic Tool Overview](#-magic-tool-overview) 
- [Linux Commands Used](#️-linux-commands-used)  
- [Lab 1 – Opening OpenLane](#-lab-1--opening-openlane)  
- [Lab 2 – Synthesis & Floorplan](#-lab-2--synthesis--floorplan)  
- [Layout Creation in Magic](#-layout-creation-in-magic)  
- [Placement](#-placement)  
- [Custom Inverter Layout](#-custom-inverter-layout)  
- [CMOS Cross-Section](#-cmos-cross-section)  
- [SPICE Simulation](#-spice-simulation)  
- [Conclusion](#-conclusion)  

---

<details>
  <summary> Overview </summary>   
  
  ---
- **Tools Used:** OpenLANE, Magic, ngspice, OpenROAD  
- **PDK:** SkyWater SKY130A (130 nm open-source)  
- **Design Used:** `picorv32a` (RISC-V Core)  
- **Duration:** 2 weeks (structured 5 + 5 days)  
- **Environment:** Oracle VM (Ubuntu)
 ---   
 
Free and Open Source Software (FOSS) and Free And Open Source Silicon (FOSSi)
EDA tools and opensource being an advantage.The workshop includes short videos and gives a good understanding for how chip design process forks.It tells how ASIC design flow works with more emphasis on the Back-End.
The Back-End usually involves steps like Synthesis,STA of the .v file then Design for Testability (DFT), Physical Design, then Physical Verification and finally the GDS-II file creation.Gds is the file saving format given to the foundries and normally it is in binary involving geometric shapes.

VLSI which stands for Very Large Scaling Industry refers to the scaling of size and increment of the transistors numbers on a single chip.

Further more chip architecture was discussed along with basic CMOS(complementary metal oxide semiconductor technology) concept that tells the reason for the steps done in the backend. Further more the workshop was equipped with the labs and assignment as well, which gives hands on experience, and practical insights of the backend process.

This 2-week workshop provides a structured introduction to digital VLSI design using Free and Open Source Software (FOSS) and Silicon (FOSSi). The video lectures were organized in a nested format, for example:

> * **Sky130 Day 3** – Design library cell using Magic Layout and ngspice characterization
>     * **SKY130_D3_SK2** – Inception of Layout – CMOS fabrication process
>       * **SKY_L9** – Lab steps to create std cell layout and extract spice netlist

We explored fundamental concepts like VLSI (Very Large Scale Integration), CMOS technology, and chip architecture, all reinforced with hands-on labs and assignments. From the image below, our workshop is more focused toward Team B (Physical Design). Labs along with the assessments are conducted. Linux System and Commands were used throughout the workshop period.


<img width="940" height="589" alt="image" src="https://github.com/user-attachments/assets/c7c9d77f-e04e-407d-82b1-cec7a2a09989" />


Virutal machine by oracle is utilized as most of the VLSI tools are based on linux so it provides isolated environment for working effectively.Linux has more advantage and for critical process like chip design which is the brain of any device or machine is a preferred choice.This documentation is more of picture based (means do the steps by keeping the images as a reference in your mind) so follow accordingly.
</details>

## Magic Tool Overview  

As per Fossi Dial up 
Magic tool is more than DRC, it can read and write GDS.It can extract and netlist (SPICE file).LEF(Library Exchange File)/DEF(Design Exchange File) compatible.Wiring refers to physical joining of the network elements whereas routing defines rules for that.This feature is also included in the Magic.Plots are available for the analysis of the results in a graphical manner.
More features
- Paint and Erase 
- Instead of bins it works on single base 

  
##  Introduction
The workshop emphasized **FOSSi (Free and Open-Source Silicon Initiative)** and demonstrated how open-source EDA tools democratize chip design.  

It followed the complete **ASIC design flow**:
1. Synthesis  
2. Floorplanning  
3. Placement  
4. Clock Tree Synthesis (CTS)  
5. Routing  
6. Static Timing Analysis (STA)  
7. Physical Verification (DRC/LVS)  
8. GDS-II generation  

Each step was practically implemented using **OpenLANE automation**, **Magic layout**, and **ngspice** simulation:  

- **Oracle VM VirtualBox** used for isolated Linux environment  
- **Linux OS** preferred for chip design reliability  
- **Magic** – layout editing, DRC/LVS, GDSII generation  
- **ngspice** – circuit simulation  
- **OpenLane** – RTL-to-GDSII flow
  
## **Lab 1** : To open the openflow   
1. type `docker` <!-- make sure you are in openlane working directory whose path is /desktop/work/tools/openlane_working_dir/openlane -->
2. type second command `./flow.tcl -interactive`   <!-- this will open openlane in an interactive mode -->

Linux commands used:
```
cd    // to change directory 
ls    // to list items
ltr   // list in chro order
pwd   // shows current directory
cd ../  // makes the directory levele two step up 
```
![start](https://github.com/user-attachments/assets/08584779-4e80-4f0a-85ad-b2579e5685a7)

## **LAB 2**: To run Synthesis and Floorplan 
after openlane is opened, type command `prep -design picorv32a`
The success preperation message will look like below  

![image](https://github.com/user-attachments/assets/f8ef0213-537e-4d7e-b3e3-f551ced1a640)  

The folder with timestamp is created where all of the results for the design is stored  
![image](https://github.com/user-attachments/assets/844248e7-5d1a-4ec8-a863-d3bd801ff187)

The picorv32a design compilation  
![image](https://github.com/user-attachments/assets/070d462c-608f-41eb-a1ce-eb7f5a3be5c9)

The synthesized results are seen by  `less` command

![image](https://github.com/user-attachments/assets/bbf5b85b-3120-4614-9a4d-da4b756f135d)
![image](https://github.com/user-attachments/assets/66470a0a-7025-4dfa-95d0-e0e1f7fdf9bf)

*Assessment 1* flop ratio 

Equals to  10.84 percentile 

*Assessment 2* area of the die 

 die height  and die width calculation by subtracting down leftmost corner from top rightmost corner == 443587.2122325 in microns square

 ![image](https://github.com/user-attachments/assets/ea5581aa-c365-4d11-83a8-cd75a775df5b)

![Uploading image.png…]()


## **Lab**:  To create layout of the picorv32a

In the results directory of the floorplan open it in the terminal and type  command:
`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &` 

![image](https://github.com/user-attachments/assets/71594757-1148-4315-baa7-d290df83a779)
from zooming the blocks are seen with its unique role in overall  


**Placement**
again the synthesis process is followed in sequence creating folder named 28-04-11:55  to `run_placement`   

![image](https://github.com/user-attachments/assets/7c534eca-cafe-4bb8-a336-9cd1969d1b20)


Further more the equidistant nature is changed for some reason and below files are again revisied  

![image](https://github.com/user-attachments/assets/7076d4f7-8b39-4add-9ca9-ee3ab139ebbe)

![image](https://github.com/user-attachments/assets/03b6b051-7205-4bb6-9244-4b6ecc5f962a)  

![image](https://github.com/user-attachments/assets/fc4c6f18-8d86-4cab-a9b7-77e064209dc9)

git cloning step for the custom inverter 
![image](https://github.com/user-attachments/assets/9cd5bcc1-4a69-49d2-a564-a6dc9f90f80a)

n and p well is identified by clicking on the S and by arrow keys for navigating it  

![image](https://github.com/user-attachments/assets/cffa7806-8191-499d-b9ab-6a2e81b3dc23)

the cloned repositry explains the steps involved for the RTL to GDSII flow  

deleting part of an area thus getting an error in DRC
which is indicated by red colour  
creation of spice file by running following commands in the tkcon terminal with the inverter being not modified
```
pwd
extract all                      // this will make .ext file
ext2spice cthresh 0 thresh 0     // this will extract parasitics 
ext2spice                          // finally spice file will be created by this commant
```
![image](https://github.com/user-attachments/assets/d210ebea-dda6-4afa-96ed-928108f6d27e)  

![image](https://github.com/user-attachments/assets/da0c115b-45e4-4fee-8792-0562fdd3b656)

now going to the window option set the 0.10 micro metre grid 
now zoom in and do the selection of the box and run the command `box`  
  
  ![image](https://github.com/user-attachments/assets/43b26074-34a1-492e-9dc4-70a5bfa50017)

next step would be editing the spice file  
  ![image](https://github.com/user-attachments/assets/1c63de64-1039-4736-a42d-f4522389d960)  
  this is the image of the 16 mask cmos process from p substrate tp the final stage that after opening the contact holes which is not discussed in the video although might be a good homework.

![image](https://github.com/user-attachments/assets/4c1f9326-1df8-47f2-bc03-3c891c130c52)  
the image describes how drain of pmos and nmos are connected together 

  
  ![image](https://github.com/user-attachments/assets/d5bc46ea-0189-4f22-9d56-704a52d14d63)  
  this image shows how source of pmos is connected to the ground,and next task would be to know where is drain of nmos here  

  
  ![image](https://github.com/user-attachments/assets/e0849e4a-8bb1-4d78-86c4-d7e0463f18ba)  
  
how they relates
pdiff/ndiff is similar to the implants in the cross sectional view of the cmos   
getting back to spice   
earlier the spice file for the inverter was created without the parasitcs of cap and res  
use 'vim sky130_inv.spice'  
to read the file   
**The spice code understaning whose screenshot can be seen by going up**
```
.option scale=10m

.subckt sky130_inv A Y VPWR VGND
X0 Y A VGND VGND sky130_fd_pr__nfet_01v8 ad=1.44n pd=0.152m as=1.37n ps=0.148m w=35 l=23
X1 Y A VPWR VPWR sky130_fd_pr__pfet_01v8 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23
C0 VPWR A 0.0774f
C1 Y A 0.0754f
C2 VPWR Y 0.117f
C3 Y VGND 0.279f
C4 A VGND 0.45f
C5 VPWR VGND 0.781f
.ends
~          
```
  
`X1 Y A VPWR VPWR sky130_fd_pr__pfet_01v8 ad=1.44n pd=0.152m as=1.52n ps=0.156m w=37 l=23`  
if you see this line the X is used to instantiate the subcircuit (in our case it is of pfet) that is present inside the sky130 pdk.
also,

1. sky130 → SkyWater 130nm process

2. fd → Fully Depleted (not relevant here; historical)

3. pr → Primitive device (used in layout and simulation)

4. pfet → P-type Field Effect Transistor = PMOS

5. 01v8 → Designed for 1.8V nominal operation (core voltage domain in CMOS)

removing subcircuit portion from the generated spice code and adding spice code as per feroz repositry take as reference  

![image](https://github.com/user-attachments/assets/0ef8f7b4-28fc-4748-a817-e429f8f43d51)  
after certain modification in the spice code  
the output was:  


![image](https://github.com/user-attachments/assets/6f5a0cd2-bd80-4451-9971-802eaf4ef509)

expected output is 
![image](https://github.com/user-attachments/assets/c452a673-866b-46d7-9075-a4055fefab09)

<img width="975" height="383" alt="image" src="https://github.com/user-attachments/assets/5e87ebc3-95eb-4f5f-8ae0-cba22084181a" />

  Downloading the drc by using the following command to perform drc violations fixing:  
```bash

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
gvim .magicrc
magic -d XR &

```
<img width="945" height="919" alt="Screenshot 2025-10-03 165238" src="https://github.com/user-attachments/assets/3cdd2173-1dde-4c21-b099-1549a7e1b2e0" />    



<img width="952" height="1047" alt="Screenshot 2025-10-03 165523" src="https://github.com/user-attachments/assets/55d45f61-2fbb-48fe-b059-7fb5e932ae6e" />  

 <img width="948" height="1079" alt="Screenshot 2025-10-03 170511" src="https://github.com/user-attachments/assets/0ea0280c-487c-4f05-ab03-2945b6f46103" />    
 

  <img width="884" height="337" alt="Screenshot 2025-10-03 171244" src="https://github.com/user-attachments/assets/d19385bf-d49b-4535-8cae-6a5586d145dc" />  
  
<img width="952" height="1017" alt="Screenshot 2025-10-03 173950" src="https://github.com/user-attachments/assets/12076a4e-5842-4334-a5e3-be0a85ff4cb0" />  

<img width="957" height="900" alt="Screenshot 2025-10-03 174135" src="https://github.com/user-attachments/assets/28b409f8-a99b-4abe-b9d4-abf9641b5f0b" />  

<img width="957" height="1079" alt="Screenshot 2025-10-03 180034" src="https://github.com/user-attachments/assets/4bc76c62-10ff-400b-8957-e41b968541e3" />

<img width="881" height="346" alt="Screenshot 2025-10-03 181503" src="https://github.com/user-attachments/assets/c8410a83-011c-49cc-b787-fc5b47439eae" />  
certain modificiations were done, so to mark the error, which was hidden.  
next we have to fix N-Well, which was overlapping the Deep N-well and the dimensions which was needed to be added was 0.4 micrometre, so to fix this error.  
 <img width="665" height="495" alt="Screenshot 2025-10-04 094632" src="https://github.com/user-attachments/assets/090f74b5-5015-478d-abf4-e09f42868758" />
 
<img width="653" height="499" alt="Screenshot 2025-10-04 094947" src="https://github.com/user-attachments/assets/773e610b-87a3-43c4-97f4-40bab5c9c2c1" />  


<img width="656" height="503" alt="Screenshot 2025-10-04 095146" src="https://github.com/user-attachments/assets/7979d8ba-5a9f-449e-9959-3a0206d7522a" />  

Given below is the tracking information, which are metal traces used for routing.  
from this we can find the pitch values, or number of grid boxed inside the selected outer box.

<img width="613" height="339" alt="Screenshot 2025-10-04 111056" src="https://github.com/user-attachments/assets/2616bb0f-8864-4eb0-ab24-ac9d2636bb09" />    
in the tkcon window we have used the `grid` command and setted the values as  
```
grid 0.46um 0.34um 0.23um 0.17um
```
which are similar to the values finded out in the routing file.
Furthermore, we looked upon 3 conditions which we have to remember: intersection, width to be odd multiple and height have to be even multiple.  

<img width="959" height="1017" alt="Screenshot 2025-10-04 114711" src="https://github.com/user-attachments/assets/47628344-23c3-467f-acba-c46057319333" />  
Next, we were exposed to how ports are named and attached to the layout files (Magic ignores the port definations, but it is useful for placement)  
<img width="415" height="273" alt="Screenshot 2025-10-04 115909" src="https://github.com/user-attachments/assets/face5495-3cf1-4ab8-9f7a-54d4868d897b" />
then, we saved it as custom inverter with the name sky130_vsdinv, which we will use in the future placements and routing stages.  

<img width="960" height="1079" alt="Screenshot 2025-10-04 122730" src="https://github.com/user-attachments/assets/0e835f8d-b3c3-458c-ab89-119782c55146" />
<img width="957" height="1079" alt="Screenshot 2025-10-04 123849" src="https://github.com/user-attachments/assets/2475cb85-f1b9-4d0e-9af0-1bd6a8004933" />  

then we, checked the config.tcl file and edited it by adding the following commands:  
```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

<img width="957" height="1077" alt="Screenshot 2025-10-04 124611" src="https://github.com/user-attachments/assets/db17432d-206c-4e4a-8fe6-4d34b507aa3e" />

rerunning the openlane flow  so, to check the command for overwriting the existing file in the same directory, and after preparing our design we are supposed to add the following commands:  
```bash
# commands to load merged.lef having our custom inverter
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Know more about synth strategy from the readme.md file located in the openlane 
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY from AREA "0"
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING from 0
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not (sky inverter )
echo $::env(SYNTH_DRIVING_CELL)
```

then we run `run_synthesis` command followed by placement and we get our Total Negative Slack value as -759.46 and Worst Negative Slack value as -24.89 in ns. These violations are expected to be fixed.  

  <img width="960" height="1079" alt="Screenshot 2025-10-04 130325" src="https://github.com/user-attachments/assets/6b9bd5b4-caff-4755-a12f-397e3d6c5a9a" />  
  
<img width="950" height="1076" alt="Screenshot 2025-10-04 144412" src="https://github.com/user-attachments/assets/7d57baf3-02c0-4ac3-9fcb-32a1695ae155" />  

<img width="961" height="1079" alt="Screenshot 2025-10-04 144420" src="https://github.com/user-attachments/assets/d906fe48-8dbd-46c0-9921-3d8c726e00d9" />

we, have confirmed the custom inverter from the merged.lef file  

<img width="958" height="1079" alt="Screenshot 2025-10-04 155544" src="https://github.com/user-attachments/assets/17ecb221-2c39-4fa0-9e5f-9717a4eaa260" />

Few errors like  in the image and is solved by using the commands  
~~~
init_floorplan
place_io
tap_decap_or
~~~

<img width="960" height="1079" alt="Screenshot 2025-10-04 160525" src="https://github.com/user-attachments/assets/c685bc42-b340-4b8b-b536-217630449cd6" />  

Resizer.lib error which was solved by moving the required file to the project directory.  

<img width="895" height="179" alt="Screenshot 2025-10-04 161154" src="https://github.com/user-attachments/assets/d17b9965-c2eb-40f7-9609-c8751352c115" />  



then we use `run_placement` command   

<img width="956" height="1079" alt="Screenshot 2025-10-04 163804" src="https://github.com/user-attachments/assets/6daf83ce-69a1-42d6-9021-639a534b1621" />  
Using magic we have confirmed the placement of our custom inverter.   
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```


  <img width="961" height="1079" alt="Screenshot 2025-10-04 164115" src="https://github.com/user-attachments/assets/f75e9d7e-614e-46ca-9651-742ffcad65c0" />

<img width="962" height="1079" alt="Screenshot 2025-10-04 164825" src="https://github.com/user-attachments/assets/8eff358f-914c-4a19-b443-e1a6959b2229" />  

<img width="960" height="1077" alt="Screenshot 2025-10-04 165356" src="https://github.com/user-attachments/assets/b2a3cd42-5b08-4ebe-9d3a-2ea0ae6adce7" />  

then, we note the capacitance value for using it in the sdc written by us. We have also created pre_sta.conf file for Static Timing Analysis by using the command `sta pre_sta.conf`

<img width="952" height="1079" alt="Screenshot 2025-10-04 191939" src="https://github.com/user-attachments/assets/9f4527d2-32e9-4f1d-adc1-0857b3a4fe6a" />  

<img width="955" height="1079" alt="Screenshot 2025-10-04 195549" src="https://github.com/user-attachments/assets/e7b47dcf-a3a7-4009-9764-660f5be42f38" />

then we, use `replace_cell <cell_name> <new_cell_name>` command to reduce the slack by noting the cells having the most delay and fanout and replacing them from the alternatives of it from the library. 

<details>command for the report reading ```report_checks -fields {net cap slew input_pins} -digits 4  
  exit``` </details>


<img width="944" height="1079" alt="Screenshot 2025-10-04 203336" src="https://github.com/user-attachments/assets/20ea4aa5-1094-4099-becf-59b6d8355eee" />  


<img width="959" height="1079" alt="Screenshot 2025-10-04 204858" src="https://github.com/user-attachments/assets/dc8d1b82-cd02-4351-817e-b1a17aa81c18" />  
slack reduced by  1.8ns. It was achieved through noting the cell number in _   _ format and making the changes accordingly.
<img width="1085" height="1079" alt="Screenshot 2025-10-04 222138" src="https://github.com/user-attachments/assets/41003e9d-2adf-412f-8cce-cc5407b7007f" />

it is a crucial stage to complete it by using `write_verilog <synthesized netlist name eg. picorv32.v>` command after the possible slack reductions.   
<details> It is noted that even without saving our Chip area for module was '\picorv32a': 181730.544000 and 
tns 0.00
wns 0.00 which was ideal, but how it came is the challenge which is not in the scope of this project currently.</details>

then, we ran `run_cts` by Triton for Clock Tree Synthesis, which will create the paths by using most likely the H Algorithm.  

  <img width="963" height="1079" alt="Screenshot 2025-10-05 070443"   src="https://github.com/user-attachments/assets/1ad9e8ce-91cb-4613-a3c1-ebb19eaf783a" />  


 Checking the file present inside configuration folder, for variables definations:  
 

  <img width="955" height="1079" alt="Screenshot 2025-10-05 083047" src="https://github.com/user-attachments/assets/caac7fb0-febf-4cb5-9003-f8b4c51259d5" />

then, we used, `read_lef ` and `read_def` commands for POST CTS (1):  

```bash
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/04-10_10-12/tmp/merged.lef

# Reading def fileOP
read_def /openLANE_flow/designs/picorv32a/runs/04-10_10-12/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/04-10_10-12/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```
below are the screenshots of the each commands:
<img width="957" height="1079" alt="Screenshot 2025-10-05 085035" src="https://github.com/user-attachments/assets/48b87e38-76eb-4d72-a329-56eb70b65352" />    


<img width="958" height="1079" alt="Screenshot 2025-10-05 085158" src="https://github.com/user-attachments/assets/0237dc9f-15e4-47dd-9569-3c01b06b52f0" />


<img width="961" height="1079" alt="Screenshot 2025-10-05 085516" src="https://github.com/user-attachments/assets/01a47db5-2680-4df1-8a40-a81b1d50a5a4" />  

we checked the slack value once again:  

<img width="957" height="1079" alt="Screenshot 2025-10-05 085555" src="https://github.com/user-attachments/assets/8eb8f0fc-bb3c-405c-be3e-f67ddeb4a9e6" />

```bash
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/04-10_10-12/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
# then we re run the POST CTS (1) commands ran earlier, to observe changes
```
<details>
  make sure to add the following commands:    
<li> # Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup   
</li>
</details>



<img width="960" height="1079" alt="Screenshot 2025-10-05 085910" src="https://github.com/user-attachments/assets/0ff563d3-113b-4b3e-8bb7-d61f136582e6" />   

<img width="953" height="1079" alt="Screenshot 2025-10-05 091404" src="https://github.com/user-attachments/assets/2a73ce32-9cab-44a3-8912-4580181ebb9d" />  

<img width="956" height="1079" alt="Screenshot 2025-10-05 091437" src="https://github.com/user-attachments/assets/2fa49088-dae1-420c-840c-e06a933617c3" />  

<img width="957" height="1079" alt="Screenshot 2025-10-05 091556" src="https://github.com/user-attachments/assets/09a0fce6-e295-4c07-b794-a07c24de7535" />    


# Power Distribution Network And Routing  
A PDN (or Power Distribution Network) is the complete path that delivers power from the supply to each transistor inside a chip.
It includes wires, PCB traces, bumps, package pins, on-chip metal layers, and vias.

Along this path, resistance, capacitance, and inductance cause the voltage at the transistors to drop or fluctuate (not perfectly equal to the power supply).  [sourced_https://semiengineering.com/knowledge_centers/low-power/low-power-design/power-delivery-network-pdn/]   

Commands used:  
```
gen_pdn
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 18-pdn.def &
#commands can be different so always cross-check
```
<img width="953" height="1079" alt="Screenshot 2025-10-05 093404" src="https://github.com/user-attachments/assets/d81b9186-02ea-4964-a900-e556070f3170" />  


<img width="965" height="1079" alt="Screenshot 2025-10-05 092100" src="https://github.com/user-attachments/assets/423eb47d-3c7c-48d6-91f4-670da8541c93" />  

 
 then, we ran `run_routing` for detailed routing.  
<img width="958" height="1079" alt="Screenshot 2025-10-05 094954" src="https://github.com/user-attachments/assets/d9ece3fa-8c50-40d9-8882-46662d2cbf63" />    

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```
<img width="961" height="1079" alt="Screenshot 2025-10-05 095508" src="https://github.com/user-attachments/assets/f39a3805-2348-4ebc-b28f-c9ce8c0582c9" />    

<img width="962" height="1075" alt="Screenshot 2025-10-05 095213" src="https://github.com/user-attachments/assets/d58b3848-cea1-4dd9-964f-bf768ef8056f" />  



## Parasitics Exxtraction    
Creating the environment for SPEF_EXTRACTOR:
<img width="956" height="1077" alt="Screenshot 2025-10-05 104417" src="https://github.com/user-attachments/assets/9c2f32b1-c245-4bb8-92a4-53ad4d724421" />    

We encountered the parsing error:  
<img width="962" height="1079" alt="Screenshot 2025-10-05 110606" src="https://github.com/user-attachments/assets/aa3c2937-ab93-4a82-8ca8-911547a2ce27" />    


and fixed it by going to the lef_util.py file and make the following changes in line number 380
<img width="958" height="1079" alt="Screenshot 2025-10-05 110553" src="https://github.com/user-attachments/assets/dec6eca3-3ee2-439a-8d62-f37a53033aa0" />    

then, we ran the below command for the extraction process:  
```ubuntu terminal
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-10_10-12/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/04-10_10-12/results/routing/picorv32a.def
```
whose result is seen below:  

<img width="960" height="1079" alt="Screenshot 2025-10-05 112559" src="https://github.com/user-attachments/assets/c3586f3d-1947-40c3-ac2e-0c6f639b9fa3" />    


<img width="957" height="1079" alt="Screenshot 2025-10-05 112544" src="https://github.com/user-attachments/assets/fe918561-82d9-4d95-af8a-53f2bcf76a11" />    

<img width="967" height="1079" alt="Screenshot 2025-10-05 121655" src="https://github.com/user-attachments/assets/9fd11937-1deb-4607-9ada-b86ccf71505e" />  


<img width="960" height="1079" alt="Screenshot 2025-10-05 121904" src="https://github.com/user-attachments/assets/57bbff99-4475-48d2-83db-efb04dd12587" />      
Final-Timing Reports after Parasitics Extraction:  

<img width="962" height="1079" alt="Screenshot 2025-10-05 122006" src="https://github.com/user-attachments/assets/1daedd99-a850-43b5-9833-4fd56da257b4" />  

 ## Conclusion

* Understood **ASIC Back-End design flow** using OpenLane & Magic
* Performed **RTL-to-GDSII flow** for `picorv32a` design
* Created and simulated a **custom inverter** in Magic + ngspice
* Learned **DRC, placement, floorplan, and SPICE netlist extraction**
* Gained **hands-on experience** with open-source PDKs and EDA tools

---   
Author: Akshit Kapoor  

Affiliation: B.Tech ECE — VLSI & Embedded Systems  
 
Year: 2025  

Tools: OpenLANE · Magic · OpenROAD · ngspice  

Design: picorv32a (RISC-V Core)  

---  




  



 




  
  
  
















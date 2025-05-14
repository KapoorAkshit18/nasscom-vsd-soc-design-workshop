# nasscom-vsd-soc-design-workshop
## 2 weeks workshop (Digital VLSI)
<details>
  <summary> INTRODUCTION </summary>
2 week workshop strucured 5 days and example:  
  below first part is the main section i.e sky130 day 3 after - is its topic and SKY130_D3_SK2 is sub section SKY_L9 is its sub-sub section.This was the format the video lectures were organized.
Sky130 Day 3 - Design library cell using Magic Layout and ngspice characterization
SKY130_D3_SK2 - Inception of Layout ÃÂ CMOS fabrication process
SKY_L9 - Lab steps to create std cell layout and extract spice netlist

EDA tools and opensource being an advantage.The workshop includes short videos and gives a good understanding for how chip design process forks.It tells how ASIC design flow works with more emphasis on the Back-End.
The Back-End usually involves steps like Synthesis,STA of the .v file then Design for Testability (DFT), Physical Design, then Physical Verification and finally the GDS-II file creation.Gds is the file saving format given to the foundries and normally it is in binary involving geometric shapes.

VLSI which stands for Very Large Scaling Industry refers to the scaling of size and increment of the transistors numbers on a single chip.

Further more chip architecture was discussed along with basic CMOS(complementary metal oxide semiconductor technology) concept that tells the reason for the steps done in the backend. Further more the workshop was equipped with the labs and assignment as well, which gives hands on experience, and practical insights of the backend process.



Virutal machine by oracle is utilized as most of the VLSI tools are based on linux so it provides isolated environment for working effectively.Linux has more advantage and for critical process like chip design which is the brain of any device or machine is a preferred choice.This documentation is more of picture based (means do the steps by keeping the images as a reference in your mind) so follow accordingly.

Magic Tool
As per Fossi Dial up 
Magic tool is more than DRC, it can read and write GDS.It can extract and netlist (SPICE file).LEF(Library Exchange File)/DEF(Design Exchange File) compatible.Wiring refers to physical joining of the network elements whereas routing defines rules for that.This feature is also included in the Magic.Plots are available for the analysis of the results in a graphical manner.
More features
- Paint and Erase 
- Instead of bins it works on single base 

   Labs along with the assessments are conducted.

  
</details>
Linux Commands used throughout the session



**Lab 1** : To open the openflow 
1. type `docker` <!-- make sure you are in openlane working directory whose path is /desktop/work/tools/openlane_working_dir/openlane -->
2. type second command `./flow.tcl -interactive`   <!-- this will open openlane in an interactive mode -->
3. 
Linux commands used:
```
cd    // to change directory 
ls    // to list items
ltr   // list in chro order
pwd   // shows current directory
cd ../  // makes the directory levele two step up 
```
![start](https://github.com/user-attachments/assets/08584779-4e80-4f0a-85ad-b2579e5685a7)

**LAB 2** To run synthesis and floorplan 
after openlane is opened type command `prep -design picorv32a`
after seeing the success preperation message like below  

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



**Lab**  To create layout of the picorv32a

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
















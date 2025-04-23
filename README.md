# nasscom-vsd-soc-design-workshop
## 2 weeks workshop (Digital VLSI)
<details>
  <summary> INTRODUCTION </summary>
EDA tools and opensource being an advantage.The workshop includes short videos and gives a good understanding for how chip design process forks.It tells how ASIC design flow works with more emphasis on the Back-End.
The Back-End usually involves steps like Synthesis,STA of the .v file then Design for Testability (DFT), Physical Design, then Physical Verification and finally the GDS-II file creation.Gds is the file saving format given to the foundries and normally it is in binary involving geometric shapes.

VLSI which stands for Very Large Scaling Industry refers to the scaling of size and increment of the transistors numbers on a single chip.

Further more chip architecture was discussed along with basic CMOS(complementary metal oxide semiconductor technology) concept that tells the reason for the steps done in the backend. Further more the workshop was equipped with the labs and assignment as well, which gives hands on experience, and practical insights of the backend process.



Virutal machine by oracle is utilized as most of the VLSI tools are based on linux so it provides isolated environment for working effectively.Linux has more advantage and for critical process like chip design which is the brain of any device or machine is a preferred choice.

Magic Tool
As per Fossi Dial up 
Magic tool is more than DRC, it can read and write GDS.It can extract and netlist (SPICE file).LEF(Library Exchange File)/DEF(Design Exchange File) compatible.Wiring refers to physical joining of the network elements whereas routing defines rules for that.This feature is also included in the Magic.Plots are available for the analysis of the results in a graphical manner.
More features
- Paint and Erase 
- Instead of bins it works on single base 

   Labs along with the assessments are conducted.

  
</details>



**Lab 1** : How to open the openflow
Linux commands used:
```
cd    // to change directory 
ls    // to list items
ltr   // list in chro order 
```
![start](https://github.com/user-attachments/assets/08584779-4e80-4f0a-85ad-b2579e5685a7)

**LAB 2** To run synthesis and floorplan 

The folder with timestamp is created where all of the results for the design is stored
![image](https://github.com/user-attachments/assets/844248e7-5d1a-4ec8-a863-d3bd801ff187)

The picorv32a design compilation

![image](https://github.com/user-attachments/assets/070d462c-608f-41eb-a1ce-eb7f5a3be5c9)

The synthesized results are seen by  `less` command

![image](https://github.com/user-attachments/assets/bbf5b85b-3120-4614-9a4d-da4b756f135d)
![image](https://github.com/user-attachments/assets/66470a0a-7025-4dfa-95d0-e0e1f7fdf9bf)

Assessment 1 flop ratio 

Equals to  10.84 percentile 

Assessment 2 area of the die 

 die height  and die width calculation by subtracting down leftmost corner from top rightmost corner == 443587.2122325 in microns squar


**Lab**  To create layout of the picorv32a


![image](https://github.com/user-attachments/assets/71594757-1148-4315-baa7-d290df83a779)



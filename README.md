# Picorv32-SOC Design -using-Open-source-tools

WorkShop is focused on understanding the concepts involved in SOC design, 
from RTL to GDSII using Open Source tools based on 180nm PDK .
It helps us to gain concepts of PD flow practically ,some key take aways 
from this workshop are basic understanding to Open Source tools, IC terminologies ,
RISCV, Floorplanning , PDk's , SPICE simulations,CMOS 16 mask fabrication process ,
CTS ,Routing ,STA, DRC .

# Contents
- **Day 1**: Introduction to IC terminologies & Open source tools & **RISCV** based ***PicoSOC***. 
- **Day 2**: Floorplanning Techniques & Introduction to library cells ,Placement .
- **Day 3**: Design & Characterization of a library cell using **Magic** tool & **Ngspice** simulations .
- **Day 4**: Timing models ,CTS & Signal Integrity 
- **Day 5**: Routing & SPEF file format 

### Day 1 : Introduction to IC terminologies & Open source tools & **RISCV** based ***PicoSOC***.
**Day1** starts with introduction to IC terminologies Package,Core,Die,Ip's & RISCV arch .
How an software  application linked with Vlsi , concept of compiler & assembler ,overview of Picorv32 SOC.

![Day_1_pic2](https://user-images.githubusercontent.com/74585082/99905038-67cc0b80-2cf4-11eb-885c-ec72aa299739.PNG)
![Day-1_pic1](https://user-images.githubusercontent.com/74585082/99904981-0ad05580-2cf4-11eb-88df-3d77966bb8aa.PNG)

Now coming to flow ,here comes the **synthesis** which is process of converting HDL code to gate level netlist , it takes RTL code & technology related info files .

![Day1-SYNt](https://user-images.githubusercontent.com/74585082/99905720-acf23c80-2cf8-11eb-82eb-b40b68dc3568.PNG)

Result of syntheis is shown in the below snap,which gives info about various design components .

![Day1-statistics](https://user-images.githubusercontent.com/74585082/99905772-edea5100-2cf8-11eb-9e63-8de0ddb2a51e.PNG)

Different Open-Source tools Used at different stages in RTL to GDSII flow are below  .
- **Synthesis     : Yosys**
- **Placement,CTS : Graywolf** 
- **Routing       : Qrouter**
- **Timing**      : **Opentimer**

### Day 2 : Floorplanning Techniques & Introduction to library cells ,Placement.
**Day 2** comes up with interesting concept floorplan which is important step in PD flow .As this step includes estimation of area (Aspect ratio & Utilization factor) ,
Pin placement & pre-placed cells placement .A good floorplan makes the implementation easier in further steps ,where as bad floorplan causes viceversa .
So it's important to understand the design requirements in the starting stage & make changes of pin placement & pre-placed cell placement.
















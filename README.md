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

Open-Source tools Used at different stages in RTL to GDSII flow are below .
- **Synthesis     : Yosys**
- **Placement,CTS : Graywolf** 
- **Routing       : Qrouter**
- **Timing**      : **Opentimer**
- **Layout**      : **Magic**

### Day 2 : Floorplanning Techniques & Introduction to library cells ,Placement.
**Day 2** comes up with interesting concept **Floorplan** which is important step in PD flow .As this step includes estimation of area (Aspect ratio & Utilization factor) ,
Pin placement & pre-placed cells placement, power planning .A good floorplan makes the implementation easier in further steps ,where as bad floorplan causes viceversa .
So it's important to understand the design requirements in the starting stage & make changes of pin placement & pre-placed cell placement.

![Day_2_pic1](https://user-images.githubusercontent.com/74585082/99907931-97cfda80-2d05-11eb-9900-24a60710c481.PNG)

**Placement**
In this stage all standard cells are placed in the design ,this is different parameters Timing ,congestion driven ,Power opt based .Timing & Routing congestion is based on placement quality. 


#### Library Characterization 

**Library** is a collection different logical cells with different functionality ,different vt types & with different sizes ,according to required specs .
I/p's for characterization of a library of a cell are PDK's ,DRC &LVS rules ,SPICE Models & User defined specs .Steps followed by i/p's are 

- **Circuit Design** --> To model the cmos logic according to library requirement like W/L ratio ,Drain current requirement .O/p of this is Circuit description language .
- **Layout Design**  --> By Using Circuit need to implement in terms of layout using **Magic tool**. Layout is doneusing **Eulers path algorithm** & **Stick diagram** .O/p's of this include GDSII, LEF , Extracted Spice netlist .

![day_2_layout](https://user-images.githubusercontent.com/74585082/99913836-e0948d00-2d1f-11eb-8275-54eaf6fc02f3.PNG)


- **Characterization** --> We need to use o/p's of circuit & layout design to characterize a logical cell 
                    - Read SPICE model file from foundry which includes PMOS & NMOS parameters .
                    - Read the extracted spice netlist .
                    - To define the behaviour of logical cell .
                    - Read the subckt of logical cell ,if any .
                    - Add power sources & apply stimulus .
                    - Provide o/p load capacitance.
                    - Perform necessary Dc & tarnsient simulations using SPICE tools ,Which in turn provides info of timing ,noise ,power .libs if a cell .

### Day 3: Design & Characterization of a library cell using Magic tool & Ngspice simulations .


















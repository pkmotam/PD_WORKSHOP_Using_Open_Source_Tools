# Picorv32-SOC Design using Open source tools

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
- **Day 5**: Routing & DRC, SPEF file format Introduction 

### Day 1 : Introduction to IC terminologies & Open source tools & **RISCV** based ***PicoSOC***.
____

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
____

**Day 2** comes up with interesting concept **Floorplan** which is important step in PD flow .As this step includes estimation of area (Aspect ratio & Utilization factor) ,
Pin placement & pre-placed cells placement, power planning .A good floorplan makes the implementation easier in further steps ,where as bad floorplan causes vice-versa .
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


**Characterization** --> We need to use o/p's of circuit & layout design to characterize a logical cell 
 - Read SPICE model file from foundry which includes PMOS & NMOS parameters .
 - Read the extracted spice netlist .
 - To define the behaviour of logical cell .
 - Read the subckt of logical cell ,if any .
 - Add power sources & apply stimulus .
 - Provide o/p load capacitance.
 - Perform necessary DC & transient simulations using SPICE tools ,Which in turn provides info of timing ,noise ,power .libs of a cell .

### Day 3: Design & Characterization of a library cell using Magic tool & Ngspice simulations .
____

On Day-3 talk is on SPICE deck creation , simulations & Layout creation of CMOS inverter .

 **Spice deck** creation involves in below steps .After this we perform DC & transient simulations to meet user specs .
- Component connectivity.
- I/p's & Tap points.
- Component values .
- O/p Load Capacitance.
- Supply volatge & I/p gate voltage .

![Day_3_spice_deck](https://user-images.githubusercontent.com/74585082/99931989-a4dbe080-2d7c-11eb-855c-8b3d71a05f88.PNG)

![Day_3_dc_simulation](https://user-images.githubusercontent.com/74585082/99932006-af967580-2d7c-11eb-903e-171c000da7df.PNG)

Parameters that define the robustness of cmos invereter are ***Switching threshold (Vm)*** .It is defined as point where *vin =vout* . By using waveforms how W/L ratio impacts rise delay & fall delay of an inverter .

- Rise Delay : Time during the transition when o/p swithces from 20% to 80% of max value .
- Fall Delay : Time during the transition when o/p swithces from 80% to 20% of max value .
- Propagation Delay : Diff in time at 50% of i/p to o/p transistion ,when o/p swicthes after appliation of i/p .

**Art of drawing Layout** ,this includes introduction on how to draw layout & rules in drawing layout which varies based process you are design, Euler's method of drawing layout which reduces routing , inturn reduces parasitics impact ,also there is an comparision drawn b/w the layout drawn with & with out Euler's method to understand how this approach makes layout robust .Tool used for drawing layout is **Magic Tool** . Once the Layout is ready we extract parasitics & spice netlist to compare the **pre-layout** & **post -layout** transient simulations using SPICE tool (ngspice) . There will be slight delay chnages due to addition of parasitics post -layout ,but the waveform remains same .

![Day_3_layout](https://user-images.githubusercontent.com/74585082/99935377-91ce0e00-2d86-11eb-8525-e7b4ff8e94b2.PNG)

![Day_3_tran_pre_layout spice](https://user-images.githubusercontent.com/74585082/99932001-aad1c180-2d7c-11eb-9a01-0d825ec14f34.PNG)

#### CMOS 16 mask Fabrication process 

A 16 Mask Cmos Fabrication process is explained in detail from scratch includes various concepts like Diffusion ,Ion implanatation ,Etching , Deposition ,Chemical mechanical polishing .Following are the major steps involved 
- Create Active regions .
- Formation of Nwell & Pwell regions .
- Formation of gate terminal .
- Lightly doped drain formation .
- Source -Drain formation .
- Local interconnect fromation .
- High -level metal formation .

### Day 4 : Timing models ,CTS & Signal Integrity
____

On Day-4 workshop is on delay tables & how delay tables are characterized . Cell delay is captured based on I/p slew & o/p load . In Library there will be look up tables defined for each cell related delays for different combinations of I/p slew's & O/p load values . Intorduction timing analysis based on ideal & real clocks ,CTS buliding , & discussed various terms timing related terminologies Skew ,latency , Setup time & Hold time , Uncertainity .
- Setup time : It is the minimum amount of time required for the data to reach the capture flop ,beofre the active edge of clock reaches it .
- Hold time  : it is the minimum amount of time the data should be stable after clock edge reaches the flop .
- Skew       : It is arrival of clock at two consecutive clock pins of a sequential elements (Flops) .
- Clock Uncertainity : It is deviation in the arrival of clock edge w.r.t ideal arrrival ,due to Jitter & noise .

**Timing analysis with ideal & real clocks**

Setup & hold timing analysis with ideal & real clocks differ with some parameters like uncertainity ,network latency (clock n/w delay) as parasitics comes into picture .

![Day_4_Setup](https://user-images.githubusercontent.com/74585082/99940251-ca271980-2d91-11eb-9490-f6f5c302d026.PNG)

**CTS:**
Clock tree synthesis is important step in builiding a clock to all clock pins in the design ,it involves in adding buffers & inverters to minimize the skew & load for better timing QOR & to meet setup & hold requirements using H-tree algorithm .

**Signal Integrity:**
As technology shrinks the impact of coupling capcitance increases ,which inturn may impact the nearby nets by changing the functionality of victim net .To avoid this we use technique called sheilding .

![Day_4_cts](https://user-images.githubusercontent.com/74585082/99940874-0e66e980-2d93-11eb-880f-6281fdd33bfa.PNG)

We have created a clock as below & stored it in a SDC file & propogated it to verify setup & hold time of design .Below commands are related to **opentimer** used to read the inputs required for timing analysis .

* create_clock -name clk -period 2.5 -waveform {0 1.25} [get_ports clk]
* read_liberty /usr/local/share/qflow/tech/osu018/osu018_stdcells.lib 
* read_verilog synthesis/picorv32.rtlnopwr.v
* link_design picorv32
* read_sdc picorv32.sdc
* report_checks

### Day 5: Routing & DRC , SPEF File format Introduction 
____

Final day, is about Routing & introduction of SPEF file format .

*Routing* is nothing but interconnection between standard cells & Macros based on the logical connections present in the netlist .This is done by algorithm named **LEE's algorithm** ,which creates routing grid & two points one is source ,other one is target .So the algorithm  does it by creating labels the adjacent grids &follow the same procedure until it meets the target .Once it reaches it find's out best possible way to reach to target by following DRC rules given by foundry .

![day_5_Routing](https://user-images.githubusercontent.com/74585082/99953223-0022c880-2da7-11eb-915f-0dd16ca5bee8.PNG)

![Day_5_routing_1](https://user-images.githubusercontent.com/74585082/99953301-17fa4c80-2da7-11eb-8ae3-f27844e7726e.PNG)

Once routing is done we have compared pre-layout & Post layout frequency ,by the below snaps ,we can observe there is a change in frequency due to parasitics impact .

![Day_5_pre_sta](https://user-images.githubusercontent.com/74585082/99995960-1b122e80-2de1-11eb-8552-eb7c390d9c3f.PNG)

![Day_5Post_layout_sta](https://user-images.githubusercontent.com/74585082/99995959-1b122e80-2de1-11eb-91b6-bf51545954d9.PNG)


#### DRC 
Design rule checks, once routing is done we need to determine whether the it is following the rules given by foundry to make the chip manufacturable ,Some of them includes
- Metal to metal spacing
- Metal width (Min,Max)
- Min Enclosure
- Poly to Poly Spacing
- Contact to Poly etc ...

#### SPEF
**STANDARD PARASITIC EXTRACTION FORMAT** is an IEEE standard for representing parasitic data of wires in a chip in ASCII format. Non-ideal wires have parasitic resistance and capacitance that are captured by SPEF. These wires also have inductance that is not included in SPEF.

SPEF file consists 4 sections 
- Header Section 
- Name Map Section 
- Top level port section 
- Parasitic description section 

* Header section consists of Design Name ,Parasitic extraction tool, Naming Styles, Units .
* SPEF allows to map long names to some numbers ,to reduce file size .
* PORT section contains all top level ports in design ,it might be an I/p ,O/p or bi-directional .
* Each extracted net will have a \*D_NET Section ,\*CONN, \*RES, \*CAP sections .

# Acknowledgements:

**Kunal Ghosh**, Co-founder (VSD Corp. Pvt. Ltd)

























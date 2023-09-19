# ADVANCED PHYSICAL DESIGN USING OPENLANESKY130

## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

<details>
<summary>How to talk to computers?</summary><blockquote>

<details>
<summary>Introduction to QFN-48 Package, chip, pads, core, die and IP</summary>
</details>

<details>
<summary>Introduction to RISC-V</summary>
</details>

<details>
<summary>From Software Applications to Hardware</summary>
</details>

</blockquote>
</details>


<details>
<summary>SoC design and OpenLANE?</summary><blockquote>

<details>
<summary>Introduction to all components of open-source digital asic design</summary>
</details>

<details>
<summary>Simplified RTL2GDS flow</summary>
</details>

<details>
<summary>Introduction to OpenLANE and Strive chipsets</summary>
</details>

<details>
<summary>Introduction to OpenLANE detailed ASIC design flow</summary>
</details>

</blockquote>
</details>


<details>
<summary>Get familiar to open-source EDA tools</summary><blockquote>

<details>
<summary>OpenLANE Directory structure in detail</summary>

```
cd work/tools
ls -ltr
cd openlane_working_dir/
cd openlane_working_dir/
ls -ltr
cd pdks/
ls -ltr
cd sky130A/
ls -ltr
cd libs.ref/
ls -ltr
cd ..
cd libs.tech/
ls -ltr
```
+ The library we will be working with is SkyWater130A, which has recently become open source.
+ libs.ref contains the timing details etc.
+ libs.tech contains the specific to the tool.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ce8d5c45-8ee9-4c7c-9b73-10432a7caafa)

+ We will be working on sky130_fd_sc_hd. 'fd' is an abbreviation of foundry.
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/69f99c3b-9ba7-4378-8a0b-995077bea6e4)

```
cd..
cd libs.ref
cd sky130_fd_sc_hd
cd lib
ls -ltr
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/836debc1-e115-4f17-9a52-9a888865639d)

+ This is the directory we will be working in.
```
~/Desktop/work/tools/openlane_working_dir/openlane$
```
</details>

<details>
<summary>Design Preparation Step</summary>

+ To invoke openlane, use the following commands.
```
docker
pwd
./flow.tcl -interactive
package require openlane 0.9
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fbd785eb-7b39-4c98-8194-2135095d2e7f)

+ How the config.tcl looks like. ls -ltr
```
cd designs
cd picorv32a/
ls -ltr
cd src
ls - ltr
cd ..
less config.tcl
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d8d831f4-61cf-4a0f-a8a2-2095f46bfd59)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ddf5f7da-7eca-4061-9e84-1ab565419c69)

+ Design preparation code

```
prep -design picorv32a
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6c79c9f9-52db-4f79-8055-eaaec67ca868)

</details>

<details>
<summary>Review files after design prep and run synthesis</summary>

```
cd runs
ls -ltr
cd 18-09_06-22/
cd tmp
ls -ltr
less merged.lef
```
+ The "runs" directory will be created in the picorv32a directory.
+ In that "runs" folder, a directory with today's date will be created which is Sept 18th.
+ In the sept 18th folder, we can see the merged.lef

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9d0e16b2-b459-4d64-a32d-6ccf904159a0)
  
+ This contains all the wire level information, vias and below that is the cell level information.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8008d146-b6d8-4766-a219-f85aaf38da14)

+  The results and reports directories will have sub-folders which will be empty as of now since nothing has been run.

+ The config.tcl basically shows what are all the default parameters the run file takes.


```
less config.tcl
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6f1382a6-76ff-4d7d-a8a1-9b15c47bbc97)

+ The cmds.log file logs all the commannds that the user has typed.
```
less cmds.log
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/472fa1cb-ee0b-4189-a0e3-caa5dfed1d33)

+ Type the follwing command the synthesis will be run along with ABC.
```
run_synthesis
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/5daa544e-d396-4754-a4bb-bdc2562010b5)
</details>

<details>
<summary>OpenLANE Project Git Link Description</summary>

+ The github link to find all the information about openlane is in
```
github.com/efabless/openlane
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/79f76ba1-66c5-4585-952c-fbad78d53377)

+ The follwing two youtube videos are also helpful in learning openlane using skywater130 pdk.
```
https://www.youtube.com/watch?v=EczW2IWdnOM&pp=ygUOZm9zc2kgZGlhbCB1cCA%3D
https://www.youtube.com/watch?v=Vhyv0eq_mLU&pp=ygUOZm9zc2kgZGlhbCB1cCA%3D
```
</details>

<details>
<summary>Steps to characterize synthesis results</summary>

+ STA and ABC run has been done already.
+ Let us see the flop ratio. Flop ratio is defined as

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/33fda301-4d95-48e3-ab07-2e8b6f0910b1)

+ From the statistics report, we can see that the number of DFFs is 1613 and the total number of cells is 14876.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9d81e55c-ea8c-4d18-94d2-a223cd5d2942)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/680f0215-08e3-42a4-8387-38168b425f9b)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/e6e5fa7b-5a11-428f-afe9-e01bf6d359b6)

+ Let us check what is there in the runs folder.
+ First the synthesis in results folder.

```
cd reuslts
cd synthesis
less picorv32a.synthesis.v 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8d5ab0fb-a14b-42bf-b31e-0ce31b3ab345)

+ Next let's check the synthesis in reports folder. We will get the statistics that was displayed earlier.
```
cd reuslts
cd synthesis
less picorv32a.synthesis.v 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/533dadb5-716b-41e9-8cc4-7398c0e3df50)

+ Similarly we can also check the opensta report.
```
less 2-opensta.timing.rpt 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/86d1fa4e-5754-4b4c-a2cf-138f4d185f0a)

</details>

</blockquote>
</details>


## Day 2 - Good floorplan vs bad floorplan and introduction to library cells

<details>
<summary>Chip Floor planning considerations</summary><blockquote>

<details>
<summary>Utilization factor and aspect ratio</summary>

+ Utilization Fator is given by:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b97d52a8-5e42-45f1-b760-bbfad0330787)

+ If the utilization is 100%, then if we want to add any more cells, we cannot. Therefore, usually 50-60% is done to keep some space in case we want to add more cells in the future, for eg: buffers for optimization.

+ Apect Ratio is given by:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9838c39f-79fb-4a75-bad1-996109745105)

+ Whenever aspect ratio is 1, it means that the chip is a square. If it is anything other than 1, then it means that the chip is a rectangle.
</details>

<details>
<summary>Concept of pre-placed cells</summary>

+ Say there is a combinational logic with huge circuit. If parts of the logic are being used multiple times in different places, then we can cut the logic into few parts, arrange them into blocks and black box them. That block need not be implemented in every place where it needs to be used. It can be implemented in a few places and can be reused whenever needed. This is the concept of reusability of cells.
+ The arrangement of these IPs/macros in a chip is called Floorplanning.
+ These IPs/blocks have user defined locations, and hence are placed in chip before automated placement-and-routing and are called pre-placed cells. Eg. Memory, clock gating cell, comparator, Mux. These automated processes do not touch these preplaced cells.
</details>

<details>
<summary>De-coupling capacitors</summary>

+ The location of pre-placed cells have to be very well defined.
+ The pre-placed cells have to be surrounded by decoupling capacitors.
+ The wire which connects Vdd and the gates has a resistance which and due to that the voltage drops below noise margin, then logic 1 won't be detected or rather whether it can be detected or not cannot be guaranteed.
+ One way to solve this problem is to surround a piece of circuit with a huge capacitor. This capacitor decouples the circuit from the main supply. Whenever there is a switching activity hapeneing, the capacitor will send the current to the circuit.
+ Since the decoupling capacitors are placed very near to the circuitry, there is hardly an voltage drop.
+ So the blocks will function properly since the supply is provided by the decoupling capacitors. 
</details>

<details>
<summary>Power planning</summary>

+ Assume the previous circuit which was decoupled with capaciors has been replicated multiple times in the circuit.
+ Now assume there is a 16 bit line which connects these replicated blocks from Vdd line and that there is a connection between two of these replicated blocks. Now 16 bit line means there are 16 capacitors and if it charged, it is logic 1 and if it is discharged, it is logic 0.
+ If all the logic 1s are set to go to logic 0, then the all of them have to get discharged to the ground.
+ Since there is a single ground line and all of them go to logic 0 together, the ground which was supposed to be at logic 0 get's a voltage spike. This is called ground bounce.
+ If the voltage level of this ground bounce goes beyond the noise margin, we will get an undefined state.
+ If suppose the reverse process had to happen where all the capacitors had to charge to logic 1, then all of them demand voltage from the Vdd.
+ Again since there is a single Vdd line, there will be a voltage droop. As long as thie droop is within the noise margin, nothing will happen. Once it goes beyond the noise margin, it is said to be in an undefined region and the circuit can interpret the voltage as logic 0 or logic 1 and it is not in our control.
+ If there were multiple power supplies and multiple ground lines, this problem would not have occurred.
+ That is what do. We put multiple ground lines and multiple vdd lines like a mesh and inside the boundaries the cells sit and the Vdd and gnd lines themselves make the mesh boundary. 
+ A cell will take power from it's nearest source and dump it's power in its nearest gnd.
</details>

<details>
<summary>Pin placement and logical cell placement blockage</summary>

+ The connectivity information between gates is coded using VHDL/Verilog language and is called netlist.
+ Input and output lines can be placed in the space between core and die.
+ Blocks are placed nearer to the inputs they use. If their output lines are far, buffers are used. No cells can be placed in the area where another cell/block is placed.
+ Clock path lines are bigger than the other pins because they are ones which drive the circuit. So we need least resistance for them.
+ Now we block the area where pins are placed. This makes sure that the automated placement tool does not place cells in that area since it is reserved for pin placement.
+ Once this blocking is done, our Floor Plan is ready for placement and routing step.
</details>

<details>
<summary>Steps to run floorplan using OpenLANE</summary>

+ The defaults for various parts of the flow is in the configurations folder.
+ The heirarchy of selecting default values are as follows:
``` 
floorplan.tcl - in configurations directory
conifg.tcl - in picorv32a directory
sky130A_sky130_fd_sc_hd_config.tcl - in picorv32a directory
```
+ The following is a snap of what is there in the configuration directory.
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less README.md 
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/configuration$ less floorplan.tcl 

```
+ Synthesis - defaults

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/544c1373-8da9-4919-9026-4a1046b84dde)

+ Floorplanning - defaults

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f7cfff6c-a4c3-486b-825d-e5e9b6d53bdc)

+ Placement - defaults

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a3ee7653-87c9-4661-91f2-e8f3ddf498d4)

+ Running Floor plan
```
run_floorplan
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/86034942-d2ec-44e5-80d8-8afffa033217)

</details>

<details>
<summary>Review floorplan files and steps to view floorplan</summary>

+ Checking the runs directory:
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs$ cd 18-09_06-22/
cd results/floorplan
less picorv32a.floorplan.def
```
+ There will be one .def (design exchange format) file in the floorplan directory.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b04cb7a8-ec0a-4f7f-8d4e-95d961994419)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/764a69f7-f664-45ea-9c73-6d7d9b8194ca)

+ Die Area is

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/402ecdd3-de5a-4757-91b3-1571e28ee60e)

+ Now opening magic to view the floorplan

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b06c9c99-7af5-4ffc-97ae-ac08afb4e87f)

</details>

<details>
<summary> Review floorplan layout in Magic</summary>

+ We can see that the pin placement is equidistant.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7539ad18-9785-4114-bfe4-9e4edccbb6a2)

+ The selected pin in the above snap is in metal layer 3

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/aa69b1f7-70e2-4adc-95e2-07ebe9914adb)

</details>

</blockquote>
</details>


<details>
<summary>Library Binding and Placement</summary><blockquote>

<details>
<summary>Netlist binding and initial place design</summary>

+ The library file contains all the information about the size,shape, delay, I/O conditions etc. information about the cells.
+ It also contains different variations of the same cells. Eg. different shapes and size, different speeds etc.
+ Once we have all the shapes and sizes, it is time to place the netlist on the floorplan.
+ Placements are done such that the there is not much delay between input and output and also the flip flops.
</details>

<details>
<summary>Optimize placement using estimated wire-length and capacitance </summary>

+ Cells have to also be placed keeping in mind the other cells which have to be placed.
+ Even then some extra distance signals will have to cover to reach the output from cells or from input to cells.
+ To solve this problem, we do optimized placement.
+ This is the stage where we estimate wire length and capacitance and based on that insert repeaters.
+ Repeaters are basically those components which recreate and reconfigure the signals which are input to them and send them to the output, eg. buffers.
+ These repeaters maintain signal integrity.
</details>

<details>
<summary>Final placement optimization</summary>

+ Connections between cells also have to be optimized.
+ Buffers should be added at the right places.
+ After this do setup timaing analysis with ideal clocks.
</details>

<details>
<summary>Need for libraries and characterization</summary>

+ First step in IC design flow is logic synthesis - converting design to legal hardware. Gates repreesnt the RTL logic.
+ Next step is the floor planning. We take the circuit from the synthesis and decide the shapes and sizes of the gates which will in turn determine the dimensions of the core and die.
+ Next step is to do placement. We do placement in way that the initial timing conditions are met.
+ Next step is the clock tree synthesis. This step is to make sure that all the cells dependent on clock receive the clock signal at exactly the same time.
+ Next step is routing. 
+ Next we do static timing analysis
</details>

<details>
<summary>Congestion aware placement using RePlAce</summary>

+ We have to remove congestions and overlapping between cells.
+ Let's run placement
+ We have to converge the overflow
+ To do placement 
```
run_placement
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/97b79538-8544-461b-ba90-cc337e15bda6)

+ To view placed cells
```
vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-09_06-22/results/placement$ magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/0e59e337-a026-45c2-8647-ac214a7887ad)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f6a11e6a-5d74-4513-9f69-b9272658069f)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4a23c572-b9e4-47e4-a83e-40b6bd78451e)

</details>

</blockquote>
</details>


<details>
<summary>Cell design and characterization flows</summary><blockquote>

<details>
<summary>Inputs for cell design flow</summary>

+ Cell design flow consists of three parts
1. Inputs
2. Design steps
3. Outputs

+ Let us look at Inputs
- Inputs contain PDKs, DRC and LVS rules, SPICE models, library and usr-defined specs.
- It has tech files which tell about labmda based rules.
- SPICE model contains physical parameters like Vth, gamma, capacitance etc. These are given by the foundry.
- User defined specs are things like cell height which is dependent on the power and ground lines which can be set by the user. Cell width is dependent on the timing data which can again be chosen by the user. Metal layers are also user defined specs. Pin locations are also user defined. Drawn gate length also can be set by user. User is library developer.
</details>

<details>
<summary>Circuit design step</summary>

+ Design steps involves three sub steps:
  1. Circuit design
  2. Layout design
  3. Characterization

+ Circuit Design has two parts:
  1. Implement the function itself
  2. Model the CMOS in order to meet the library requirements.
  3. The output that we get from this is called the CDL(Circuit Description Language)
</details>

<details>
<summary>Layout design step</summary>

+ Next step we need to do Euler's path - path which has been traced only once.
+ After getting the Euler's path, we should draw the stick diagram which has all the connections.
+ Next step is to convert the stick diagram into Layout according to the DRC and user defined specs.
+ Now we use a tool to see the layout. Then we extract the parasitics out of the layout and characterize it in terms of timing data.
+ The output of the layout is GDSII, LEF (defines width and height of the cell), extracted spice netlist(.cir) which gives the resistance and capacitance of each and every element.
</details>

<details>
<summary>Typical characterization flow</summary>

+ First step is to read in the model which is given by the foundry.
+ Second step is to read the extracted spice netlist.
+ Third step is to recognize the bahaviour of the buffer.
+ Fourth step is to read the sub-circuit of the inverter
+ Fifth is to attach necessary power sources.
+ Sixth is to apply the right stimulus.
+ Seventh is to provide the necessary output capacitances.
+ Eighth step is to provide the necassary simulation commands., like transient, DC, AC etc.
+ Next is to feed all the above steps as a configuration file to a characterziation software called GUNA.
+ GUNA will generate timing, noise and power.libs
+ There are three characterziations types - Timing characterization, Power characterization, Noise characterization.
</details>

</blockquote>
</details>


<details>
<summary>General timing characterization parameters</summary><blockquote>

<details>
<summary>Timing threshold definitions</summary>

+ slew_low_rise_thr - Slope of lower part of rising signal, usually 20%.
+ slew_high_rise_thr - Slope of higher part of rising signal, usually 20%.
+ slew_low_fall_thr - Slope of lower part of falling signal, usually 20%.
+ slew_high_fall_thr - Slope of lower part of falling signal, usually 20%.
+ in_rise_thr - Input rising signal threshold, around 50% of the signal.
+ in_fall_thr - Input falling signal threshold, around 50% of the signal.
+ out_rise_thr - Output rising signal threshold, around 50% of the signal.
+ out_fall_thr - Output falling signal threshold, around 50% of the signal.
+ To calculate the delay between signals subtract the output-input values from the above four parameters.
</details>

<details>
<summary>Propagation delay and transition time</summary>

+ Poor choice of threshold points will result in negative propagation delays.
+ Large length of wire between cells will result in large slew which will give negative propagation delay even at 50% level.
```
Propagation  Delay: time(out_*_thr)-time(in_*_thr)
```
+ Transition time is the time taken by a signal to transition from logic 0 to logic 1.
+ For rising signal:
```
Transition time = time(slew_high_rise_thr) - time(slew_low_rise_thr)
```
+ For falling signal
```
Transition time = time(slew_high_fall_thr) - time(slew_low_fall_thr)
```
+ Two more important timing parameters are output current waveform and output voltage waveform.
</details>

</blockquote>
</details>


## Day 3 - Design library cell using Magic Layout and ngspice characterization

<details>
<summary>Labs for CMOS inverter ngspice simulations</summary><blockquote>

<details>
<summary>IO placer revision</summary>

+ Suppose we want to change the values of variables in cofiguration files, we have to copy variable name and use set command in docker to change the value.
+ I/O pins are placed in an equidistant manner. 
</details>

<details>
<summary>SPICE deck creation for CMOS inverter</summary>

+ SPICE Deck, we need to create it.
  1. Component connectivity information. 
  2. Component Values - W and L values of Pmos and Nmos and load capacitor value and source voltage values.
  3. Identify Nodes - Nodes are basically points in between which components/cells are present.
  4. Name the nodes
+ The order of pins in a transistor in SPICE deck is drain, gate, source, substrate.
+ The spice deck contains the following code:

```
*** MODEL Description ***
*** NETLIST Description ***

M! out in vdd vdd pmos W=0.375u L =0.25u
M2 out in 0 0 nmos W=0.375u L =0.25u

cload out 0 10f
Vdd vdd 0 2.5
Vin in 0 0.25

*** SIMULATION COMMANDS ***
.op
.dc Vin 0 0.25 0.05

*** .include tsmc_025um_model.mod ***
.LLIB "tsmc_025um_model.mod" CMOS_MODELS
.end
```

+ The words in '' in the following description are node names.
+ Cload is a capacitor connected between 'out' and '0' and has a value of 10f.
+ Vdd is supply voltage conected between 'vdd' and '0' and has value of 2.5.
+ Vin is supply voltage conected between 'in' and '0' and has value of 2.5.
+ In the '.dc' line we will sweep the Vin from 0 to 2.5 in steps of 0.05. This is to calculate the waveform at the output.
+ All the technology parameters like descriptions of nmos and pmos are given in the model file (.mod). That is how the code knows what is pmos and nmos.
+ W/L = 1.5

</details>

<details>
<summary>SPICE simulation lab for CMOS inverter</summary>
</details>

<details>
<summary>Switching Threshold Vm</summary>

+ Switching Threshold voltage, Vm, is the point where Vin = Vout, or are almost approximaetly equal.
</details>

<details>
<summary>Static and dynamic simulation of CMOS inverter</summary>
</details>

<details>
<summary>Lab steps to git clone vsdstdcelldesign</summary>

+ We will use the sykwater libraries for nmos and pmos from github.
```
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign/
ls -ltr
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/609f0495-03c3-42ed-b70d-4b020229a6de)

+ We are not going to make the inverter from scratch.
+ We will do the spice extraction and post layout spice simulations from the cloned repository.
+ sky130A.tech has been copied from the pdks folder into the cloned repository for ease.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/80a3a9a0-3510-4499-9f55-d7e2c5400eee)

+ To view the .mag file of the sky130A inverter:
```
magic -T sky130A.tech sky130_inv.mag &
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/60c10027-73f1-47ef-805e-07895fde4e1b)

</details>

</blockquote>
</details>


<details>
<summary>Inception of Layout Â CMOS fabrication process</summary><blockquote>

<details>
<summary>Create Active regions</summary>
</details>

<details>
<summary>Formation of N-well and P-well</summary>
</details>

<details>
<summary>Formation of gate terminal</summary>
</details>

<details>
<summary>Lightly doped drain (LDD) formation </summary>
</details>

<details>
<summary>Source and drain formation</summary>
</details>

<details>
<summary>Local interconnect formation </summary>
</details>

<details>
<summary>Higher level metal formation </summary>
</details>

<details>
<summary>Lab introduction to Sky130 basic layers layout and LEF using inverter  </summary>

+ When poly crosses n-diffusion, it is nmos and when poly crosses p-diffusion it is pmos.
+ The highlighted part in the below image as shown is an nmos.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/dc1eb504-184f-4761-9718-3796306f410f)

+ The highlighted part in the below image as shown is an pmos.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/da4cf776-e1c9-4fa6-b99f-375538294c77)

+ The highlighted part shows the connectivity between drain of pmos and drain of nmos.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a11e8138-b9c2-4329-be48-28cf86fbe4b0)

+ The highlighted part shows the connectivity between source of pmos and vdd.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ce68c648-1c89-4a36-84d7-8297db1be2e8)

+ The highlighted part shows the connectivity between source of nmos and gnd.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/148fc7fc-5280-47a0-a775-880a8e290e12)

+ LEF has all the information about the metal layers. It has no information about the logic part.
</details>

<details>
<summary>Lab steps to create std cell layout and extract spice netlist</summary>

+ For Bouding box creation:
+ llx - lower left x value
+ lly - lower left y value
+ urx - upper right x value
+ ury - upper right y value
+ If DRC violations occur, it can be seen by clicking on the drc tab in magic window and then the tkcon window the specifics of the DRC error will be displayed and in the magic window, the part where the error occurs is highlighted and zoomed in.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/3e3281a3-ae2c-4cee-a118-706bec48b7d8)

+ First we will do spice extraction of the layout that we have opened.
+ Type the following the tkcon window.
```
extract all
```
+ The .ext file has been extracted to the directory we were working in

 ![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/68a03450-d6b8-464c-8925-612ca4341c9c)

+ To do spice extraction. This will also extract parasitics.
```
ext2spice cthresh 0 rthresh 0
ext2spice
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d2931ed6-4d78-4767-9ab4-8231d9fccd79)

</details>

</blockquote>
</details>


<details>
<summary>Sky130 Tech File Labs</summary><blockquote>

<details>
<summary>Lab steps to create final SPICE deck using Sky130 tech </summary>

+ The .spice file looks like this:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/984d5db9-ab04-4142-bae9-20b76f272bb8)

</details>

<details>
<summary>Lab steps to characterize inverter using sky130 model files</summary>

+ Open ngspice
```
ngspice sky130_inv.spice
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/c5395bf3-ad2b-4c61-85cc-de44c64690b1)

+ Plot output vs time

```
plot y vs time a
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fc8b016c-52d2-436f-ab05-7aac1c5993c7)

+ Next is to characterize inverter.
+ We will check the 205 value first and then the 80% signal value
+ The following graph will be displayed for rise time.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/47f95375-768d-4f96-add5-04d2e125f729)

+ The value of the points which were of interest on the signal are:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a3ea88c6-13e2-4191-8ac4-7ec736d2c1bf)

+ The rise time is 0.039 ns
+ The following graph will be displayed for rise time.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/c97385e3-dff7-4a0b-908a-7af37da5a976)

+ The fall time is 0.02851ns.
+ The propagation delay graph would be:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/00a0e44b-9674-4f9a-b5a8-edb14ff4833f)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8a64e512-d285-40c5-8cad-7c3c4f923d12)

+ The propagation delay is 0.03725ns.
  
</details>

<details>
<summary>Lab introduction to Magic tool options and DRC rules </summary>
</details>

<details>
<summary>Lab introduction to Sky130 pdk's and steps to download labs</summary>

+ To download drc_tests
```
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/972f8c5c-9942-4bf4-b9d3-fb90dcc4ade5)

+ Move the compressed file to desktop using the following command.
```
mv drc_tests.tgz Desktop/
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f42bf743-dbb3-4c15-a6aa-e51af5a31251)

+ Go to desktop and enter the following command to extract.
```
tar xfz drc_tests.tgz 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f92f60f9-f103-4cc6-a7a2-1d44e5c990fc)

+ Go inside drc_tests and check the files in it
```
cd drc_tests/
ls
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/2b9b3526-a06e-4984-b448-1b22fcc58cad)

</details>

<details>
<summary>Lab introduction to Magic and steps to load Sky130 tech-rules </summary>

+ To open the layout in the downloaded software
```
magic -d XR
```
+ Then choose met3.mag from the file menu->open.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/18096fd4-d6aa-403f-a15a-bffa0d10b8b5)

</details>

<details>
<summary>Lab exercise to fix poly.9 error in Sky130 tech-file</summary>
</details>

<details>
<summary>Lab exercise to implement poly resistor spacing to diff and tap </summary>
</details>

<details>
<summary>Lab challenge exercise to describe DRC error as geometrical construct</summary>
</details>

<details>
<summary>Lab challenge to find missing or incorrect rules and fix them</summary>
</details>

</blockquote>
</details>


<details>
<summary>General timing characterization parameters</summary><blockquote>

<details>
<summary>Timing threshold definitions</summary>
</details>

<details>
<summary>Propagation delay and transition time</summary>






![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b86fa8ce-5cda-4b2c-98d7-d0233fbcbe91)

  
</details>

</blockquote>
</details>

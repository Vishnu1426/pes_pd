# ADVANCED PHYSICAL DESIGN USING OPENLANESKY130

## Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK

<details>
<summary>How to talk to computers?</summary><blockquote>

<details>
<summary>Introduction to QFN-48 Package, chip, pads, core, die and IP</summary>

+ Arduino Microcontroller

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7f07c337-4492-43f9-8488-a6c142c23e5f)

+ The main chip that controls the entire board is:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/86d283de-4595-4c85-9f04-7bbe538633cb)

+ Since Arduino is open source, there are many different chips which can be used and varies from board to board.
+ Around the chip there are many interfaces which are connected to the chip.
+ A typical block diagram view of the board is:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/94b38a3f-3df8-4832-9050-901015ff2abf)

+ SDRAM would be an external chip.
+ A labelled diagram of pins in the IC is as follows:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/42fdc799-e438-413e-a3ab-12c97b56f709)

+ The main chip would be connected to the package pins by things known as wirebounds.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6b74ecc0-6fcd-4ca3-b103-d195f5c91e4a)

+ Let us open up the chip

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4a1ff79b-b5d3-4565-b784-60ea35a559e9)

+ The blue parts are called PADS. These are things which allow the signal to flow from outside to the internals of the IC and vice versa.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ac68fa59-dd4d-48f0-89c1-65782463b2fe)

+ The CORE is basically the part of the IC which contains all the logic cells and their connections.
+ The CORE PADS, pins etc. all together is called a die. The die is the entire piece which contains elements of the IC

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/736d7114-6053-4d3b-9052-aef620a615dd)

+ This is what a sample RISC-V SoC along with the required components in an IC looks like in a higher level of abstraction.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4a704eed-8ffd-4d4a-8fb9-e83d16488088)

+ The PLLs, ADC, DAC and SRAM and other similar components are called Foundry IPs.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fa84d31c-094d-407f-bf01-5518b8fba5ba)

+ All the manufacturing of ICs are done in a Foundry.
+ Next are macros - these are blocks of pure digital logic.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9f6aa99f-df2c-4f5a-85b4-c19b2e11441b)
</details>

<details>
<summary>Introduction to RISC-V</summary>

+ An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software.
+ The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.
+ RISC-V[b] (pronounced "risk-five") is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles.
+ Unlike most other ISA designs, RISC-V is provided under royalty-free open-source licenses.
+ A number of companies are offering or have announced RISC-V hardware; open source operating systems with RISC-V support are available, and the instruction set is supported in several popular software toolchains.
+ A sample C program compiled to RISC-V assembly language program.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/59b92c50-a382-4404-8832-a4138966542d)

+ This assembly program is then converted to machine language program which is basically 1s and 0s.

+ Some RISCV Assemmbly Instructions are
1. lui: Load Upper Immediate 

![LUI](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/28ee7cf1-99fd-4fb8-979e-5ddb95b0f8f4)

2. addi: Add immediate

![addi](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5ff94dea-4d32-4943-b0ea-441e9196d299)

+ These 1s and 0s are then converted to electrical signals which are high and low voltages. This is the language that hardware understands.
+ The assembly logic is converted to a layout which is the hardware that performs the programmed logic. This is called Layout.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a0b8b6ab-6769-498d-b77a-0a8dd8d694c2)

+ There needs to be an interface between every language.
+ The interface which is in between the assembly language and layout is called the Hardware Description Language.
+ An example hardware which can implement the assembly logic would be a picorv32 core. This picorv32 core is defined using an HDL program.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/39235fe8-d41f-4781-a82f-9ccce564a8ef)

+ The final working of a C program would basically look like:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fd9ac20d-4d01-40a0-b2c1-10ba6ea183f8)
</details>

<details>
<summary>From Software Applications to Hardware</summary>

+ Applications that we use everyday run on hardware.
+ How does this work? ISA explains this to a certain level. But let's go into it deeper.
+ The application software is the computer program of an application or app.
+ The application software enters into a block called system software.
+ System software consists of OS, Compiler and Asspembler in a braod sense.
+ The system software block converts the application software program to hardware language and helps it run.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ac4e22d6-03d5-4042-ac26-1767272e36e6)

+ Let us look at the parts of the system software:
1. Operating System - It handles IO operations, allocates memory, and generates low level system functions. The output of the OS is basically functions in C/C++/Java/VB and that is sent to the compiler. 
2. Compiler - It takes the incoming C/C++/Java/VB program from the OS and generates a .exe file in windows which is an executable file. This file contains all the instructions in the assembly language of the hardware on which the program is going to be run.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/01165b27-22ea-40d8-99ee-59f21fee28be)
 
3. The assembler converts the assembly language to machine language which is basically 1s and 0s. This is then sent to the hardware.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9389a93f-ea6e-419b-a3de-0749907554bc)

4. Another intermediate interface between machine language and the hardware is RTL. It implements the machine language into a logic design of the hardware.
</details>

</blockquote>
</details>


<details>
<summary>SoC design and OpenLANE?</summary><blockquote>

<details>
<summary>Introduction to all components of open-source digital asic design</summary>

+ Digital ASIC design can be abstracted broadly as

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f663ac08-d0fd-41b4-94e3-cd4074666afb)

+ To do Open Source ASIC design, we need all open source EDA tools, RTl designs and PDK data.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/02166064-4b18-4a97-b530-c3f54df36572)

+ Open source EDA tools are Qflow, OpenROAD and OpenLANE
+ Open source RTL designs are librecores.org, opencores.org and github.com
+ In the early days the IC design was majorly controlled by those who knew physics well.
+ Then came the labda based design rules which separated the physics from the design step. Physics is indeed involved. However, we need not worry about it while designing.
+ PDK - Process Design Kits, are an in terface between Fab and designers.
+ PDk can be summarised as follows:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a80c50f7-87b4-41f7-aa49-b50e7f7ad544)

</details>

<details>
<summary>Simplified RTL2GDS flow</summary>

+ A simplified RTL to GDSII flow diagram with only the major steps would look like:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/89bf2bbb-956a-4077-b689-38c85bf28e65)

+ Synthesis - Converts RTL to a circuit out of components from a standard cell library (SCL). The result is called an HDL file called Gate Level Letlist.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/43669470-346c-4622-b507-dd92338f67cb)

+ Standard cells have regular layouts. Each cell comes with different views/models. Liberty view has electrical models, HDL and spice cells. We also have the GDSII view and the Lef view.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/bca2eac8-53f0-4167-96f8-6e2381e953f1)

+ Floor Planning - Planning the location and design of the area where cells are going to be placed. There are different types of Floor Planning.
  1. Chip Floor Planning -

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ea2fce4a-afe8-49ff-a271-c0bfbc84ffb9)

  2. Macro Floor Planning -

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7d79684c-4445-4e51-b308-f373fd471b8e)

+ Power planning - Planning the power distribution and efficiency of power consumption of the IC.
+ Power pads are connected to horizontal and vertical strips inside the IC. This is done to reduce resistance.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a4409a14-18bf-4cef-a9cb-a0e853d93d00)

+ Placement - Placing the cells on the planned floor. These cells are taken from the Gate Level Netlist generated out of the synthesis.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ea224cbf-0f2f-4fe6-a906-8ac7082a55f7)

+ Placement is usually done in two steps:
  1. Global Placement - Considering an entire chip, the cells are are arranged and placed in approximately right locations. At this stage cell overlap exists.
  
  ![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/55793a3f-a5c1-465a-9dc7-3cfd7382bfa4)

  2. Detailed Placement - The cells are considered in different areas in the chip and arranged and placed so that no overlap etc. occurs between cells.

  ![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/43cfff29-2a8f-47d6-b354-6dfd71114a49)
  
+ Clock Tree synthesis - All the parts of the chip, all the gates, registers etc should receive the same direct or derived clock signal without power loss or unintended delay since clock signal is what drives a circuit.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8ede5b21-a0eb-452f-8088-608e5b8b86e6)

+ Routing - Connecting all the cell interconnects using available metal layers.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ff6729b1-7f29-41ce-9cf0-82e704a3e87d)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/3da1ee21-1681-496f-95b9-371910d4d023)

+ Sign off - Signing off with last steps which involve checks amd verifications.
+ Physical Verifications
  1. Design Rule Check (DRC) - Checks if all the design constraints are met. For eg. lambda based rules.
  2. Layout vs Schematic (LVS) - Compares the output of the layout and the simulation output.
+ Timing Verifications
  1. Static Timing Analysis (STA) - Divides the entire circuit into timing paths and checks for delays.
</details>

<details>
<summary>Introduction to OpenLANE and Strive chipsets</summary>

+ When we are using opensource tools, the following things have to be taken care of:
  1. Tools Qualification - Whether the tools are qualified and are good enough to actually be useful.
  2. Tools Calibration - Whether the tools are calibrated to the right values.
  3. Missing Tools - If some tools or parts of them are missing, they have to be taken care of. 

+ OPENLANE

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/c4a1de8d-883f-4629-8c9c-ffa08171bc1b)

+ Started out as an  Open-Source Flow for a True Open Source Tape-out experiment.
+ striVe is a family of open everything SoCs - Open PDK, Open EDA and Open RTL

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d88537bc-5b43-4b23-a1ce-06575aaac173)

+ striVe family:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f96e1b29-18d7-47d5-ba4f-b52c04bcea86)

+ The main goal of openlane is to provide a clean GDSII with no human interventions.
+ Clean means
  1. No LVS vioaltions.
  2. No DRC vioaltions.
  3. No Timing vioaltions (still work in progress)

+ OpenLANE is tuned for skywater 130nm Open PDK. It also supports XFAB180 and GF130G.
+ It is containerized, meaning it is functional out of the box.
+ Can be used to harden (generate GDSII) Macros and Chips.
+ It has two modes of operation:
  1. Autonomous - We configure the flow, press a button, wait for sometime and everything will be ready.
  2. Interative - We can execute every command one by one.
+ Design Space Explorations - We can find the best set of flow configurations.
+ There are a large number of design examples also in OpenLANE.
</details>

<details>
<summary>Introduction to OpenLANE detailed ASIC design flow</summary>

+ The following diagram shows the OpenLANE ASIC flow

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ea78bfcf-9d8e-42b3-9702-1b6cddce604e)

+ OpenLANE is based on several open source projects such as:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/3a20d6c0-0aad-455f-b3d8-6b6338e08234)

+ Design RTL is sent to Yosys along with the constraints. It is mapped into standard cell library using abc.
+ Synthesis exploation allows us to select the best strategy based on how much delay and area is being consumed.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a72952b6-ab68-4c89-b107-ebc2f0cfc1e6)
 
+ Design exploration allows us to sweep design configurations and see the report.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/827bd958-759f-4777-95fd-215e014cacc9)

+ The design exploiration utility is also used for regression testing (CI). Compare the performance of different design configurations for different designs.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/c5374a96-4f71-4778-b7c8-4010bbff9231)

+ OpenLANE also has Design for Testability (DFT) and it involves the following steps:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a497f1f7-4b9f-4648-a06d-e0528de500e2)

+ Physical Immplementation is done using OpenROAD and involves the follling:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7ce7a4f3-0b43-48b7-808b-dfe61be5eaa6)

+ Everytime a netlist is modified, verification must be performed.
+ LEC (Logic Equivalence Check) - It is used to formally confirm that the function did not change after modifying the netlist. This is done by Yosys.
+ Dealing with Antenna Rule Violations:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7072eef9-0ff2-49e8-adac-a4d9bc065a61)

+ Solutions for antenna rule violatins:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d671c892-054e-4afe-a52a-6d5b77b8fb17)

+ OpenLANE takes a preventive approach for dealing with antenna rule violations

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/61e68cd8-3fd5-429d-9464-160d1b139e5d)

+ Static Timing Analysis is done by OpenROAD's OpenSTA after doing the RC extraction: DEF2SPEF
+ Physical verification (DRC and LVS):

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8b7ee1ec-31d7-4a65-930d-e97942536ee5)

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

M1 out in vdd vdd pmos W=0.375u L =0.25u
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
<summary>Switching Threshold Vm</summary>

+ Switching Threshold voltage, Vm, is the point where Vin = Vout, or are almost approximaetly equal.
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

+ We have to add the drc rules for poly in the tech file sky130A.tech
+ Add the allplynonres drc spacing rule as shown below:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/84b3c34f-3205-425a-b4d5-197af7323818)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/e468d769-2edd-41c4-ad9b-5e6fd6821c42)

+ After that, in the tkcon window type the following
```
tech load sky130A.tech
drc check
```
+ The drc rule will be applied and we will be able to see the changes.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/67032f4d-7078-4d20-b6bf-39c2a640b66a)

</details>

<details>
<summary>Lab exercise to implement poly resistor spacing to diff and tap </summary>

+ Next we need to change some more rules in the tech file so that all the drc are included.
```
change *nds to alldiff
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4369ae02-e70c-41eb-84ee-6376da222545)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d9670a4b-bb13-4a82-982b-3a20d9952446)

</details>

<details>
<summary>Lab challenge exercise to describe DRC error as geometrical construct</summary>

+ DRC rules check for leftover area using boolean operations on the layout cells.
+ We show in this that drc rules can be done as geometrical constructs.
+ Load nwell.mag
+ Let us see nwell.6
+ Type the following commands in the tkcon window.
```
cif ostyle drc
cif see dnwell_shrink
cif see nwell_missing
```
The following is displayed for nwell.6
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9d9ed902-d727-4af5-99b7-0573c51a562b)

</details>

<details>
<summary>Lab challenge to find missing or incorrect rules and fix them</summary>
	
+ We can see that the nwell.4 shows incorrect implementation, since all nwells must contain metal contacted taps and this one does not have that.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/3d1f4502-62e1-406c-a136-969c403f23eb)

+ We do the following changes in the tech file:
1. Add the following after "templayer nwell_missing" in "style drc"

```
templayer nwell_tapped nwell
bloat-all nsc nwell

templayer nwell_untapped
and-not nwell_tapped
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/ecb255a4-edc3-4e13-b3ba-26ba499371e7)

2. Add the following in "NWELL"
```
 variants (full)
 cifmaxwidth nwell_untapped 0 bend_illegal \
	"Nwell Missing Tap (nwell.4)"
 variants *
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/1dc0ba41-0303-4f4c-9aa3-f649ff6d3072)

3. Save the file
4. Do the following commands in the tkcon window

```
drc check
drc style drc(full)
drc check
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/d40fce15-3273-4dd8-b7b7-d635a63958e6)

+ nwell.4 still shows error

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/5d97fcc9-aad0-46fe-a12a-7deba4a30052)

+ To rectufy this we need to add a contact.
+ Select the nwell.4 and move your pointer to an empty area and press 'c'. This will copy paste the nwell.4
+ Now select a small area on the copied cell and hover over 'nsubstratecontact' on the right side. Now press 'p'
+ This will paint the selected area with the contact.
+ Run the drc check again and now we will not get any error.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/023473d8-4f2f-4ff2-8fd2-bed2b9a95e06)

</details>

</blockquote>
</details>

## Day 4 - Pre-layout timing analysis and importance of good clock tree

<details>
<summary>Timing modelling using delay tables</summary><blockquote>

<details>
<summary>Lab steps to convert grid info to track info</summary>

+ OpenLANE is a Place and Route tool.
+ For Place and Route we only need Input, Output, Power and Ground ports information. This is available in lef files.
+ So the next step would be extract a lef file out of the mag file.
+ It would be interesting to see if we can plug the lef file into the picorv32 core. This is what we will do.
+ Open the mag file in the vsdstdcelldsign directory.
```
magic -T sky130A.tech sky130_inv.mag 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/daf47620-2628-4012-9c8c-d3d116380b39)

+ There are some guidelines that we must follow:
  1. The input and the output must lie on the intersection of the vertical and horizontal tracks.
  2. The width of the standard cell should be an odd multiples of horizontal track pitch and height should be an odd multiple of horizontal track pitch.
 
+ Let us undestand what tracks are. Tracks are used during the routing stage. Routes go over the tracks.
+ Go to openlane_working_directory and type the following.
```
cd pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd
less tracks.info
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/655a802c-2762-41c9-b463-c0897272acad)

+ Let us use the grid commnad. Before that check what all the grid command needs.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/5b8af821-a6a8-401e-842b-0357dcc481aa)

+ Type in the values of the track from the track file into the grid command
```
grid 0.46um 0.34um 0.23um 0.17um
```
+ Now the grid definition gets converted to the size definition of the tracks.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7235d93a-4422-49b4-8fd2-c04cbf6d21ad)

+ Since the grids have the size of the tracks, we can see that the input and output lie on the intersection of the vertical and horizontal tracks.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/30288f82-11f3-4de6-b68f-6ed6256e2d2c)

</details>

<details>
<summary>Lab steps to convert magic layout to std cell LEF</summary>

+ The second guideline was that the width of the standard cell should be an odd multiples of horizontal track pitch and height should be an odd multiple of horizontal track pitch.
+ We can see that also has beem met.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/057d1eb2-c413-4cc8-bebe-6f98d655437c)

+ When we extract the lef file, the ports are the ones which are going to be pins. Labels hve to be coverted to ports (input or output).
+ If we want to define our ports, then select the cell and go to edit menu->Text. Fill it up in the following way and give whatever name and port number you want.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/2fdf621d-2ac8-4f93-8771-8afe08c4a682)

+ Let us save this as sky130_vsdinv.mag
```
save sky130_vsdinv.mag 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/bd006e94-3b56-46f2-9084-642afb67f91e)

+ We can see that the cell design has been saved.
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/312bb837-22d3-4855-a5e3-75af0c607ea1)

+ Open the newly created mag file
```
magic -T sky130A.tech sky130_vsdinv.mag &
```

+ To extract the lef file, type in the tkcon window.
```
lef write 
```
+ If we don't specify any name, the lef file will have the name of the mag file itself. We can see in the directory that the lef file has been created.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/458a751e-9a26-4cf5-8a99-e5ca6bc252b0)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/59fa9354-0131-43d1-bab1-120ecef7b6cb)

+ To open the lef file
```
less sky130_vsdinv.lef
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/1a15e326-7d64-46ef-83c4-d0592a4aaa93)

</details>

<details>
<summary>Introduction to timing libs and steps to include new cell in synthesis</summary>

+ Now it is time to plug in the lef file into picorv32 folder.
+ Let us put all our files into the src folder for ease.
+ Go to src folder. The files currently in src directory are:

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4125eba5-e03a-4da9-b97c-287abdb93c5f)

+ Copy the lef file into the src folder
```
cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
```
+ We have to include our custom cell into the openlane flow. First step is synthesis. So we need a library which has the cell definitions.
+ Go to libs folder and check out the typical library file
```
less 
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/5e6c6ad9-b634-4eb1-8c2d-4109b1448ea7)

+ Our cell is towards the end.
```
/vsdinv
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4f607915-72d9-43b6-bf65-5740aa705875)

+ Copy all the library files into src folder
```
cp sky130_fd_sc_hd__* /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/eeabf26b-6f95-4e74-9ba8-1aea31abbaf0)

+ Before moving ahead we need to modify our config.tcl in picorv32a folder
```
gedit config.tcl
```
+ Add the following lines into the config.tcl
```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"

set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"

set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"



set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/361f212b-2192-4922-8073-85667f72c2fb)

+ Now open docker and invoke openlane and set to overwrite the previous directory.
```
docker 
./flow.tcl -interactive
package require openlane 0.9 
prep -design picorv32a -tag 19-09_21-30 -overwrite
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6740123f-1a11-4762-9f33-776876ae0126)

+ Type in two more lines in the openlane so that it knows to take in the lef file.
```
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

+ Next let's do synthesis and see whether it is able to map the design to the standard cell library.
```
run_synthesis
```
+ Synthesis was successful

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6e0a032b-8232-46c7-8b77-c6db84a3dd32)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6a19a9b8-f259-4d3c-a9d2-5e10d222505a)

</details>

<details>
<summary>Lab steps to configure synthesis settings to fix slack and include vsdinv</summary>

+ As it can be seen there is a lot of slack. 

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/92fc58b9-d63e-4e07-8923-bc41f7611af8)

+ Let us try to rectify it. Update the environment variables as shown below.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/500c2ac3-49b7-423a-9818-649f5318b661)
```
run_synthesis
```

+ Next let us run floorplan and run pplacement
```
run_floorplan
run_placement
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/e626a3e5-bf94-41f3-a4a7-6c032a5c1394)

+ Next let us check the placed design in the results folder. Type this in the results folder created in run->date.
```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4c637ef9-14d9-4f4d-910b-aab083a930ec)

+ The sky130_vsdinv - _17251_

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/1c3a1729-18ae-41b8-884e-d1bea3f8479b)

+ Let's expand some random cells. Type this in the tkcon window after selecting one of the inverter instances.
```
expand
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/0891c5b6-2920-4069-8e37-82778a8b3723)

</details>

</blockquote>
</details>


<details>
<summary>Timing analysis with ideal clocks using openSTA</summary><blockquote>

<details>
<summary>Lab steps to configure OpenSTA for post-synth timing analysis</summary>

+ The STA configuration file has to have the following sources for performing the timing analysis. Let us create this .conf file in openlane directory and add the following lines in it.
```
set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um
read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib
read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib
read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/19-09_21-30/results/synthesis/picorv32a.synthesis.v
link_design picorv32a
read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/base.sdc
report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns
```
+ Next create my_base.sdc in src folder and add the following. The contents are taken from base.sdc in scripts folder. There are some changes however based on our specific file.
```
             set ::env(CLOCK_PORT) clk
             set ::env(CLOCK_PERIOD) 12.000
             set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
             set ::env(SYNTH_DRIVING_CELL_PIN) Y
             set ::env(SYNTH_CAP_LOAD) 17.65
             create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
             set IO_PCT  0.2
             set input_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
             set output_delay_value [expr $::env(CLOCK_PERIOD) * $IO_PCT]
             puts "\[INFO\]: Setting output delay to: $output_delay_value"
             puts "\[INFO\]: Setting input delay to: $input_delay_value"
             
             
            set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]
            #set rst_indx [lsearch [all_inputs] [get_port resetn]]
            set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]
            #set all_inputs_wo_clk_rst [lreplace $all_inputs_wo_clk $rst_indx $rst_indx]
            set all_inputs_wo_clk_rst $all_inputs_wo_clk
            
            
            # correct resetn
            set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
            #set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
            set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]
            
            # TODO set this as parameter
            set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
            set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
            puts "\[INFO\]: Setting load to: $cap_load"
            set_load  $cap_load [all_outputs]
```

+ After doing this let's run the sta in openlane directory.
```
sta pre_sta.conf
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/62e0a296-d41a-4282-9a39-bcb934ed93a6)

</details>

<details>
<summary>Lab steps to optimize synthesis to reduce setup violations </summary>

+ Right now hold time does not have any significance since we are uisng ideal clocks.
+ As we can see the slack is very high.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6dc890cb-9545-4fd3-86d8-c64df3b07728)

+ Delays are functions of input slew & output capacitance.
+ So we will try to reduce the input slew & output capacitance.
+ Reasons for high i/p slew is high fanout values
+ We can do the folllowing to reduce slack.
```
set ::env(SYNTH_MAX_FANOUT) 4
run_synthesis
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/2a8e294b-e9ba-431a-825e-5410729d098d)

+ We can also upsize buffers as required and remove slack to optimum value.
```
replace_cell _14481_ sky130_fd_sc_hd__or4_4
report_checks -fields {net cap slew input_pins} -digits 4
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/a1b76bd5-6a5d-4700-94a9-c691a62ad2bf)

+ This can be done for other cells as well and we can see slack is reduced.
</details>

<details>
<summary>Lab steps to do basic timing ECO </summary>

+ We can upsize other components and check the values.
```
replace_cell _14487_ sky130_fd_sc_hd__a221o_1
replace_cell _15169_ sky130_fd_sc_hd__or2_4
replace_cell _14462_ sky130_fd_sc_hd__a221o_4
```
+ In the end we still have slack but it has reduced.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9e379f65-c1d0-4e9c-a34b-eac0a71b11d7)

</details>
</blockquote>
</details>


<details>
<summary>Clock tree synthesis TritonCTS and signal integrity</summary><blockquote>

<details>
<summary>Lab steps to run CTS using TritonCTS</summary>

+ After a lot of changing we were able to reduce the slack. We can still reduce it with further changes.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/8710c541-b5a5-47b0-8a5a-6f825ca3c171)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b78d879f-046e-4cd6-a6ba-066a6cf6a3bd)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/bdf924d1-2269-411f-8d38-d05452714d64)

+ We have to use write verilog and make sure that openlane uses this new netlist.
```
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/19-09_21-30/results/synthesis/picorv32a.synthesis.v
```
+ Next we will run floorplan in openlane. This floorplan will now take the new netlist.
```
run_floorplan
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fb693ec1-0c17-46ef-a3a4-cf1d06353162)

+ Next we run placement
```
run_placement
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/796a2937-cfe0-433f-b40c-36d920583589)

+ Next is Clock Tree Synthesis
```
run_cts
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/f7dd17d5-e514-4aa0-bb62-c052f8696626)

</details>

<details>
<summary>Lab steps to verify CTS runs </summary>

+ There are procs in cts file. Procs are similar to functions. To check  that go to openlane directory->scripts->tcl_commmands
```
ls -ltr
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/cd9871ca-bfb1-4efb-8b59-25c53f999904)
```
less cts.tcl
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/113fdec8-c3c3-490e-9256-8e95cd1e7cd5)

+ This is the cts file that run_cts uses.
+ OpenRoad does not contain synthesis.tcl because Yosys does synthesis.
+ The or_cts.tcl under the openroad directory contains

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7bc84651-cd44-4c5b-9c42-735eee0a3005)
</details>

</blockquote>
</details>


<details>
<summary>Timing analysis with real clocks using openSTA</summary><blockquote>


<details>
<summary>Lab steps to analyze timing with real clocks using OpenSTA</summary>

+ Now that we have done the Clock Tree Synthesis, let's do timing analysis. Openroad also has an STA tool.
```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/19-09_21-30/tmp/merged.lef
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7aa31f21-0bd3-4aa2-8b8f-936617b0c7c7)

+ A def file will be created post cts
```
read_def /openLANE_flow/designs/picorv32a/runs/19-09_21-30/results/cts/picorv32a.cts.def
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/73a9263e-ece1-469d-ba68-6527b3e039e3)

+ Now we will write a db file. The nwe will read it.
```
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/19-09_21-30/results/synthesis/picorv32a.synthesis_cts.v
read_liberty -max $::env(LIB_SLOWEST)
read_liberty -min $::env(LIB_FASTEST)
```

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b9dd52fd-5bee-41b8-bb0c-30ccd5820351)

+ Next we read the sdc file and then check the reports of the slack of setup and route.
```
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/dcbaaa2f-9878-4ada-8342-4107a99e8313)
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b72c56f2-1f09-42ee-bc28-534fdf48a875)

</details>

<details>
<summary>Lab steps to execute OpenSTA with right timing libraries and CTS assignment</summary>

+ The previous analysis we did is not completely right.
+ This is because Triton CTS is built for typical library. But we used min and max library.
+ Exit from openroad and open it again and type in the following:
```
openroad
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/19-09_21-30/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -fields {slow trans net cap input_pin} -format full_clock_expanded -digits 4
```
+ The hold time there is no violation but setup time has violation since we had lot of slack in the netlist.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/851b540a-c35a-419e-87dc-501681e4a8c8)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6fe0b5f2-2032-4ae9-a55f-5d854abc9157)

</details>

<details>
<summary>Lab steps to observe impact of bigger CTS buffers on setup and hold timing</summary>

+ Having a bigger CTS will improve the setup and hold time constraints.
+ Now let's report the clock skews
```
report_clock_skew -hold
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/37fdfbbe-ec15-4a91-ab60-18808780b415)

```
report_clock_skew -setup
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/9b37ecdb-ae78-45f9-8e82-38400a77f7f5)

</details>

</blockquote>
</details>


## Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

<details>
<summary>Power Distribution Network and routing</summary><blockquote>

<details>
<summary>Lab steps to build power distribution network </summary>

+ To run and generate the power distribution network, all we have to do is type
```
gen_pdn
```
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/09f882bd-2ed0-4489-8f8e-3ab8006061a7)

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/32f1a6d0-265c-481d-9e90-5ca0b20505f7)

+ It would have created def file.
</details>

<details>
<summary>Lab steps from power straps to std cell power</summary>

+ This is how a power distribution network diagram looks like. The statistics provided shows all the parts in the diagram.

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/bfca20f6-f492-4365-a5d8-d7bd3b61eb51)

</details>

<details>
<summary>Basics of global and detail routing and configure TritonRoute </summary>

+ OpenLANE uses the TritonRoute tool for routing. There are 2 stages of routing:
1. Global routing: Routing region is divided into rectangle grids which are represented as course 3D routes (Fastroute tool)
2. Detailed routing: Finer grids and routing guides used to implement physical wiring (TritonRoute tool)

+ To run routing type
```
run_routing
```

</details>

</blockquote>
</details>

<details>
<summary>TritonRoute Features</summary><blockquote>

<details>
<summary>Routing topology algorithm and final files list post-route</summary>

+ This is the routing topology algorithm

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/6c2b7ef7-fc2d-44d7-abdc-bd454b6d6e16)

+ First optimisation
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/7459974e-297d-48a8-ab72-5639258b590b)

+ Second optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/73c84362-a80f-4837-a55d-3d861306f1b8)

+ Third optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b74aeae4-c42b-46cd-9bb6-85e59bb77baa)

+ Fourth optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/b8027f5b-f380-447e-b1a4-eb5795488009)

+ Fifth optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/90f643b9-696b-4c9d-a126-e127b2a0c701)

+ Sixth optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/4b7678cf-142a-4cf9-a8f4-c537bd7ca5cd)

+ Seventh optimisation

![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/c034402d-0152-44c6-87a7-48b9fe4fd73e)

+ 
![image](https://github.com/Vishnu1426/pes_pd/assets/79538653/fe9626ca-be49-4a00-b5ca-341b4b56d92f)

</details>

<blockquote>
</details>

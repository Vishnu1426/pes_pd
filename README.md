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
</details>

<details>
<summary>Concept of pre-placed cells</summary>
</details>

<details>
<summary>De-coupling capacitors</summary>
</details>

<details>
<summary>Power planning</summary>
</details>

<details>
<summary>Pin placement and logical cell placement blockage</summary>
</details>

<details>
<summary>Steps to run floorplan using OpenLANE</summary>
</details>

<details>
<summary>Review floorplan files and steps to view floorplan</summary>
</details>

<details>
<summary> Review floorplan layout in Magic</summary>
</details>

</blockquote>
</details>


<details>
<summary>Library Binding and Placement</summary><blockquote>

<details>
<summary>Netlist binding and initial place design</summary>
</details>

<details>
<summary>Optimize placement using estimated wire-length and capacitance </summary>
</details>

<details>
<summary>Final placement optimization</summary>
</details>

<details>
<summary>Need for libraries and characterization</summary>
</details>

<details>
<summary>Congestion aware placement using RePlAce</summary>
</details>

</blockquote>
</details>


<details>
<summary>Cell design and characterization flows</summary><blockquote>

<details>
<summary>Inputs for cell design flow</summary>
</details>

<details>
<summary>Circuit design step</summary>
</details>

<details>
<summary>Layout design step</summary>
</details>

<details>
<summary>Typical characterization flow</summary>
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
</details>

</blockquote>
</details>


## Day 3 - Design library cell using Magic Layout and ngspice characterization

<details>
<summary>Labs for CMOS inverter ngspice simulations</summary><blockquote>

<details>
<summary>IO placer revision</summary>
</details>

<details>
<summary>SPICE deck creation for CMOS inverter</summary>
</details>

<details>
<summary>SPICE simulation lab for CMOS inverter</summary>
</details>

<details>
<summary>Switching Threshold Vm</summary>
</details>

<details>
<summary>Static and dynamic simulation of CMOS inverter</summary>
</details>

<details>
<summary>Lab steps to git clone vsdstdcelldesign</summary>
</details>

</blockquote>
</details>


<details>
<summary>Inception of Layout Â CMOS fabrication process</summary><blockquote>

<details>
<summary>Create Active regions</summary>
</details>

<details>
<summary>Optimize placement using estimated wire-length and capacitance </summary>
</details>

<details>
<summary>Final placement optimization</summary>
</details>

<details>
<summary>Need for libraries and characterization</summary>
</details>

<details>
<summary>Congestion aware placement using RePlAce</summary>
</details>

</blockquote>
</details>


<details>
<summary>Cell design and characterization flows</summary><blockquote>

<details>
<summary>Inputs for cell design flow</summary>
</details>

<details>
<summary>Circuit design step</summary>
</details>

<details>
<summary>Layout design step</summary>
</details>

<details>
<summary>Typical characterization flow</summary>
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
</details>

</blockquote>
</details>

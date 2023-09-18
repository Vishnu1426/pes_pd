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
</details>

<details>
<summary>Review files after design prep and run synthesis</summary>
</details>

<details>
<summary>OpenLANE Project Git Link Description</summary>
</details>

<details>
<summary>Steps to characterize synthesis results</summary>
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

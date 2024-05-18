# NASSCOM-VSD SoC Design Program

<details>
<summary>A PREREQ</summary>
<br>
1.A package refers to the enclosure or casing that houses a semiconductor chip. It provides physical protection, electrical connections, and heat dissipation for the chip.<br>
  
2.An integrated circuit (IC), is a small piece of semiconductor material, typically made of silicon. It contains electronic components such as transistors, resistors, and capacitors that are interconnected to perform specific functions <br>

3.A die refers to a small block of semiconducting material on which a specific functional circuit is fabricated. It is usually cut from a larger silicon wafer during the manufacturing process <br>

4.IP can refer to various things. It can represent proprietary designs, algorithms, or architectures that are protected by intellectual property rights. Semiconductor companies often develop their IP, which can include specialized circuit designs, software algorithms, or system architectures that give them a competitive advantage in the market

</details>


<details>
<summary>OPENSOURCE EDA TOOLS</summary>
<br>
        
  # OPENLANE

[OpenLane](https://github.com/The-OpenROAD-Project/OpenLane) is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, KLayout and a number of custom scripts for design exploration and optimization. It also provides a number of custom scripts for design exploration and optimization.

The flow performs all ASIC implementation steps from RTL all the way down to GDSII. Currently, it supports both A and B variants of the sky130 PDK, the C variant of the gf180mcu PDK.

OpenLane abstracts the underlying open source utilities, and allows users to configure all their behavior with just a single configuration file.
There are Two modes of operation: automonomous and interactive

![1](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/2b255544-dfbc-484f-b0bf-6a8def7b211f)
### Synthesis

`yosys/abc` - Perform RTL synthesis and technology mapping.

`OpenSTA` - Performs static timing analysis on the resulting netlist to generate timing reports

### Floorplaning

`init_fp` - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)

`ioplacer` - Places the macro input and output ports

`pdngen` - Generates the power distribution network

`tapcell` - Inserts welltap and decap cells in the floorplan

### Placement

`RePLace` - Performs global placement

`Resizer` - Performs optional optimizations on the design

`OpenDP` - Performs detailed placement to legalize the globally placed components

### CTS

`TritonCTS` - Synthesizes the clock distribution network (the clock tree)

### Routing

`FastRoute` - Performs global routing to generate a guide file for the detailed router

`TritonRoute` - Performs detailed routing

`OpenRCX` - Performs SPEF extraction

### Tapeout

`Magic` - Streams out the final GDSII layout file from the routed def

`KLayout` - Streams out the final GDSII layout file from the routed def as a back-up

### Signoff

`Magic` - Performs DRC Checks & Antenna Checks

`KLayout` - Performs DRC Checks

`Netgen` - Performs LVS Checks

`CVC` - Performs Circuit Validity Check

<details>
<summary>OPENSOURCE EDA TOOLS</summary>
<br>

  ### FILE FORMATS

  ### INSTALLATION OF OPENLANE
    Installing Docker

    # Install Docker
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

    # Check for installation
    sudo docker run hello-world

  <br>

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    
    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub. (amd64)
    3. The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.

  <br>

    Now We will make docker available without root
    sudo groupadd docker
    sudo usermod -aG docker $USER
    sudo reboot # REBOOTS

  ### Installing OpenLane
    git clone https://github.com/The-OpenROAD-Project/OpenLane.git
    cd OpenLane/
    make
    make test
    #On make test if everything is installed properly you will get the below message
    Basic test passed
</details>

</details>

### SKY130 PDK
There are seven standard cell libraries provided directly by the SkyWater Technology foundry available for use on SKY130 designs, which differ in intended applications and come in three separate cell heights

```<Process name>_<Source>_<Type>_<Density>```	

here we hace used the sky130_fd_sc_hd.lib

Sky130 : process technology (node)
fd : SkyWater Foundry
sc : Digital Standard Cells
hd : High density

### USING OPENLANE


    Move to the directory where Openlane is Installed
    cd Desktop/work/tools/openlane_working_dir/openlane
    
    Start the Docker container and enter the OpenLANE shell:
    
    docker
    ./flow.tcl -interactive

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/27dc9631-ec33-42d5-8126-f1cae063d21d)

### flow.tcl

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/665a4343-c183-4efd-98f6-0ace33887b7e)

**Initialize the environment**

    package require openlane 0.9

### The picorv32a Directory
    prep -design picorv32a
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/e600df33-05c7-4326-acbe-2cd11e2558a6)
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/f5bcd8a7-b400-4b48-8461-978f60726b3e)

Now we can see that there is a directory created(check timestamp) under which we could navigate to the runs directory where we can find the ```merged.lef``` 

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/9f4a59d8-3558-45fc-a0f5-4f6c62475c00)

Inside the ```merged.lef```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/cb8a1527-e82d-4987-9dfd-a015fb929fa4)
We can seee the specs about the vias metal layer cuts and the dimensions


### Synthesis

      run_synthesis

  ![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/4082a566-185e-454a-9c24-2c2ab0c8d92e)

  After Running the synthesis command we can see the update inside the design directory of openlane where we have the picorv32a (check the modified date)
  ```/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_11/results/synthesis```

  ![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/2937f4e2-f619-414c-a11d-ee30f1eb8ace)

  **Below is the synthesis netlist inside the synthesis directory**
  ![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/ae047862-f160-4fc8-879f-5f22de3bdf69)

  **can see the Std cell mapping in the netlist file**
  ![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/92318ca6-6561-41b4-be58-4d2ff5195357)

  **Inside the yosys reports**

  ```
Printing statistics.

=== picorv32a ===

   Number of wires:              14596
   Number of wire bits:          14978
   Number of public wires:        1565
   Number of public wire bits:    1947
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   ##### Number of cells:              14876 #####
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       35
     sky130_fd_sc_hd__a211oi_2      60
     sky130_fd_sc_hd__a21bo_2      149
     sky130_fd_sc_hd__a21boi_2       8
     sky130_fd_sc_hd__a21o_2        57
     sky130_fd_sc_hd__a21oi_2      244
     sky130_fd_sc_hd__a221o_2       86
     sky130_fd_sc_hd__a22o_2      1013
     sky130_fd_sc_hd__a2bb2o_2    1748
     sky130_fd_sc_hd__a2bb2oi_2     81
     sky130_fd_sc_hd__a311o_2        2
     sky130_fd_sc_hd__a31o_2        49
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2        46
     sky130_fd_sc_hd__a41o_2         1
     sky130_fd_sc_hd__and2_2       157
     sky130_fd_sc_hd__and3_2        58
     sky130_fd_sc_hd__and4_2       345
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       1656
     sky130_fd_sc_hd__buf_2          8
     sky130_fd_sc_hd__conb_1        42
    ##### sky130_fd_sc_hd__dfxtp_2     1613  #####
     sky130_fd_sc_hd__inv_2       1615
     sky130_fd_sc_hd__mux2_1      1224
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux4_1       221
     sky130_fd_sc_hd__nand2_2       78
     sky130_fd_sc_hd__nor2_2       524
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        42
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_2       2
     sky130_fd_sc_hd__o211a_2       69
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2        54
     sky130_fd_sc_hd__o21ai_2      141
     sky130_fd_sc_hd__o21ba_2      209
     sky130_fd_sc_hd__o21bai_2       1
     sky130_fd_sc_hd__o221a_2      204
     sky130_fd_sc_hd__o221ai_2       7
     sky130_fd_sc_hd__o22a_2      1312
     sky130_fd_sc_hd__o22ai_2       59
     sky130_fd_sc_hd__o2bb2a_2     119
     sky130_fd_sc_hd__o2bb2ai_2     92
     sky130_fd_sc_hd__o311a_2        8
     sky130_fd_sc_hd__o31a_2        19
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32a_2       109
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2       1088
     sky130_fd_sc_hd__or2b_2        25
     sky130_fd_sc_hd__or3_2         68
     sky130_fd_sc_hd__or3b_2         5
     sky130_fd_sc_hd__or4_2         93
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__or4bb_2        2

   Chip area for module '\picorv32a': 147712.918400
  ```
**Inside The OpenSTA reports**

```bash
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-05_11-17/reports/synthesis$ less 2-opensta.rpt
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/4e75101a-1ac0-47b4-8c16-03f6c3a75b09)


 ### Synthesis Results

 
```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}  = \frac{1613}{14876} = 0.1084
```
```math
DFF's\ percent  = Flop\ Ratio * 100 = 0.1084* 100 = 10.84\ \%
```

### Floorplanning with OpenLane

**What's inside the README.md of Config files?**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/1351c213-2339-44c5-9517-25e89946a4cf)

This gives a documentation the various settings are user can use by help of the switches we we can set in the ```~/Desktop/work/tools/openlane_working_dir/openlane/configuration/floorplan.tcl```

**Inside the floorplan.tcl**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/f11a1c5c-1c2b-4469-b910-5d0e3aa86425)

 (FP_IO MODE) 0 - matching mode
 (FP_IO MODE) 1 - equidistance positioning

In the openlane interactive mode
```run_floorplan```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/ba478d2b-8b7c-45f3-932f-40463c6604e4)

**floorplan.def was updated as shown in the below image**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/070a0874-3160-4ddd-92a6-6aafb2cbdbb1)

### REVIEWING THE FLOORPLAN REPORTS

```bash
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/results/floorplan
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/3614d7b3-1990-4499-8dc4-0235bc0d2565)

**picorv32a.floorplan.def.png**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8a90ea4b-a979-438c-a0cc-687fc532264e)

**Inside the picorv32a.floorplan.def**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/6aecb454-1068-4f9b-a269-e148bd43b707)

**OBSERVATIONS FROM THE FLOORPLAN RESULTS**

```math
Given\ 1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width = 660685 \ in \ unit \  distance
```
```math
Die\ height = 671405 \ in \ unit \  distance
```

```math
Die\ width = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die = 660.685 * 671.405 = 443587.212425\ Sq\ Microns
```

### Layout in Magic

**INSIDE THE config.tcl**
```
~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/config.tcl
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/fff62f85-74ac-45ef-ab57-602a59e0e0a3)


We need a lef and def file along with pdk's techfile into order to map accordingly and view the floorplan in the Magic
```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```


![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/246d4bde-bb5a-4147-886c-7182fc04f5a2)


**Decap cells**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/945c3d1a-2fe6-4847-9b64-6d97b76d23fb)

**An overview of decap cells tap cells** 
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/c64121fc-3ae2-4133-b8be-845688c346f9)

```
Click on any cell and select it, Then press "S" which will open a tkcon window and type "what" to get a brief note on the selected cell" 
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/eb46600d-e896-450d-b849-c87d75de041c)


**Standard cells placed at the bottom of the layout**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/1ec2757a-dbe7-4da3-9268-e750afdbd444)
___________________________________

### PLACEMENT

```run_placement```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/da446621-1138-411b-8f50-725936b2b3e6)


![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/1fbd4478-c13c-4ecb-b90f-91a73670a9ce)



**PLACEMENT RESULTS**

```home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/results/placement/picorv32a.placement.def.png```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/fa1278d2-0e85-4e23-a439-75d48a48f8e7)

```~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/logs/placement/8-resizer.log```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/f2b27172-4969-4079-9a9c-5fb5ad1bdb0b)


```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/cb1dcb36-6d40-4464-9546-594a1fb438a3)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/eecd8a25-75ad-412f-b12b-a6ee58ae2717)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/9e68d2ac-065a-46a0-88c7-9e851a6b355a)


### TRYING DIFFERENT SWITCHES

**WITH THE DEFAULT CONFIGURATION**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/39c58e23-252b-4b8c-b71d-e741a50e21de)

In the openlane interactive window 
```bash
set ::env(FP_IO_MODE) 2
```

inside the `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-05_05-22/results/floorplan`

```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/f140f4f0-36b2-48c2-973c-7243c6377842)

We can See that the pins aren't like before it was and completely rearranged now and not in equidistant.
___________________________________________________

### LIBRARY CELL DESIGN USING MAGIC AND NGSPICE

```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
In the working directory clone the above github repo

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/dae41510-7fd9-4839-a3e8-8f6e8591802c)

To view the CMOS Inverter layout
```bash
magic -T sky130A.tech sky130_inv.mag &
```

Below are the brief view on the various diffusion and metal layer of the cmos inverter.The area of interest is highlighted with a thin white bounding box and to know about the details "What" command is used in tkcon.
As a CMOS Inverter is Intended to be, The source of NMOS,PMOS are connected to the power rails and the drains are connected together from which the output is taken from a contact.

**POLY LAYER**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/cb3413be-f8ef-4e7d-bcae-afd08b93530f)

**NMOS**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/d05a6e39-db66-4db6-8a01-fc9ee5f741b3)

**PMOS**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/4a428f8f-8d94-4f3c-8bea-305d3333866c)

**input(A) poly contact**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/6661f92d-e5ba-48b8-9776-ee3196c6af84)

**N-Diffusion**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/21396b55-06dc-44ce-b287-a5ed7215f1a1)

**P-diffusion**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/a948415d-3d40-4ff4-98f4-4b58c57af836)

### EXTRACTING THE SPICE NETLIST

`Inside tkcon bash, while in the clone directory with .tech and .mag file `
```bash
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8dd21810-3522-44e6-a1df-a4108977aedf)


inside the `sky130_inv.ext` **WE CAN WITNESS THE EXTRACTED NETLIST INFORMATION**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/897af63b-e29d-45e6-8c54-c32d8e05af57)


**MODIFIED EXTRACTED SPICE NETLIST**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/3ad94559-13c3-469a-85d2-467390fd09db)

`The include files were present in the working directory`


**SPICE SIMULATION RESULTS**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/9536df2b-fae7-4b37-99ab-7b898cd6bdf7)


**RISE TIME**
```math
x0 = 2.16151e-09, y0 = 0.659639 \         \   

x0 = 2.20386e-09, y0 = 2.63012
```
Rise time transition 20% to 80% - time value = 43ps

**FALL TIME**

```math
x0 = 4.04043e-09, y0 = 2.64059 \  \
x0 = 4.06827e-09, y0 = 0.662766
```
Fall time transition 20% to 80% - time value = 28ps

**CELL RISE DELAY**
Calculated at 50% of VDD = 35ps
```math
x0 = 2.15e-09, y0 = 1.65189 \  \

x0 = 2.185e-09, y0 = 1.65094
```

**CELL FALL DELAY**
Calculated at 50% of VDD = 20ps
```math
x0 = 4.06051e-09, y0 = 1.65147 \  \

x0 = 4.05492e-09, y0 = 1.65
```

### DRC ERRORS AND TECH FILE - AN OVERVIEW

```bash
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
gvim .magicrc
magic -d XR &
```
`magicrc`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/324d75d3-1132-4938-a85d-f38d6f53df33)

`launching magic`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/662a4e3c-a2d5-4ca6-8a00-ab5c8e2969d2)




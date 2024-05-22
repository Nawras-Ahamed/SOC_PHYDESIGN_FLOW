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
```tcl
run_floorplan
```
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
```tcl
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
```tcl
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

[Sky130 Periphery Rules](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

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

`open met3.mag`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/92f4328b-5082-465e-b346-f2257d0a5d7a)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/1ec9e6ae-6be0-42f8-85cc-a15b213fc596)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/be599bed-f892-4861-bb99-136e61d59320)


__________________________________________________

### Fixing poly.9 error in Sky130 tech-file

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/2513ca14-4538-47b5-8eaa-f05666a8d15d)

```bash
gvim sky130A.tech
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/39074ad8-c222-49f4-9fa0-52d33800dd6b)

`change to allpolynonres`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/c0546763-1e77-490b-b9d9-143048a9b679)


![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/1f05582f-4ad1-401d-a1ec-6e4f20853a07)


### implement poly resistor spacing to diffusion and tap

```
add this line---------------------
spacing xhrpoly,uhrpoly,xpc allpolynonres 480 touching illegal \
    "xhrpoly/uhrpoly resistor spacing to diffusion < %d (poly.9)"
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/14b752d0-cdee-4d03-b9cc-f119baae7ef9)

<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/48469e08-0da6-4cc0-a880-ad6b68735bbb)

<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/b6c0403f-8b55-4b2f-b7e1-eb9415acbf1e)



### Describing DRC error as Geometrical Construct

`open > nwell.mag`
<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/5aa1d43a-53fe-407c-9164-0a9a487871fd)


``` tcl
cif ostyle drc
cif see dnwell_shrink
feed clear
cif see nwell_missing
feed clear
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/842d07b2-ebf9-4ed6-8577-e20a8033c472)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/5d1742fc-7597-4b2d-8a29-15725c9946f7)

### Finding missing or incorrect Rules

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/d1c276f4-1246-43cb-acf7-ae3534f1634a)

```
 variants (full)
  cifmaxwidth nwell_untapped 0 bend_illegal \
  "Nwell missing tap (nwell.4)"

 variants *
 ```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/14ee1893-9b36-4c3f-8e78-6f8ccffc23f9)


```
 templayer nwell_tapped
 bloat-all nsc nwell

 templayer nwell_untapped nwell
 and-not nwell_tapped

```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/430b9847-13c3-4968-95ff-1efb22f17ae4)

`now we can see the mistake in the implementation from the drc checker`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/e32bb292-f9f5-49ac-acd1-f66e812f25db)

___________________________________________

### PRE LAYOUT TIMING ANALYSIS

We need to extract the track information first and set the grid view of the layout according to the track pitch x and y values 

As a rule, the output port and input port of the cell has to be placed in such a position that it is in the intersection of both the x and y axis of the tracks

`grid x-spacing y-spacing x-orgin y-origin` the local interconnect information can be found from 

`/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd`

**Width of the standard cell should be odd multiples of the horizontal track pitch**
**Height of the standard cell should be even multiples of the vertical track pitch**

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/9fce6aca-ed2e-4059-b9cd-fa618ca7e788)

*To set the grid size*
```tcl
grid 0.46um 0.34um 0.23um 0.17um
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/a35121e8-a22b-4f05-8495-4b0c8d2ddc8f)

`after settign the grid size based on the track pitch`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/534cb4cb-ac2a-48d0-a9f5-a6847a251886)

**importing with custom lef**
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/4a091c85-7fbb-40c5-8cef-f7cbe9741df0)


### Adding my custom inverter cell
<br>

 `BEFORE MAKING ANY CHANGES`
<br>
`run_synthesis`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/fe1632d2-5982-40fc-87b1-eba67c6a2c2f)

<br>

`run_floorplan + run_synthesis`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/91ca7c54-cfc8-4ac6-9d97-bfea9c0acaf8)


`Copy the necessary files to the source directory`1

```bash
cp sky130_nawras_inv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/876554ef-8049-4a47-8584-c5844ccd9907)

<br>

`add the below lines to the config.tcl in the picorv32a directory`

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/57b5b5be-7365-4fe8-9d3f-e181d18ff41a)

`invoke openlane and start with the latest run`
<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/7d7d99d9-c665-4d55-81f2-64201efbb631)

`set the design directory from the interactive window itself and synthesis`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/a56de26f-37c3-4518-92ab-01cfca7044f5)

`CHIP AREA`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8563356d-1d39-4703-a721-b26bc773018f)

`Timing Report`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/e448b8cb-a2b9-41e9-b0d0-ab9379b5b21d)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/74d5a825-b0b1-47e9-90c0-281feeb0d705)

`Modifications inorder to reduce the slack violations`

```tcl
prep -design picorv32a -tag 16-05_24-24 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
echo $::env(SYNTH_STRATEGY) # display current value of variable SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3" #  set new value for SYNTH_STRATEGY
echo $::env(SYNTH_BUFFERING)#  display current value of variable SYNTH_BUFFERING
echo $::env(SYNTH_SIZING) # display current value of variable SYNTH_SIZING
set ::env(SYNTH_SIZING) 1 # set new value for SYNTH_SIZING
echo $::env(SYNTH_DRIVING_CELL) # display current value of SYNTH_DRIVING_CELL 
run_synthesis
```
`can see the custom vsd inverter cell`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/41575e88-85aa-40ce-976e-ba628361dce0)

`run_floorplan`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8a6ce9d5-b1c9-4846-b1be-7e473c59750f)

`run_placement`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/63e09cf8-a780-4503-b7f0-864d14debe03)
____________________________________________________________________________
### ISSUES I FACED
Due to failed flow i had to manually
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/f7188808-8e7c-4cbf-8207-1b48fb3bc91e)

```bash
init_floorplan
place_io
tap_decap_or
run_placement
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/634f8001-b9d3-40ae-bbb2-d0c789131c74)


![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/27916472-4920-4546-b183-9f33fe6c4ce1)

<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/80993a93-b03a-4b70-a348-e2efe48c418b)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/36febaea-b782-4222-b165-6c9fff27f6eb)
________________________________________________________________________________________________________________


```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/19-05_10-06/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
`picorv32a/runs/19-05_10-06/results/placement/picorv32a.placement.def.png`

`tmp/merged.lef`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/831440f7-4cfb-48d7-8355-77bfaedbfd6e)

<br>

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8ed78fa3-0750-4484-9aff-23a69a75149e)
<br>
________________________________________________

### AFTER SOME DEBUGGING

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/41f366d8-0ef0-41b3-9e61-9ebbb61b323a)


### STATIC TIMING ANALYSIS using OpenSTA

*POST SYNTHESIS TIMING ANALYSIS*

`inside the openlane/pre_sta.conf`

```
set_cmd_units -time ns -capacitance pF -current mA -voltage V -resistance kOhm -distance um

read_liberty -max /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib

read_liberty -min /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib

read_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/19-05_12-54/results/synthesis/picorv32a.synthesis.v

link_design picorv32a

read_sdc /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/my_base.sdc

report_checks -path_delay min_max -fields {slew trans net cap input_pin}
report_tns
report_wns
```

`openalne/designs/src/my_base.sdc`

```
set ::env(CLOCK_PORT) clk
set ::env(CLOCK_PERIOD) 24.73
#set ::env(SYNTH_DRIVING_CELL) sky130_vsdinv
set ::env(SYNTH_DRIVING_CELL) sky130_fd_sc_hd__inv_8
set ::env(SYNTH_DRIVING_CELL_PIN) Y
set ::env(SYNTH_CAP_LOAD) 17.653
set ::env(IO_PCT) 0.2
set ::env(SYNTH_MAX_FANOUT) 6

create_clock [get_ports $::env(CLOCK_PORT)]  -name $::env(CLOCK_PORT)  -period $::env(CLOCK_PERIOD)
set input_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]
set output_delay_value [expr $::env(CLOCK_PERIOD) * $::env(IO_PCT)]

puts "\[INFO\]: Setting output delay to: $output_delay_value"
puts "\[INFO\]: Setting input delay to: $input_delay_value"

set_max_fanout $::env(SYNTH_MAX_FANOUT) [current_design]

set clk_indx [lsearch [all_inputs] [get_port $::env(CLOCK_PORT)]]

#set rst_indx [lsearch [all_inputs] [get_port resetn]]

set all_inputs_wo_clk [lreplace [all_inputs] $clk_indx $clk_indx]

#set all_inputs_wo_clk_rst [lreplace $all_inputs_wo_clk $rst_indx $rst_indx]

set all_inputs_wo_clk_rst $all_inputs_wo_clk

set_input_delay $input_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] $all_inputs_wo_clk_rst
#set_input_delay 0.0 -clock [get_clocks $::env(CLOCK_PORT)] {resetn}
set_output_delay $output_delay_value  -clock [get_clocks $::env(CLOCK_PORT)] [all_outputs]

set_driving_cell -lib_cell $::env(SYNTH_DRIVING_CELL) -pin $::env(SYNTH_DRIVING_CELL_PIN) [all_inputs]
set cap_load [expr $::env(SYNTH_CAP_LOAD) / 1000.0]
puts "\[INFO\]: Setting load to: $cap_load"
set_load  $cap_load [all_outputs]

```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/2219f5d8-909c-46a6-be41-46de4ca672f1)

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/361cf8f7-2e4f-4df2-b5fa-201a968d5d49)
`Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again`

```bash

prep -design picorv32a -tag 19-05_12-54 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_SIZING) 1

set ::env(SYNTH_MAX_FANOUT) 4

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis
```

`Lesser drive Strength OR2 Gate has a Fanout 4`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8c1ab9d1-2d9e-4e2f-9e45-d24659a0a2a3)

### Commands to perform analysis and optimize timing by replacing the OR Gate

```bash
report_net -connections  _10911_
replace _13691_ sky130_fd_sc_hd__or3_4
report_checks -fields {net cap slew input_pins} -digits 4
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/20507f2a-50cb-45da-8808-d5275cdbfd8b)
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/2e923184-37bd-4b37-a3f7-b4197dc2c72e)

```bash
report_net -connections  _10566_
replace _13165_ sky130_fd_sc_hd__or3_4
report_checks -fields {net cap slew input_pins} -digits 4
```


![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/b017bb79-22e2-4fc4-877b-1c72d73ca204)

`OR4 gate of drive strength 2 driving OA gate has delay`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/24ce7882-3b37-4cf0-a716-a629f64a765a)

```bash
% report_net -connections _10534_
Net _10534_
Driver pins
 _13132_/X output (sky130_fd_sc_hd__or4_2)

Load pins
 _13160_/A1 input (sky130_fd_sc_hd__o2111a_2)

% replace_cell _13132_ sky130_fd_sc_hd__or4_4        
1
% report_checks -fields {net cap slew input_pins} -digits 4
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/3719a0de-ac5f-4e67-87af-8ebc28fb31f5)

`replacing with OR gate of drive strength 4`

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/fd8818b9-85e0-4361-b63c-c3203b2e6631)

```bash
% report_net -connections _10566_
Net _10566_
Driver pins
 _13165_/X output (sky130_fd_sc_hd__or3_4)

Load pins
 _13166_/A input (sky130_vsdinv)
 _13167_/B2 input (sky130_fd_sc_hd__o221a_2)
 _13287_/B input (sky130_fd_sc_hd__or2_2)
 _13690_/B input (sky130_fd_sc_hd__or2_2)

% replace_cell _13690_ sky130_fd_sc_hd__or2_4
1
% report_checks -fields {net cap slew input_pins} -digits 4

```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/8902fec0-1a5d-498e-ada7-99b3e356849f)

After ECO we have reduced -23.89 to -22.9259 = 0.9641ns reduced
________________________________

### Replace the old netlist with the new netlist generated after timing ECO

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-05_16-17/results/synthesis/
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
```

```tcl
help write_verilog
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/22-05_16-17/results/synthesis/picorv32a.synthesis.v
exit
```
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/aa728a3a-962b-4fad-9655-4f3f098a38e2)

_____________________________

### PERFORMING FP, PLACEMENT, CTS on the Updated Netlist

```bash
prep -design picorv32a -tag 24-03_10-03 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_STRATEGY) "DELAY 3"

set ::env(SYNTH_SIZING) 1

run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

run_cts
```

![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/e3c2977c-8683-4dcf-a220-71e2ffaea8a9)

`CHECKS`
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/eb91f5ca-4052-47ae-8e5c-54998133b5e8)


_____________________________


### POST-CTS Timing Analysis

Performing timing analysis with the integrated OpenSTA with OpenRoad

```bash
openroad

read_lef /openLANE_flow/designs/picorv32a/runs/22-05_16-17/tmp/merged.lef

read_def /openLANE_flow/designs/picorv32a/runs/22-05_16-17/results/cts/picorv32a.cts.def

write_db pico_cts.db

read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/22-05_16-17/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
help report_checks


report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit
```












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

```<Process name> _ <Library Source Abbreviation> _ <Library Type Abbreviation> <Library Name>```	

sky130_fd_sc_hd.lib:

Sky130 : process technology.
fd : SkyWater Foundry.
sc : Digital Standard Cells.
hd : High density.

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


 ### Synthesis Results

 
```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}  = \frac{1613}{14876} = 0.1084
```
```math
DFF's\ percent  = Flop\ Ratio * 100 = 0.1084* 100 = 10.84\ \%
```

 


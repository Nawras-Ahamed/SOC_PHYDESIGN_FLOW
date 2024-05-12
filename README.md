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

yosys/abc - Perform RTL synthesis and technology mapping.

OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports

### Floorplaning

init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)

ioplacer - Places the macro input and output ports

pdngen - Generates the power distribution network

tapcell - Inserts welltap and decap cells in the floorplan

### Placement

RePLace - Performs global placement

Resizer - Performs optional optimizations on the design

OpenDP - Performs detailed placement to legalize the globally placed components

### CTS

TritonCTS - Synthesizes the clock distribution network (the clock tree)

### Routing

FastRoute - Performs global routing to generate a guide file for the detailed router

TritonRoute - Performs detailed routing

OpenRCX - Performs SPEF extraction

### Tapeout

Magic - Streams out the final GDSII layout file from the routed def

KLayout - Streams out the final GDSII layout file from the routed def as a back-up

# Signoff

Magic - Performs DRC Checks & Antenna Checks

KLayout - Performs DRC Checks

Netgen - Performs LVS Checks

CVC - Performs Circuit Validity Check

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

Now we can see that there is a directory created(check timestamp) under which we could navigate to the runs directory where we can find the ```merged_lef.py``` 
![image](https://github.com/Nawras-Ahamed/SOC_PHYDESIGN_FLOW/assets/50738659/9f4a59d8-3558-45fc-a0f5-4f6c62475c00)



    
    

    



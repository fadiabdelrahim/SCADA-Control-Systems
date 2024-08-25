# <p align="center">SCADA Control Systems

## <p align="center">Part 1: Introduction to SCADA Control Systems

**Purpose:** The purpose of this Lab exercise is to get familiarized with SCADA Control Systems, Docker containers and begin configuring the virtual environment that will be used throughout the remaining labs.

**Objective:** The objective of part 1 of this lab is to research software, protocols and tools used by SCADA Control Systems and the components within the UAH environment. In the conclusion of part 1 of this lab we will be able to operate the control system enviroment.

**Lab Setup:** Need a browser with internet access to conduct research and download any necessary lab files and the scadalab-1.0.ovo.

## Step 1: Introduction to Docker

Get familiarized with Docker https://docker-curriculum.com/

## Step 2: Introduction to the UAH SCADA and DOCKER Environment

The UAH environment will utilize Virtual Box and Docker to simulate two industrial control systems:
- One Tank Water Pump-Three Docker Containers (PLC, HMI & Sbox)
- One Station Gas Pipeline-Three Docker Containers (PLC, HMI & Sbox)

The Water Tank and Gas Pipeline can only be run individually. Login for the virtual machine = (username:ccre, password:ccre) (username:root,password:toor). Recommend logging in as ccre and using sudo to execute privileged commands. NOTE: Any time sudo is used to execute privileged commands you will have to enter the ccre password:ccre
- PLC (Programmable Logic Controller) container is running on Debian with OpenPLC.
- HMI (Human Machine Interface) container is running on Alpine using ScadaBR to display the HMI.
- Sbox (Simulation Box) is running on Debian using a complied MATLAB model and an interface program to simulate the control system traffic.

The following scripts are provided on the virtual machine (/home/ccre/scadalab/scripts) to launch the Docker containers and configure the network environment. These scripts will be utilized throughout the labs, so familiarize yourself with the content and usage of each script.
- ***gaspipeline.sh*** - Stops & removes plc0, HMI, & sbox containers, then starts HMI, plc0 & sbox, running scripts in plc0 & sbox to start the gas pipeline sim & ladder logic
- ***watertank.sh*** - Stops & removes plc0, HMI, & sbox containers, then starts HMI, plc0 & sbox, running scripts in plc0 & sbox to start the Water tank sim & ladder logic
- ***netstart.sh*** - First stops plcnet & datanet, then starts plcnet & datanet (Netstart should only be run once during initial setup of the environment. In addition, it will fail if there are any existing containers attached to either network)
- ***netstop.sh*** - Stops plcnet & datanet
- ***cleanup.sh*** - Brute Force, removes all containers

## Step 3: Setup SCADA LAB Enviroment

***Part 1: Import the virtual machine into virtual box.***

<div align="center">Click “Choose a virtual appliance file to import” icon and browse to the scadalab.ova.</div>
<p align="center"><img src=images/Picture1.png></p>

<div align="center">Click “Finish”</div>
<p align="center"><img src=images/Picture2.png></p>

***Part 2: Login to virtual machine and run Water Tank Docker containers.***

<div align="center">To start the virtual machine in the VirtualBox Manager, select the scadalab VM, and select Start.</div>
<p align="center"><img src=images/Picture3.png></p>

<div align="center">Login using the credentials (username:ccre, password:ccre)</div>
<p align="center"><img src=images/Picture4.png></p>

<div align="center">Start Docker by running sudo service docker start</div>
<p align="center"><img src=images/Picture5.png></p>

<div align="center">Navigate to the scripts folder /home/ccre/scadalab/scripts and run the script to configure the network ./netstart.sh</div>
<p align="center"><img src=images/Picture6.png></p>

<div align="center">Start the Water Tank containers, run ./watertank.sh</div>
<p align="center"><img src=images/Picture7.png></p>

<div align="center">To verify the containers loaded and started correctly, run sudo docker ps in a terminal to view the status of the containers.</div>
<p align="center"><img src=images/Picture8.png></p>

<div align="center">To launch the water tank HMI, pull up the internet browser on the virtual machine and navigate to 100.100.100.2:8080/ScadaBR then login to ScadaBR (username:ccre, password:ccre)</div>
<p align="center"><img src=images/Picture9.png></p>

<div align="center">Verify the IP address of the Modbus data source is pointing to your PLC container (100.100.100.3 – Water Tank). Click on Data Sources on the top menu.</div>
<p align="center"><img src=images/Picture10.png></p>

<div align="center">Click on the edit button for the Water Tank</div>
<p align="center"><img src=images/Picture11.png></p>

<div align="center">Once the edit screen is open, verify the IP address matches the PLC container IP 100.100.100.3 for the Water Tank and then click on the blue floppy disk to save</div>
<p align="center"><img src=images/Picture12.png></p>

Go back to the Data Sources screen and enable the water tank data sources to allow ScadaBR to pull data from OpenPLC
<p align="center"><img src=images/Picture13.png></p>

<div align="center">Click on Graphical Views</div>
<p align="center"><img src=images/Picture14.png></p>

<div align="center">Select the HMI Water Tank. Verify the levels are changing on the Water Tank HMI.</div>
<p align="center"><img src=images/Picture15.png></p>

<div align="center">Disable the Water Tank Data Source</div>
<p align="center"><img src=images/Picture16.png></p>

<div align="center">Start the Single Gas Pipeline, run ./gaspipeline.sh</div>
<p align="center"><img src=images/Picture17.png></p>

<div align="center">To verify the containers loaded and started correctly, run sudo docker ps in a terminal to view the status of the containers.</div>
<p align="center"><img src=images/Picture18.png></p>

<div align="center">Click on the edit button for the Single Gas Pipeline</div>
<p align="center"><img src=images/Picture19.png></p>

<div align="center">Once the edit screen is open, verify the IP address matches the PLC container IP 100.100.100.4 for the Single Gas Pipeline and then click on the blue floppy disk to save</div>
<p align="center"><img src=images/Picture20.png></p>

Go back to the Data Sources screen and enable the Single Gas Pipeline data sources to allow ScadaBR to pull data from OpenPLC
<p align="center"><img src=images/Picture21.png></p>

<div align="center">Select the HMI Single Gas Pipeline. Verify the levels are changing on the Single Gas Pipeline HMI.</div>
<p align="center"><img src=images/Picture22.png></p>

<div align="center">Disable all data sources</div> 
<p align="center"><img src=images/Picture23.png></p>

<div align="center">Run cleanup script ./cleanup</div>
<p align="center"><img src=images/Picture24.png></p>

## Step 4: Interact with HMI and Configure for Unsafe Operations

***Part 1: Interact with the Water Tank HMI***

<div align="center">To start the Water Tank containers, run ./watertank.sh</div>
<p align="center"><img src=images/Picture25.png></p>

<div align="center">Enable the Water Tank Data Source</div>
<p align="center"><img src=images/Picture26.png></p>

<div align="center">Pull up the Water Tank HMI in ScadaBR</div>
<p align="center"><img src=images/Picture27.png></p>

<div align="center">Turn the Pump On by turning on Manual Mode and clicking the “Pump ON” button. Wait 30 seconds and observe the water tank activity</div>
<p align="center"><img src=images/Picture28.png></p>

<div align="center">Now turn the Pump Off by clicking the “Pump OFF” button and observe the activity</div>
<p align="center"><img src=images/Picture29.png></p>

<div align="center">Turn the HMI on Auto and observe the fluctuations in water levels.</div>
<p align="center"><img src=images/Picture30.png></p>

<div align="center">Change setpoints to Minimum=20 and Maximum=25 and observe the difference when range is narrowed</div>
<p align="center"><img src=images/Picture31.png></p>

***Part 2: Configure Water Pump for Unsafe Operation***

<div align="center">Attack 1 – Set the Minimum setpoint more than the Maximum setpoint</div>
<p align="center"><img src=images/Picture32.png></p>

<div align="center">Attack 2 – Set the Minimum setpoint to -5</div>
<p align="center"><img src=images/Picture33.png></p>

<div align="center">Attack 3 – set Maximum setpoint to more than 100</div>
<p align="center"><img src=images/Picture34.jpg></p>

---

## <p align="center">Part 2: SCADA Control System Networking

**Purpose:** The purpose of part 2 in this Lab exercise is to get familiarized with Modbus/TCP protocol and analyze network traffic in the SCADA control system environment.

**Objective:** To utilize Radzio to observe Modbus traffic and Wireshark to analyze network traffic. Wireshark filters will then be applied to view specific traffic and packets. Python will be used to open a network socket and send fake Modbus/TCP queries and responses to clients and servers.

**Lab Setup and Requirements:** The virtual machine and the Water Tank Docker containers running. Radzio! Modbus Master Simulator and Wireshark are used to observe, capture and analyze the network traffic.

## Step 1: Introduction to Modbus

Modbus is a serial communications protocol published for use with its programmable logic controllers (PLCs). Modbus has become a de facto standard communication protocol, and it is now a commonly available means of connecting industrial electronic devices. Modbus is used in multiple master-slave applications to monitor and program devices, communicate between intelligent devices and sensors and instruments and monitor field devices using PCs and HMIs.

Facts about Modbus include:
- Modbus has two implantations, IP/TCP and serial
- Modbus/TCP Relationship is that of master and slave
- Modbus transactions are a three-step process similar to the 3-way-hand shake
  - Request
  - Response from PDU
  - Exception Response PDU
- Modbus functions include: Public, User-defined and Reserved
- Modbus Data types are Discrete input, Discrete output (coils), input registers, and holding registers

## Step 2: Use Water Tank and verify traffic with Radzio! Modbus Master Simulator












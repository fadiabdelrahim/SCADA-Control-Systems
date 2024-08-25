# <p align="center">SCADA-Control-Systems

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



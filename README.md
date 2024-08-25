# <p align="center">SCADA Control Systems

## <p align="center">Part 1: Introduction to SCADA Control Systems

**Purpose:** The purpose of part 1 in this Lab exercise is to get familiarized with SCADA Control Systems, Docker containers and begin configuring the virtual environment that will be used throughout the remaining labs.

**Objective:** The objective of part 1 of this lab is to research software, protocols and tools used by SCADA Control Systems and the components within the UAH environment. In the conclusion of part 1 of this lab we will be able to operate the control system enviroment.

**Lab Setup:** Need a browser with internet access to conduct research and download any necessary lab files and the scadalab-1.0.ovo.

## Step 1: Introduction to Docker

Get familiarized with Docker https://docker-curriculum.com/

## Step 2: Introduction to the UAH SCADA and DOCKER Environment

The UAH environment will utilize Virtual Box and Docker to simulate two industrial control systems:
- One Tank Water Pump -Three Docker Containers (PLC, HMI & Sbox)
- One Station Gas Pipeline -Three Docker Containers (PLC, HMI & Sbox)

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

<div align="center">Start the Water Tank Containers, run ./watertank.sh</div>
<p align="center"><img src=images/Picture35.png></p>

<div align="center">Verify the Modbus traffic using a tool called Radzio. Opena a terminal and navigate to /home/ccre/scadalab/lab2/Radzio</div>
<p align="center"><img src=images/Picture36.png></p>

<div align="center">Run wine RMMS.exe to launch the tool</div>
<p align="center"><img src=images/Picture37.png></p>

<div align="center">Select File > New to open a new table</div>
<p align="center"><img src=images/Picture38.png></p>

<div align="center">Select Connection > Settings</div>
<p align="center"><img src=images/Picture39.png></p>

<div align="center">Select Modbus TCP protocol. IP= PLC VM1 IP (100.100.100.3). TPC Port = 502. Select OK</div>
<p align="center"><img src=images/Picture40.png></p>

<div align="center">Select Connection > Connect. The Polls and Status should be increasing if the Modbus traffic is successfully being transmitted from the PLC container</div>
<p align="center"><img src=images/Picture41.jpg></p>
<p align="center"><img src=images/Picture42.png></p>

## Step 3: Introduction to Wireshark & Traffic Capture

Wireshark is a widely-used network protocol analyzer. With Wireshark, you can view
your network at a microscopic level and use it to capture packets for analysis. It's
also used by hackers to gather data in transit.

<div align="center">Launch Wireshark (Applications > Internet > Wireshark)</div>
<p align="center"><img src=images/Picture43.png></p>

<div align="center">Go to the Capture > Options list and select the interface you want to begin capturing traffic on (plcnet0)</div>
<p align="center"><img src=images/Picture44.png></p>

<div align="center">Select Capture to start capturing the network traffic</div>
<p align="center"><img src=images/Picture45.png></p>

<div align="center">Stop Capture after one minute. Take note of the columns and information captured by Wireshark</div>
<p align="center"><img src=images/Picture46.png></p>

## Step 4: Wireshark filters

<div align="center">Apply the following filter. Ip.addr == 100.100.100.1 this filter is used to focus on packets that are source or destination</div>
<p align="center"><img src=images/Picture47.png></p>

<div align="center">Apply the following filter. ip.addr == 100.100.100.1 && ip.addr == 100.100.100.3 this filter will show only traffic between the virtual machine and the PLC container</div>
<p align="center"><img src=images/Picture48.png></p>

<div align="center">http or dns this filter will show traffic over TCP port 80 (HTTP) and TCP port 53 (DNS)</div>
<p align="center"><img src=images/Picture49.png></p>

<div align="center">tcp.port==502 this filter will show traffic over TCP port 502 (Modbus)</div>
<p align="center"><img src=images/Picture50.png></p>

<div align="center">tcp.flags.reset this filter will show traffic with TCP reset flag</div>
<p align="center"><img src=images/Picture51.png></p>

<div align="center">http.request this filter will show all HTTP get request</div>
<p align="center"><img src=images/Picture52.png></p>

<div align="center">tcp contains traffic this filter will show all TCP traffic</div>
<p align="center"><img src=images/Picture53.png></p>

<div align="center">!(http or dns) this filter will remove all HTTP and DNS traffic</div>
<p align="center"><img src=images/Picture54.png></p>

<div align="center">tcp.analysis.retransmission this filter will show all retransmissions</div>
<p align="center"><img src=images/Picture55.png></p>

<div align="center">Another way to filter for Modbus traffic is mbtcp. Apply this filter to see the traffic between the HMI (100.100.100.2) and the PLC (100.100.100.3) containers</div>
<p align="center"><img src=images/Picture56.png></p>

## Step 5: Python script to open network socket and inject traffic

<div align="center">Open terminal from the Lab 2 directory /home/ccre/scadalab/lab2</div>
<p align="center"><img src=images/Picture57.png></p>

<div align="center">Run nano modbus.py to open the script to update the IP address</div>
<p align="center"><img src=images/Picture58.png></p>

<div align="center">Add the PLC IP (100.100.100.3) to the script and save and close</div>
<p align="center"><img src=images/Picture59.png></p>

<div align="center">Run python3 modbus.py. Press any key and enter to send a new packet. To quit, hit enter</div>
<p align="center"><img src=images/Picture60.png></p>

<div align="center">Launch Wireshark. Go to the Capture > Options list and select the interface plcnet0 and Start Capture</div>
<p align="center"><img src=images/Picture61.png></p>

<div align="center">Send a few packets for Wireshark to capture</div>
<p align="center"><img src=images/Picture62.png></p>

<div align="center">Use filter ip.addr == 100.100.100.1 to see the traffic from the virtual machine. Find where the Modbus traffic injected from the host</div>
<p align="center"><img src=images/Picture63.png></p>

---

## <p align="center">Part 3: SCADA CONTROL SYSTEM NETWORK ENUMERATION AND DENIAL OF SERVICE

**Purpose:** The purpose of part 3 in this Lab exercise is to learn about reconnaissance techniques which expose vulnerabilities commonly found within SCADA control systems.

**Objective:** Use tools to scan the SCADA environment to discover information about the network. Using the reconnaissance information, launch a Denial of Service attack against the SCADA control system.

**Part 3 Lab Setup and Requirements:** Need to have the virtual machine and the Water Pump Docker containers running. Nmap and Low Orbit Ion Canon (LOIC) will be used to conduct the network scan and launch the Denial of Service attack.

## Step 1: Introduction to NMAP/ZENMAP

Nmap is an open source network discovery and audit tool used by network admins to monitor networks and by hackers to learn more about their target. Nmap is used to perform security scans and network audits. It scans for live hosts, operating systems, packet filters and open ports running on remote hosts. Zenmap is the official GUI for Nmap.

<div align="center">Using Zenmap (Applications > Internet > Zenmap), type in the IP address target host (100.100.100.2) or the CIDR notation of the target network</div>
<p align="center"><img src=images/Picture64.png></p>
<p align="center"><img src=images/Picture65.png></p>

<div align="center">If not already running, start Water Tank containers</div>
<p align="center"><img src=images/Picture66.png></p>
<p align="center"><img src=images/Picture67.png></p>
<p align="center"><img src=images/Picture68.png></p>

<div align="center">Verify Docker containers are running using sudo docker ps</div>
<p align="center"><img src=images/Picture69.png></p>

<div align="center">Open and enable the Water Tank HMI in ScadaBR</div>
<p align="center"><img src=images/Picture70.jpg></p>
<p align="center"><img src=images/Picture71.jpg></p>

<div align="center">Xmas scan: sudo nmap -sX 100.100.100.2-3</div>
<p align="center"><img src=images/Picture72.png></p>

<div align="center">This is the Xmas scan. It sends TCP packets with the FIN, PSH, and URG flags (lighting the packet up like a Christmas tree) to the target device. If a port is closed then a RST packet will be returned. If nothing is returned, then there is a possibility that a certain port may be open. Use clues from other kinds of scans to pin down those tricky ports. The advantage to using this method is that it may bypass some unstateful firewalls and packet filters, however, some IDS can be configured to detect some of this.</div>

<div align="center">Null Scan: sudo nmap -sN 100.100.100.2-3</div>
<p align="center"><img src=images/Picture73.png></p>

<div align="center">This is the null scan. It sends TCP packets with no flags set towards the target device. It behaves the same way as the Xmas scan, except with no flags.</div>

<div align="center">ACK Scan: sudo nmap -sA 100.100.100.2-3</div>
<p align="center"><img src=images/Picture74.png></p>

<div align="center">This is the ACK scan. This sends an ACK packet to the target device. It can never tell you if a port is open, but it is useful for mapping out firewalls and finding out whether they are stateful or not.</div>

<div align="center">TCP Connect Scan: sudo nmap -sT 100.100.100.2-3</div>
<p align="center"><img src=images/Picture75.png></p>

<div align="center">This is the TCP connect scan. It makes a full TCP connection with each target port instead of creating raw packets. Useful for users who do not have raw packet privileges and is also the Nmap default scanning technique.</div>

<div align="center">SYN Scan: sudo nmap -sS 100.100.100.2-3</div>
<p align="center"><img src=images/Picture76.png></p>

<div align="center">This is a SYN Scan or Half-Open scan. It only makes half of a TCP connection with the target port.</div>

## Step 2: Network Enumeration using Nmap/Zenmap

<div align="center">Launch Zenmap GUI to begin enumerating the network. (You need to run Zenmap with sudo or Root in order to run a full scan</div>
<p align="center"><img src=images/Picture77.png></p>
<p align="center"><img src=images/Picture78.png></p>

<div align="center">Enter IP range of the target network as the “Target”. Select “Quick Scan” as Profile. Command = nmap -T4 -F 100.100.100.2-3</div>
<p align="center"><img src=images/Picture79.png></p>

<div align="center">Observe nmap scan report for the details of a quick scan</div>
<p align="center"><img src=images/Picture80.png></p>

<div align="center">Scan for the specific port used by Modbus (port 502). Command = nmap -p 502 100.100.100.2-3. Record the IP with port 502 open and the name of the service in use</div>
<p align="center"><img src=images/Picture81.png></p>

## Step 3: Determine OS, Manufacturer and Model of Identified Systems

<div align="center">On host VM, launch Zenmap GUI to begin run a scan to determine OS and version. Command = nmap -A 100.100.100.2-3</div>
<p align="center"><img src=images/Picture82.png></p>

## Step 4: Perform Denial of Service Attack

<div align="center">Open a Terminal from Lab 3 directory (/home/ccre/scadablab/lab3)</div>
<p align="center"><img src=images/Picture83.png></p>

<div align="center">Run mono LOIC.exe</div>
<p align="center"><img src=images/Picture84.png></p>
<p align="center"><img src=images/Picture85.png></p>

<div align="center">Enter PLC IP (100.100.100.3) at Target IP and select TCP as Method</div>
<p align="center"><img src=images/Picture86.png></p>

<div align="center">Click “IMMA CHARGIN MAH LAZER” to start flood</div>
<p align="center"><img src=images/Picture87.png></p>

## Step 5: Use Python to conduct a LAND attack

<div align="center">Open a terminal and navigate to the Lab 3 directory where the python script is located</div>
<p align="center"><img src=images/Picture88.png></p>

<div align="center">Run sudo python land.py</div>
<p align="center"><img src=images/Picture89.png></p>
<p align="center"><img src=images/Picture90.png></p>

## Step 6: Observe effects of DoS attacks on HMI

<div align="center">The LAND attack and LOIC attack should overload the system as it attempts to handle the errors created by the DoS attack. The HMI will slow down, lock up and possibly crash containers and/or the VM</div>
<p align="center"><img src=images/Picture91.png></p>

---

## <p align="center">Part 4: SCADA Control System Network Packet Alteration and Injection

**Purpose:** The purpose of part 4 in this Lab exercise is to learn about vulnerabilities commonly found within SCADA control systems. This lab demonstrates how to exploit common vulnerabilities by injecting traffic and altering data which will compromise the integrity of the SCADA system.

**Objective:** Conduct a man-in-the-middle (MITM) attack using Ettercap. The text-only version of Ettercap will be installed on a new Docker container and used to conduct the MITM attack. Once installed and configured, an Ettercap script will be used to drop Modbus/TCP Query packets. Ettercap script will be created/used to change pressure in the Gas Pipeline.

**Part 4 Setup and Requiirements:** Need the VM and Gas Pipeline Docker containers running. Refer to part 1 for virtual machine and Docker containers setup instructions. Wireshark and the Gas Pipeline HMI need to be running as well to observe traffic modification.

## Step 1: MITM Setup and Install ettercap

Ettercap is a comprehensive suite for man-in-the-middle (MITM) attacks. It features sniffing of live connections, content filtering on the fly and many other interesting tricks. It supports active and passive dissection of many protocols and includes many features for network and host analysis.

<div align="center">Running a MITM container and installing Ettercap. Start Gas Pipeline containers. Verify Docker containers are running using sudo docker ps. Enable the Gas Pipeline data source</div>
<p align="center"><img src=images/Picture92.jpg></p>
<p align="center"><img src=images/Picture93.png></p>
<p align="center"><img src=images/Picture94.png></p>
<p align="center"><img src=images/Picture95.png></p>
<p align="center"><img src=images/Picture96.jpg></p>
<p align="center"><img src=images/Picture97.jpg></p>

<div align="center">From a terminal on the VM, run sudo docker run -ti –net=plcnet –privileged –cap-add=NET_ADMIN –ip 100.100.100.5 –name mitm ubuntu:14.04 bash</div>
<p align="center"><img src=images/Picture98.png></p>

<div align="center">On the MITM container, run apt-get update && apt-get install ettercap-common p0f to update and install Ettercap on mitm container. Enter Y to continue when prompted</div>
<p align="center"><img src=images/Picture99.png></p>

## Step 2: Setting up the MITM attack

<div align="center">On the MITM container, run ettercap -T -q -M arp:remote -i eth0 /100.100.100.2// /100.100.100.4//& (This sets up the ARP poisoning and the “&” makes it run in the background)</div>
<p align="center"><img src=images/Picture100.png></p>

<div align="center">Run jobs to see the status of the ettercap jobs/process running in the background</div>
<p align="center"><img src=images/Picture101.png></p>

<div align="center">Run echo 1 > /proc/sys/net/ipv4/ip_forward to forward the IPv4 traffic</div>
<p align="center"><img src=images/Picture102.png></p>

<div align="center">Run fg 1 to bring a background process to the foreground and take control of background process running ettercap</div>
<p align="center"><img src=images/Picture103.png></p>

<div align="center">Open Wireshark and notice the Retransmissions occurring while the MITM attack is ongoing</div>
<p align="center"><img src=images/Picture104.jpg></p>

## Step 3: Use Ettercap Filter to drop traffic

<div align="center">Copy the dropmodbustraffic.filter from the lab4 folder to the MITM container. From the terminal, navigate to the lab4 folder and run: sudo docker cp dropmodbustraffic.filter mitm:/dropmodbustraffic.filter</div>
<p align="center"><img src=images/Picture105.png></p>

<div align="center">In the mitm container, run etterfilter dropmodbustraffic.filter -o dropmodbustraffic.ef on the MITM container</div>
<p align="center"><img src=images/Picture106.png></p>

<div align="center">Run ettercap -T -q -F dropmodbustraffic.ef -M arp:remote -I eth0 /100.100.100.2// /100.100.100.4//&</div>
<p align="center"><img src=images/Picture107.png></p>

<div align="center">You should see the message “MODBUS TRAFFIC FOUND -> DROPPED MODBUS TRAFFIC” as the packets are found and dropped</div>
<p align="center"><img src=images/Picture108.png></p>

## Step 4: Use Ettercap filter to change Gas Pipeline Value

<div align="center">Copy the changepressure.filter from the lab4 folder to the MITM container. From the terminal, navigate to the lab4 folder and run: sudo docker cp change_pressure.filter mitm:/change_pressure.filter</div>
<p align="center"><img src=images/Picture109.png></p>

<div align="center">In the mitm container, run etterfilter change_pressure.filter -o change_pressure.ef on the MITM container</div>
<p align="center"><img src=images/Picture110.png></p>

<div align="center">Run ettercap -T -q -F change_pressure.ef -M arp:remote -I eth0 /100.100.100.2// /100.100.100.4//&</div>
<p align="center"><img src=images/Picture111.png></p>

<div align="center">Run echo 1 > /proc/sys/net/ipv4/ip_forward to forward the IPv4 traffic</div>
<p align="center"><img src=images/Picture112.png></p>

<div align="center">You should see the message “data changed” as the packets are discovered, and data injected</div>
<p align="center"><img src=images/Picture113.png></p>

## Step 5: Use Ettercap filter to Alter Gas Pipeline traffic

<div align="center">Copy the stuxnet.filter from the lab4 folder to the MITM container. From the terminal, navigate to the lab4 folder and run: sudo docker cp stuxnet.filter mitm:/stuxnet.filter</div>
<p align="center"><img src=images/Picture114.png></p>

<div align="center">In the mitm container, run etterfilter stuxnet.filter -o stuxnet.ef on the MITM container</div>
<p align="center"><img src=images/Picture115.png></p>

<div align="center">Run ettercap -T -q -F stuxnet.ef -M arp:remote -i eth0 /100.100.100.2// /100.100.100.4//&</div>
<p align="center"><img src=images/Picture116.png></p>

<div align="center">Run echo 1 > /proc/sys/net/ipv4/ip_forward to forward the IPv4 traffic. You should see the messages “data injected” OR “data injected again” as the packets are altered, and data injected</div>
<p align="center"><img src=images/Picture117.png></p>

---

## Part 5: SCADA CONTROL SYSTEM NETWORK INTRUSTION DETECTION

**Purpose:** The purpose of part 5 in this Lab exercise is to learn about detecting and preventing attacks in SCADA control systems. The installation, configuration, and setup of the Snort Intrusion Detection System will be carried out to detect potential attacks.

**Objective:** Install and configure Snort to monitor the SCADA network traffic and configure Snort rules to detect/alert on Modbus traffic. Whitelist Modbus traffic in the Snort configuration files and write rules to detect DoS attack and NMAP scan.

**Part 5 Setup and Requirements:** Need to have the VM and either the Gas Pipeline or Water Pump Docker containers running. The browser on the SCADA VM will need internet access to download Snort files.

## Step 1: Installing Snort














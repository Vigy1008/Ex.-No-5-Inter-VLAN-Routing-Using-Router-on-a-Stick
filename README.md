
# Ex. No: 5 Inter-VLAN Routing Using Router-on-a-Stick
## Date: 13/09/2025
## Name: VIGNESHWARAN VINAYAGAMOORTHY
# RegNo: 212223060301

________________________________________
# Objective
To configure Inter-VLAN routing using a single router interface with subinterfaces (Router-on-a-Stick) so that hosts in different VLANs can communicate with each other.
________________________________________
# Apparatus/Tools Required
•	Cisco Packet Tracer<br>
•	1 Router (e.g., 2911)<br>
•	1 Managed Switch (e.g., 2960)<br>
•	4 PCs<br>
•	Straight-through Ethernet cables<br>
________________________________________
# Network Topology Diagram
# Description:
•	PC0 and PC1 belong to VLAN 10 (192.168.10.0/24)<br>
•	PC2 and PC3 belong to VLAN 20 (192.168.20.0/24)<br>
•	Switch connected to Router via a trunk port (FastEthernet0/1 on switch → GigabitEthernet0/0 on router)<br>
•	Router subinterfaces handle VLAN routing<br>
(Insert screenshot of your Packet Tracer setup here)<br>
________________________________________
# IP Addressing Table
Device	VLAN	IP Address	Subnet Mask	Port/Interface<br>
PC0	10	192.168.10.1	255.255.255.0	FastEthernet0/1<br>
PC1	10	192.168.10.2	255.255.255.0	FastEthernet0/2<br>
PC2	20	192.168.20.1	255.255.255.0	FastEthernet0/3<br>
PC3	20	192.168.20.2	255.255.255.0	FastEthernet0/4<br>
Router G0/0.10	10	192.168.10.254	255.255.255.0	Subinterface VLAN 10<br>
Router G0/0.20	20	192.168.20.254	255.255.255.0	Subinterface VLAN 20<br>
________________________________________
# Procedure
1.	Setup devices in Packet Tracer: Place 4 PCs, 1 switch, and 1 router.<br>
2.	Cabling:<br>
o	PCs to switch ports (PC0–F0/1, PC1–F0/2, PC2–F0/3, PC3–F0/4)<br>
o	Switch F0/5 to Router G0/0<br>
3.	Assign IP addresses to each PC as per the IP table.<br>
4.	Switch Configuration:<br>
o	Create VLAN 10 and VLAN 20<br>
o	Assign ports F0/1–F0/2 to VLAN 10, ports F0/3–F0/4 to VLAN 20<br>
o	Configure trunk on port F0/5 to the router<br>
5.	Router Configuration (Router-on-a-Stick):<br>
o	Enable subinterfaces G0/0.10 and G0/0.20<br>
o	Assign encapsulation dot1q for each VLAN ID<br>
o	Assign IP addresses to each subinterface (default gateway for respective VLANs)<br>
6.	Testing:<br>
o	Ping from PC0 to PC2 (should succeed after routing is configured)<br>
o	Ping between PCs in the same VLAN (should succeed)<br>
________________________________________
# Commands Used
Switch Configuration:<br>

Switch> enable<br>
Switch# configure terminal<br>
Switch(config)# vlan 10<br>
Switch(config-vlan)# name STAFF<br>
Switch(config-vlan)# exit<br>
Switch(config)# vlan 20<br>
Switch(config-vlan)# name STUDENTS<br>
Switch(config-vlan)# exit<br>
Switch(config)# interface range fastethernet0/1 - 2<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 10<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface range fastethernet0/3 - 4<br>
Switch(config-if-range)# switchport mode access<br>
Switch(config-if-range)# switchport access vlan 20<br>
Switch(config-if-range)# exit<br>
Switch(config)# interface fastethernet0/5<br>
Switch(config-if)# switchport mode trunk<br>
Switch(config-if)# exit<br>


Router Configuration:<br>

Router> enable<br>
Router# configure terminal<br>
Router(config)# interface gigabitethernet0/0.10<br>
Router(config-subif)# encapsulation dot1Q 10<br>
Router(config-subif)# ip address 192.168.10.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0.20<br>
Router(config-subif)# encapsulation dot1Q 20<br>
Router(config-subif)# ip address 192.168.20.254 255.255.255.0<br>
Router(config-subif)# no shutdown<br>
Router(config)# interface gigabitethernet0/0<br>
Router(config-if)# no shutdown<br>
________________________________________
# Output (Screenshots)
### •	Logical Setup<br>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a4f595d2-3bd4-4e79-99cb-dc3d44550c00" />
<br>

### •	VLAN configuration on the switch<br>
<img width="788" height="547" alt="image" src="https://github.com/user-attachments/assets/379b9fd7-677e-46fd-a895-c9dc6315d54a" />
<br>

### •	Router subinterface configuration<br>

<img width="917" height="196" alt="image" src="https://github.com/user-attachments/assets/88d77c9b-5aa8-4043-b395-0f3466a066fa" />
<br>

### •	PC IP settings<br>
#### PC0
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d7d87991-d2ba-4800-8442-798050da2130" />
<br>

#### PC1
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b3fdfd19-d772-4c87-a0a1-26e671d2996e" />
<br>

### •	Successful ping between PCs in different VLANs after routing(Pinging from PC1 to PC0)<br>
<img width="877" height="888" alt="image" src="https://github.com/user-attachments/assets/dec189db-9ced-492a-9dc7-76c793501bd9" />
<br>

### •	Successful ping between PCs in the same VLAN(Pinging from PC2 to PC0)<br>
<img width="877" height="888" alt="image" src="https://github.com/user-attachments/assets/4f7327ba-c7a5-4ad2-85c6-3e52e6ce6bf8" />

________________________________________
# Result
Inter-VLAN routing was successfully configured using the Router-on-a-Stick method. PCs in different VLANs could communicate through the router.

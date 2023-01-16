# A Study on Router access restriction on a VLAN Network

By Saksham Rawat

## Project Description:

An organization uses a VLAN-based network. There are 4 VLAN’s on the
network, namely VLAN 1, VLAN 2, VLAN 3 and VLAN 4. The VLAN’S are
mapped with the IP networks 192.168.1.0/24, 192.168.2.0/24, 192.168.3.0/24,
and 192.168.4.0/24. It is required that only VLAN A should be able to remote
access the router using telnet. All the other VLAN’s should be blocked. To
demonstrate the solution a lab is set up with Cisco routers and switches with the
topology simulated. The necessary configurations required to achieve the
solutions is identified.

## Networking requirement:

1. Network Design strategy.
2. VLAN and IP network Design.
3. Network Topology diagram.
4. Configurations required on switches, routers, and PC.

## Network Design strategy:

Unique VLAN’s are assigned to the different departments. VLAN 1 is assigned to
A, VLAN 2 is assigned to B, VLAN 3 is assigned to C and VLAN 4 is assigned to
D. The VLAN’s are mapped with unique network addresses. Appropriate
configurations are performed on the router for communication between the


users belonging to the different departments ( VLAN’S). Access control lists are
used on VLAN’S to provide restrictions to the router.
VLAN and IP Network Design

### VLAN Department IP Network

### VLAN 1 A 192.168.1.0/

### VLAN 2 B 192.168.2.0/

### VLAN 3 C 192.168.3.0/

### VLAN 4 D 192.168.4.0/

The VLAN’s are mapped with the network addresses as shown in the above
table. The users (PC) belonging to the different department are configured with
IP addresses belonging to the IP network address range as shown in the table.

## Network Topology Diagram:

![image](https://user-images.githubusercontent.com/90713896/212735304-6bc0cf9b-459c-483a-9229-42af754e2211.png)



## Network and System Integration

The PC’s belonging to respective departments are configured with IP addresses
belonging to the network address of the specific VLAN’S. The respective ports
on the switches are made members of the appropriate VLAN’s. A link is
connected to the router from the switch, which is used for carrying traffic from
different VLAN’s and for Inter-VLAN communication.

## Configurations

## Switch configuration

### Create VLAN’s on the switch with respective names.

### switch(config)#vlan 1

### switch(config-vlan)#name A

### switch(config-vlan)#exit

### switch(config)#vlan 2

### switch(config-vlan)#name B

### switch(config-vlan)#exit

### switch(config)#vlan 3

### switch(config-vlan)#name C

### switch(config-vlan)#exit

### switch(config)#vlan 4

### switch(config-vlan)#name D

### switch(config-vlan)#exit


### Create ports on the switch as members of different VLAN’s

The belong configuration shows how Port 1 on the switch is made a member of
VLAN 1.
_switch(config)#interface fastethernet 0/_

### switch(config-if)#switchport mode access

### switch(config-if)#switchport access vlan 1

### switch(config-if)#exit

The belong configuration shows how Port 5 on the switch is made a member of
VLAN 2.

### switch(config)#interface fastethernet 0/

### switch(config-if)#switchport mode access

### switch(config-if)#switchport access vlan

### switch(config-if)#exit

The below configuration shows how Port 6 on the switch is made a Member of
VLAN 3.

### switch(config)#interface fastethernet 0/

### switch(config-if)#switchport mode access

### switch(config-if)#switchport access vlan

### switch(config-if)#exit

The belong configuration shows how Port 7 on the switch is made a member of
VLAN 4.

### switch(config)#interface fastethernet 0/


### switch(config-if)#switchport mode access

### switch(config-if)#switchport access vlan

### switch(config-if)#exit

After the ports are made members of different VLAN’s, the link connecting the
switch to router is configured as a trunk port. The below configuration shows
how to configure the port as a trunk. Port 8 on the switch is configured as a
trunk port. The port would carry traffic from all the created VLAN’s.

### switch(config)#interface fastethernet 0/

### switch(config-if)#switchport mode trunk

### switch(config-if)#switchport trunk allowed vlan all

### switch(config-if)#exit

## Router Configurations:

### Configure VLAN’s with respective IP addresses

Configures a sub interface on the physical interface fast Ethernet 0/1. The sub
interface is created with the IP address 192.168.1.1. The interface is mapped
with VLAN 1 and would be the gateway address for users belonging to
VLAN 1. The configuration detail is shown below

### router(config)#interface fast Ethernet 0/0.

### router(config-subif)#encapsulation dot1Q 1

### router(config-subif)#ip address 192.168.1.1 255.255.255.

### router(config-subif)#no shutdown

### router(config-subif)#exit


Configures a sub interface on the physical interface fast Ethernet 0/1. The sub
interface is created with the IP address 192.168.2.1. The interface is mapped
with VLAN 2 and would be the gateway address for users belonging to
VLAN 2. The configuration detail is shown below

### router(config)#interface fast Ethernet 0/0.

### router(config-subif)#encapsulation dot1Q 2

### router(config-subif)#ip address 192.168.2.1 255.255.255.

### router(config-subif)#no shutdown

### router(config-subif)#exi

### t

Configures a sub interface on the physical interface fast Ethernet 0/1. The sub
interface is created with the IP address 192.168.3.1. The interface is mapped
with VLAN 3 and would be the gateway address for users belonging to
VLAN 3.The configuration detail is shown below

### router(config)#interface fastethernet 0/0.

### router(config-subif)#encapsulation dot1Q 3

### router(config-subif)#ip address 192.168.3.1 255.255.255.

### router(config-subif)#no shutdown

Configures a sub interface on the physical interface fast Ethernet 0/1. The sub
interface is created with the IP address 192.168.4.1. The interface is mapped
with VLAN 4 and would be the gateway address for users belonging to
VLAN 4. The configuration detail is shown below

### router(config)#interface fastethernet 0/0.

### router(config-subif)#encapsulation dot1Q 4


### router(config-subif)#ip address 192.168.4.1 255.255.255.

### router(config-subif)#no shutdown

### router(config-subif)#exit

## Telnet configuration on router:

### Router(config)# line vty 0 4 Router(config-line)# password cisco

### Router (config)# enable password cisco (Configure enable password)

## Access restriction to telnet:

Create a standard ACL which would allow traffic from VLAN 4 (192.168.4.
network)

### Router(config)#access-list 1 permit 192.168.4.0 0.0.0.255.

Apply the ACL on the telnet interface Router(config)#line vty 0 4

### Router(config-line)#access-class 1 in (1 is the access list number created

### above)

The above configuration would ensure that only VLAN 4, which is the IT
department can telnet to the router.


## PC Configuration:

### PC IP address Switch Port

### PC1 (A) 192.168.1. 2 1

### PC2 (B) 192.168.1. 3 2

### PC3 (C) 192.168.2. 2 3

### PC4 (D) 192.168.2. 3 4

### The gateway for the PC’s are configured as the respective VLAN IP

### addresses configured on the router, as shown in the topology diagram.

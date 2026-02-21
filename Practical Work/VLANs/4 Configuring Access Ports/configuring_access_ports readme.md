## Access Port Configuration – Pre-Configuration State

Before configuring access ports for the Clients and Servers VLANs, the existing configuration of the relevant interfaces on Switch22 was reviewed to confirm they were in their default state.

### Command
```text
show run


interface GigabitEthernet0/0
 negotiation auto
!
interface GigabitEthernet0/2
 negotiation auto
!
interface GigabitEthernet0/3
 negotiation auto
!
interface GigabitEthernet1/0
 negotiation auto
!
interface GigabitEthernet1/1
 negotiation auto
!         
interface GigabitEthernet1/2
 negotiation auto
!
interface GigabitEthernet1/3
 negotiation auto
!
interface GigabitEthernet2/0
 negotiation auto
!
interface GigabitEthernet2/1
 negotiation auto
!
interface GigabitEthernet2/2
 negotiation auto
!
interface GigabitEthernet2/3
 negotiation auto
!


Access Port Configuration – VLAN Assignment

Access ports were configured on all three switches with ports gi1/0–3 assigned to the Clients VLAN (VLAN 5) and ports gi2/0–3 assigned to the Servers VLAN (VLAN 6). Configuration was verified using show run on each switch.




IP change for VLAN 5 (Clients)
PC1: ip 192.168.5.11/24
PC2: ip 192.168.5.12/24


A ping test was done from PC! to PC2
ping 192.168.5.12

* Replies was received
* No packet loss
* Confirms VLAN 5 access-port configuration works

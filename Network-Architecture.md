## Layer 1:

### Backbone

* TL-SG108E managed switch (8 ports, VLAN trunking)

* Raspberry Pi 4B (Named: PiWRT, main router)

* TP-Link Archer C7 v5.6 (Named: ArcherWRT -- OpenWRT smart switch)

* Netgear R6400v2 (Named: NetWRT -- repeater AP)

* TP-Link Deco X60 (Home Wi-Fi AP, stock firmware)

* Google WiFi Puck (Named: GoogleWRT -- OpenWRT AP for Guest + IoT)

### Direct cabling (switch ports)

* Port 1: ArcherWRT (uplink trunk)

* Port 5: Deco X60 (Home VLAN untagged)

* Port 6: GoogleWRT (Guest + IoT trunk)

* Port 7: Pop!_OS Admin machine

* Port 8: PiWRT (main router trunk)

### End devices (wired into ArcherWRT)

* LAN1: GPU node

* LAN2: Beelink S12 Mini PC

* LAN3: Lenovo Tiny M700

* LAN4: Lenovo Tiny M700

---
# Layer 2:

### Switch VLAN configs (TL-SG108E)

* VLAN 10 (Home): Ports 5 (U), 8 (T)

* VLAN 20 (Guest): Ports 6 (T), 8 (T)

* VLAN 30 (Server): Ports 1 (T), 8 (T)

* VLAN 40 (Admin): Ports 1 (T), 6 (T), 7 (U), 8 (T)

* VLAN 50 (DMZ): Ports 1 (T), 8 (T)

* VLAN 60 (IoT): Ports 6 (T), 8 (T)

### PVIDs (default untagged assignment)

* Port 5 → VLAN 10

* Port 7 → VLAN 40

* Others default → VLAN 1

### ArcherWRT VLAN configs

* VLAN 30 (Server): CPU/eth0 (T), LAN1-4 (U), WAN (T)

* VLAN 40 (Admin): CPU/eth0 (T), WAN (T)

* VLAN 50 (DMZ): CPU/eth0 (T), LAN1 (T), WAN (T)

---
## Layer 3

## Routing
### PiWRT (OpenWRT, router-on-a-stick)

* Source of all inter-VLAN routing

* Static subnets per VLAN:

  * VLAN 10 (Home): 192.168.10.0/24

  * VLAN 20 (Guest): 192.168.20.0/24

  * VLAN 30 (Server): 192.168.30.0/24

  * VLAN 40 (Admin): 192.168.40.0/24

  * VLAN 50 (DMZ): 192.168.50.0/24

  * VLAN 60 (IoT): 192.168.60.0/24

### Static IPs (already assigned):

* PiWRT → 192.168.1.1 (router)

* TL-SG108E → 192.168.40.3

* ArcherWRT → 192.168.40.4

* GoogleWRT → 192.168.40.5

* NetWRT → 192.168.40.6

* Deco X60 → 192.168.10.9

---

## Layers 5-7

#### Access rules (firewall on PiWRT):

* VLAN 10 (Home):

* WAN access

* Access to VLAN 30 servers 

### No access to router WebUI/SSH 

#### VLAN 20 (Guest):

* WAN only 

* Isolated from all VLANs 

### VLAN 30 (Server):

* WAN access 

* Serve files to VLAN 10 

* Isolated from other VLANs 

### VLAN 40 (Admin):

* Full access to everything 

### VLAN 50 (DMZ):

* WAN access 

* No LAN access 

* Devices isolated from each other 

### VLAN 60 (IoT):

* WAN access 

* No LAN access 

* Devices isolated from each other

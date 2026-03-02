# Cisco Core Switch (C2960G)

## System Information
* **Hostname:** SW1-LAB
* **IOS Version:** Ver 15.0
* **Management IP:** 10.80.99.2

## VLANs
* **VLAN 20:** WIRED-USERS
* **VLAN 30:** WIRELESS-USERS
* **VLAN 40:** WIRELESS-GUEST
* **VLAN 50:** SERVER
* **VLAN 99:** MGMT
* **VLAN 999:** BLACKHOLE

## Physical Port Mapping
| Interface | Connected to | Vlan configuration | Notes           |
|-----------|--------------|--------------------|-----------------|
| Gi0/6     | Prox-LAB     | Access (VLAN 50)   | Hypervisor link |
| Gi0/18    | pfSense-LAB  | Trunk (All VLANs)  | Main Uplink     |
| Gi0/20    | AP-U7        | Trunk              | Wi-Fi Networks  |

## Running Config Snippets
### pfSense
```text
interface GigabitEthernet0/18
 description Uplink_pfSense
 switchport trunk native vlan 999
 switchport trunk allowed vlan 20,30,40,50,99
 switchport mode trunk
 spanning-tree portfast trunk
 ```
### UniFi AP
```text
interface GigabitEthernet0/20
 description Wireless AP
 switchport trunk native vlan 99
 switchport trunk allowed vlan 20,30,40,99
 switchport mode trunk
 spanning-tree portfast trunk
 ```
### Server
```text
interface GigabitEthernet0/6
 description Proxmox
 switchport access vlan 50
 switchport mode access
 spanning-tree portfast
 ```
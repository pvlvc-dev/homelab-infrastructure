# pfSense Router (Lenovo M720q)

## Hardware specifications
* **CPU:** Intel(R) Core(TM) i5-9400T CPU @ 1.80GHz 
* **RAM:** 8gb 3200Mhz
* **NICs:** IBM I340-T4 Quad Port NIC with PCI-E riser

## Interface assignments
* **WAN Interface:** igb0 - Connected to ISP modem
* **LAN Interface:** igb1 - Connected to Cisco C2960G (Interface gi0/18)

## Firewall rules
### WIREDUSERS
| Action | Protocol     | Source             | Destination       | Destination port | Description     |
|--------|--------------|--------------------|-------------------|------------------|-----------------|
| Allow  | IPv4 TCP/UDP | WIREDUSERS subnets | This firewall     | 53 (DNS)         | Allow DNS       |
| Allow  | IPv4 ICMP    | WIREDUSERS subnets | This firewall     | *                | Allow ping      |
| Allow  | IPv4         | WIREDUSERS subnets | SERVER subnets    | *                | Allow server    |
| Allow  | IPv4         | WIREDUSERS subnets | MGMT subnets      | *                | Allow mgmt      |
| Block  | IPv4         | WIREDUSERS subnets | WIFIGUEST subnets | *                | Block guests    |
| Allow  | IPv4         | WIREDUSERS subnets | *                 | *                | Internet access |
### WIFIUSERS
| Action | Protocol     | Source            | Destination       | Destination port | Description     |
|--------|--------------|-------------------|-------------------|------------------|-----------------|
| Allow  | IPv4 TCP/UDP | WIFIUSERS subnets | This firewall     | 53 (DNS)         | Allow DNS       |
| Allow  | IPv4 ICMP    | WIFIUSERS subnets | This firewall     | *                | Allow ping      |
| Allow  | IPv4         | WIFIUSERS subnets | SERVER subnets    | *                | Allow server    |
| Block  | IPv4         | WIFIUSERS subnets | MGMT subnets      | *                | Block mgmt      |
| Block  | IPv4         | WIFIUSERS subnets | WIFIGUEST subnets | *                | Block guests    |
| Allow  | IPv4         | WIFIUSERS subnets | *                 | *                | Internet access |
### WIFIGUEST
| Action | Protocol     | Source            | Destination   | Destination port | Description           |
|--------|--------------|-------------------|---------------|------------------|-----------------------|
| Allow  | IPv4 TCP/UDP | WIFIGUEST subnets | This firewall | 53 (DNS)         | Allow DNS             |
| Allow  | IPv4 ICMP    | WIFIGUEST subnets | This firewall | *                | Allow ping            |
| Block  | IPv4         | WIFIGUEST subnets | RFC1918       | *                | Block internal access |
| Allow  | IPv4         | WIFIGUEST subnets | *             | *                | Internet access       |
### SERVER
| Action | Protocol     | Source         | Destination   | Destination port | Description            |
|--------|--------------|----------------|---------------|------------------|------------------------|
| Allow  | IPv4 TCP/UDP | SERVER subnets | 10.80.50.1    | 53 (DNS)         | Allow DNS              |
| Allow  | IPv4 TCP/UDP | SERVER subnets | 10.80.50.1    | 123 (NTP)        | Allow NTP              |
| Allow  | IPv4 ICMP    | SERVER subnets | This firewall | *                | Allow ping             |
| Allow  | IPv4         | CTRL_Unifi     | *             | *                | Unifi controller       |
| Block  | IPv4         | SERVER subnets | Internal_nets | *                | Block lateral movement |
| Allow  | IPv4         | SERVER subnets | *             | *                | Internet access        |
### MGMT
| Action | Protocol     | Source       | Destination   | Destination port | Description      |
|--------|--------------|--------------|---------------|------------------|------------------|
| Allow  | IPv4 TCP/UDP | MGMT subnets | 10.80.50.1    | 53 (DNS)         | Allow DNS        |
| Allow  | IPv4 ICMP    | MGMT subnets | This firewall | *                | Allow ping       |
| Allow  | IPv4         | MGMT subnets | CTRL_Unifi    | *                | Unifi controller |
| Allow  | IPv4         | MGMT subnets | *             | *                |                  |

## Core services
* DHCP Server (Managing VLANs: 20,30,40,50,99)
* OpenVPN Endpoint
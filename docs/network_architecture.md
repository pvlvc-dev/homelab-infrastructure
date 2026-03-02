# Network Architecture

## IP Address Scheme
A master list of the assigned IP addresses.

## VLAN Segmentation
Configured on the Cisco C2960G and routed via pfSense.

## DNS & DHCP
* **DHCP Server:** Handled by pfSense across all VLANs. 
* **Internal DNS:** AdGuard Home (LXC on Prox-LAB). pfSense DHCP pushes the AdGuard IP as the primary DNS server to all clients.
* **Upstream DNS:** Cloudflare (1.1.1.1) and Quad9 (9.9.9.9).

## Remote Access (VPN)
* **Protocol:** OpenVPN
* **Server:** pfSense-LAB
* **Tunnel Network:** 10.x.x.x
* **Access Rules:** 
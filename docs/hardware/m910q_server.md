# Proxmox Hypervisor (Lenovo M910q)

## Hardware & Storage
* **CPU:** Intel(R) Core(TM) i7-7700T CPU @ 2.90GHz
* **RAM:** 8gb 3200Mhz
* **Boot Drive:** 256gb SSD
* **VM/LXC Storage:** 152 storage pool

## VM and Container Inventory
| ID  | Hostname | IP Address  | OS     | Role          |
|-----|----------|-------------|--------|---------------|
| 100 | UniFi    | 10.80.50.15 | Ubuntu | AP Controller |
| 101 | adguard  | 10.80.50.16 | Ubuntu | Internal DNS  |
| 102 | Seafile  | 10.80.50.20 | Ubuntu | File storage  |

## Power Cycle Procedures
> **Note:** This hardware is not 24/7. Expected uptime is ~8 hours a day when in use.
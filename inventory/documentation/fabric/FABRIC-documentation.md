# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | l3leaf | BDR1-FAB1 | 192.168.1.152/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | BDR1-FAB2 | 192.168.1.162/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | BDR2-FAB1 | 192.168.1.153/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | BDR2-FAB2 | 192.168.1.163/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF1-FAB1 | 192.168.1.156/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF1-FAB2 | 192.168.1.166/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF2-FAB1 | 192.168.1.157/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF2-FAB2 | 192.168.1.167/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF3-FAB1 | 192.168.1.158/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF3-FAB2 | 192.168.1.168/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF4-FAB1 | 192.168.1.159/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | DLF4-FAB2 | 192.168.1.169/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | SPN1-FAB1 | 192.168.1.150/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | SPN1-FAB2 | 192.168.1.160/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | SPN2-FAB1 | 192.168.1.151/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | SPN2-FAB2 | 192.168.1.161/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | SVC1-FAB1 | 192.168.1.154/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | SVC1-FAB2 | 192.168.1.164/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | SVC2-FAB1 | 192.168.1.155/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | SVC2-FAB2 | 192.168.1.165/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | BDR1-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet1 |
| l3leaf | BDR1-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet1 |
| l3leaf | BDR1-FAB1 | Ethernet3 | l3leaf | BDR1-FAB2 | Ethernet3 |
| l3leaf | BDR1-FAB1 | Ethernet7 | mlag_peer | BDR2-FAB1 | Ethernet7 |
| l3leaf | BDR1-FAB1 | Ethernet8 | mlag_peer | BDR2-FAB1 | Ethernet8 |
| l3leaf | BDR1-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet1 |
| l3leaf | BDR1-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet1 |
| l3leaf | BDR1-FAB2 | Ethernet7 | mlag_peer | BDR2-FAB2 | Ethernet7 |
| l3leaf | BDR1-FAB2 | Ethernet8 | mlag_peer | BDR2-FAB2 | Ethernet8 |
| l3leaf | BDR2-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet2 |
| l3leaf | BDR2-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet2 |
| l3leaf | BDR2-FAB1 | Ethernet3 | l3leaf | BDR2-FAB2 | Ethernet3 |
| l3leaf | BDR2-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet2 |
| l3leaf | BDR2-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet2 |
| l3leaf | DLF1-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet5 |
| l3leaf | DLF1-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet5 |
| l3leaf | DLF1-FAB1 | Ethernet7 | mlag_peer | DLF2-FAB1 | Ethernet7 |
| l3leaf | DLF1-FAB1 | Ethernet8 | mlag_peer | DLF2-FAB1 | Ethernet8 |
| l3leaf | DLF1-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet5 |
| l3leaf | DLF1-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet5 |
| l3leaf | DLF1-FAB2 | Ethernet7 | mlag_peer | DLF2-FAB2 | Ethernet7 |
| l3leaf | DLF1-FAB2 | Ethernet8 | mlag_peer | DLF2-FAB2 | Ethernet8 |
| l3leaf | DLF2-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet6 |
| l3leaf | DLF2-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet6 |
| l3leaf | DLF2-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet6 |
| l3leaf | DLF2-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet6 |
| l3leaf | DLF3-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet7 |
| l3leaf | DLF3-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet7 |
| l3leaf | DLF3-FAB1 | Ethernet7 | mlag_peer | DLF4-FAB1 | Ethernet7 |
| l3leaf | DLF3-FAB1 | Ethernet8 | mlag_peer | DLF4-FAB1 | Ethernet8 |
| l3leaf | DLF3-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet7 |
| l3leaf | DLF3-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet7 |
| l3leaf | DLF3-FAB2 | Ethernet7 | mlag_peer | DLF4-FAB2 | Ethernet7 |
| l3leaf | DLF3-FAB2 | Ethernet8 | mlag_peer | DLF4-FAB2 | Ethernet8 |
| l3leaf | DLF4-FAB1 | Ethernet1 | spine | SPN1-FAB1 | Ethernet8 |
| l3leaf | DLF4-FAB1 | Ethernet2 | spine | SPN2-FAB1 | Ethernet8 |
| l3leaf | DLF4-FAB2 | Ethernet1 | spine | SPN1-FAB2 | Ethernet8 |
| l3leaf | DLF4-FAB2 | Ethernet2 | spine | SPN2-FAB2 | Ethernet8 |
| spine | SPN1-FAB1 | Ethernet3 | l3leaf | SVC1-FAB1 | Ethernet1 |
| spine | SPN1-FAB1 | Ethernet4 | l3leaf | SVC2-FAB1 | Ethernet1 |
| spine | SPN1-FAB2 | Ethernet3 | l3leaf | SVC1-FAB2 | Ethernet1 |
| spine | SPN1-FAB2 | Ethernet4 | l3leaf | SVC2-FAB2 | Ethernet1 |
| spine | SPN2-FAB1 | Ethernet3 | l3leaf | SVC1-FAB1 | Ethernet2 |
| spine | SPN2-FAB1 | Ethernet4 | l3leaf | SVC2-FAB1 | Ethernet2 |
| spine | SPN2-FAB2 | Ethernet3 | l3leaf | SVC1-FAB2 | Ethernet2 |
| spine | SPN2-FAB2 | Ethernet4 | l3leaf | SVC2-FAB2 | Ethernet2 |
| l3leaf | SVC1-FAB1 | Ethernet7 | mlag_peer | SVC2-FAB1 | Ethernet7 |
| l3leaf | SVC1-FAB1 | Ethernet8 | mlag_peer | SVC2-FAB1 | Ethernet8 |
| l3leaf | SVC1-FAB2 | Ethernet7 | mlag_peer | SVC2-FAB2 | Ethernet7 |
| l3leaf | SVC1-FAB2 | Ethernet8 | mlag_peer | SVC2-FAB2 | Ethernet8 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 198.18.249.0/25 | 128 | 32 | 25.0 % |
| 198.18.251.0/25 | 128 | 32 | 25.0 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| BDR1-FAB1 | Ethernet1 | 198.18.249.9/31 | SPN1-FAB1 | Ethernet1 | 198.18.249.8/31 |
| BDR1-FAB1 | Ethernet2 | 198.18.249.11/31 | SPN2-FAB1 | Ethernet1 | 198.18.249.10/31 |
| BDR1-FAB1 | Ethernet3 | 172.16.100.0/31 | BDR1-FAB2 | Ethernet3 | 172.16.100.1/31 |
| BDR1-FAB2 | Ethernet1 | 198.18.251.49/31 | SPN1-FAB2 | Ethernet1 | 198.18.251.48/31 |
| BDR1-FAB2 | Ethernet2 | 198.18.251.51/31 | SPN2-FAB2 | Ethernet1 | 198.18.251.50/31 |
| BDR2-FAB1 | Ethernet1 | 198.18.249.13/31 | SPN1-FAB1 | Ethernet2 | 198.18.249.12/31 |
| BDR2-FAB1 | Ethernet2 | 198.18.249.15/31 | SPN2-FAB1 | Ethernet2 | 198.18.249.14/31 |
| BDR2-FAB1 | Ethernet3 | 172.16.100.2/31 | BDR2-FAB2 | Ethernet3 | 172.16.100.3/31 |
| BDR2-FAB2 | Ethernet1 | 198.18.251.53/31 | SPN1-FAB2 | Ethernet2 | 198.18.251.52/31 |
| BDR2-FAB2 | Ethernet2 | 198.18.251.55/31 | SPN2-FAB2 | Ethernet2 | 198.18.251.54/31 |
| DLF1-FAB1 | Ethernet1 | 198.18.249.25/31 | SPN1-FAB1 | Ethernet5 | 198.18.249.24/31 |
| DLF1-FAB1 | Ethernet2 | 198.18.249.27/31 | SPN2-FAB1 | Ethernet5 | 198.18.249.26/31 |
| DLF1-FAB2 | Ethernet1 | 198.18.251.65/31 | SPN1-FAB2 | Ethernet5 | 198.18.251.64/31 |
| DLF1-FAB2 | Ethernet2 | 198.18.251.67/31 | SPN2-FAB2 | Ethernet5 | 198.18.251.66/31 |
| DLF2-FAB1 | Ethernet1 | 198.18.249.29/31 | SPN1-FAB1 | Ethernet6 | 198.18.249.28/31 |
| DLF2-FAB1 | Ethernet2 | 198.18.249.31/31 | SPN2-FAB1 | Ethernet6 | 198.18.249.30/31 |
| DLF2-FAB2 | Ethernet1 | 198.18.251.69/31 | SPN1-FAB2 | Ethernet6 | 198.18.251.68/31 |
| DLF2-FAB2 | Ethernet2 | 198.18.251.71/31 | SPN2-FAB2 | Ethernet6 | 198.18.251.70/31 |
| DLF3-FAB1 | Ethernet1 | 198.18.249.33/31 | SPN1-FAB1 | Ethernet7 | 198.18.249.32/31 |
| DLF3-FAB1 | Ethernet2 | 198.18.249.35/31 | SPN2-FAB1 | Ethernet7 | 198.18.249.34/31 |
| DLF3-FAB2 | Ethernet1 | 198.18.251.73/31 | SPN1-FAB2 | Ethernet7 | 198.18.251.72/31 |
| DLF3-FAB2 | Ethernet2 | 198.18.251.75/31 | SPN2-FAB2 | Ethernet7 | 198.18.251.74/31 |
| DLF4-FAB1 | Ethernet1 | 198.18.249.37/31 | SPN1-FAB1 | Ethernet8 | 198.18.249.36/31 |
| DLF4-FAB1 | Ethernet2 | 198.18.249.39/31 | SPN2-FAB1 | Ethernet8 | 198.18.249.38/31 |
| DLF4-FAB2 | Ethernet1 | 198.18.251.77/31 | SPN1-FAB2 | Ethernet8 | 198.18.251.76/31 |
| DLF4-FAB2 | Ethernet2 | 198.18.251.79/31 | SPN2-FAB2 | Ethernet8 | 198.18.251.78/31 |
| SPN1-FAB1 | Ethernet3 | 198.18.249.16/31 | SVC1-FAB1 | Ethernet1 | 198.18.249.17/31 |
| SPN1-FAB1 | Ethernet4 | 198.18.249.20/31 | SVC2-FAB1 | Ethernet1 | 198.18.249.21/31 |
| SPN1-FAB2 | Ethernet3 | 198.18.251.56/31 | SVC1-FAB2 | Ethernet1 | 198.18.251.57/31 |
| SPN1-FAB2 | Ethernet4 | 198.18.251.60/31 | SVC2-FAB2 | Ethernet1 | 198.18.251.61/31 |
| SPN2-FAB1 | Ethernet3 | 198.18.249.18/31 | SVC1-FAB1 | Ethernet2 | 198.18.249.19/31 |
| SPN2-FAB1 | Ethernet4 | 198.18.249.22/31 | SVC2-FAB1 | Ethernet2 | 198.18.249.23/31 |
| SPN2-FAB2 | Ethernet3 | 198.18.251.58/31 | SVC1-FAB2 | Ethernet2 | 198.18.251.59/31 |
| SPN2-FAB2 | Ethernet4 | 198.18.251.62/31 | SVC2-FAB2 | Ethernet2 | 198.18.251.63/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 198.18.248.64/26 | 64 | 8 | 12.5 % |
| 198.18.248.224/27 | 32 | 2 | 6.25 % |
| 198.18.250.64/26 | 64 | 8 | 12.5 % |
| 198.18.250.224/27 | 32 | 2 | 6.25 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | BDR1-FAB1 | 198.18.248.69/32 |
| FABRIC | BDR1-FAB2 | 198.18.250.79/32 |
| FABRIC | BDR2-FAB1 | 198.18.248.70/32 |
| FABRIC | BDR2-FAB2 | 198.18.250.80/32 |
| FABRIC | DLF1-FAB1 | 198.18.248.73/32 |
| FABRIC | DLF1-FAB2 | 198.18.250.83/32 |
| FABRIC | DLF2-FAB1 | 198.18.248.74/32 |
| FABRIC | DLF2-FAB2 | 198.18.250.84/32 |
| FABRIC | DLF3-FAB1 | 198.18.248.75/32 |
| FABRIC | DLF3-FAB2 | 198.18.250.85/32 |
| FABRIC | DLF4-FAB1 | 198.18.248.76/32 |
| FABRIC | DLF4-FAB2 | 198.18.250.86/32 |
| FABRIC | SPN1-FAB1 | 198.18.248.225/32 |
| FABRIC | SPN1-FAB2 | 198.18.250.235/32 |
| FABRIC | SPN2-FAB1 | 198.18.248.226/32 |
| FABRIC | SPN2-FAB2 | 198.18.250.236/32 |
| FABRIC | SVC1-FAB1 | 198.18.248.71/32 |
| FABRIC | SVC1-FAB2 | 198.18.250.81/32 |
| FABRIC | SVC2-FAB1 | 198.18.248.72/32 |
| FABRIC | SVC2-FAB2 | 198.18.250.82/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 198.18.248.0/26 | 64 | 8 | 12.5 % |
| 198.18.250.0/26 | 64 | 8 | 12.5 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | BDR1-FAB1 | 198.18.248.5/32 |
| FABRIC | BDR1-FAB2 | 198.18.250.15/32 |
| FABRIC | BDR2-FAB1 | 198.18.248.5/32 |
| FABRIC | BDR2-FAB2 | 198.18.250.15/32 |
| FABRIC | DLF1-FAB1 | 198.18.248.9/32 |
| FABRIC | DLF1-FAB2 | 198.18.250.19/32 |
| FABRIC | DLF2-FAB1 | 198.18.248.9/32 |
| FABRIC | DLF2-FAB2 | 198.18.250.19/32 |
| FABRIC | DLF3-FAB1 | 198.18.248.11/32 |
| FABRIC | DLF3-FAB2 | 198.18.250.21/32 |
| FABRIC | DLF4-FAB1 | 198.18.248.11/32 |
| FABRIC | DLF4-FAB2 | 198.18.250.21/32 |
| FABRIC | SVC1-FAB1 | 198.18.248.7/32 |
| FABRIC | SVC1-FAB2 | 198.18.250.17/32 |
| FABRIC | SVC2-FAB1 | 198.18.248.7/32 |
| FABRIC | SVC2-FAB2 | 198.18.250.17/32 |

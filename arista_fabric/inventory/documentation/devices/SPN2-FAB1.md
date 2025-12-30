# SPN2-FAB1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | MGMT | 192.168.1.151/24 | - |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | OOB_MANAGEMENT | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description OOB_MANAGEMENT
   no shutdown
   vrf MGMT
   ip address 192.168.1.151/24
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | UNIX-Socket | Default Services |
| ---- | ----- | ----------- | ---------------- |
| False | True | - | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |
| cvpadmin | 15 | network-admin | False | - |
| gregg | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 <removed>
username cvpadmin privilege 15 role network-admin secret sha512 <removed>
username gregg privilege 15 role network-admin nopassword
```

### Enable Password

Enable password has been disabled

## Spanning Tree

### Spanning Tree Summary

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_BDR1-FAB1_Ethernet2 | - | 198.18.249.10/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_BDR2-FAB1_Ethernet2 | - | 198.18.249.14/31 | default | 1500 | False | - | - |
| Ethernet3 | P2P_SVC1-FAB1_Ethernet2 | - | 198.18.249.18/31 | default | 1500 | False | - | - |
| Ethernet4 | P2P_SVC2-FAB1_Ethernet2 | - | 198.18.249.22/31 | default | 1500 | False | - | - |
| Ethernet5 | P2P_DLF1-FAB1_Ethernet2 | - | 198.18.249.26/31 | default | 1500 | False | - | - |
| Ethernet6 | P2P_DLF2-FAB1_Ethernet2 | - | 198.18.249.30/31 | default | 1500 | False | - | - |
| Ethernet7 | P2P_DLF3-FAB1_Ethernet2 | - | 198.18.249.34/31 | default | 1500 | False | - | - |
| Ethernet8 | P2P_DLF4-FAB1_Ethernet2 | - | 198.18.249.38/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_BDR1-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.10/31
!
interface Ethernet2
   description P2P_BDR2-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.14/31
!
interface Ethernet3
   description P2P_SVC1-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.18/31
!
interface Ethernet4
   description P2P_SVC2-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.22/31
!
interface Ethernet5
   description P2P_DLF1-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.26/31
!
interface Ethernet6
   description P2P_DLF2-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.30/31
!
interface Ethernet7
   description P2P_DLF3-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.34/31
!
interface Ethernet8
   description P2P_DLF4-FAB1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.38/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 198.18.248.226/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 198.18.248.226/32
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | False |

#### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65100 | 198.18.248.226 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 198.18.248.69 | 65101 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.70 | 65101 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.71 | 65102 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.72 | 65102 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.73 | 65103 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.74 | 65103 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.75 | 65104 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.76 | 65104 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.249.11 | 65101 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.15 | 65101 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.19 | 65102 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.23 | 65102 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.27 | 65103 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.31 | 65103 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.35 | 65104 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.39 | 65104 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Peer-tag In | Peer-tag Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ----------- | ------------ | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True | - | - | - | - | default | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65100
   router-id 198.18.248.226
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 <removed>
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 <removed>
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 198.18.248.69 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.69 remote-as 65101
   neighbor 198.18.248.69 description BDR1-FAB1_Loopback0
   neighbor 198.18.248.70 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.70 remote-as 65101
   neighbor 198.18.248.70 description BDR2-FAB1_Loopback0
   neighbor 198.18.248.71 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.71 remote-as 65102
   neighbor 198.18.248.71 description SVC1-FAB1_Loopback0
   neighbor 198.18.248.72 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.72 remote-as 65102
   neighbor 198.18.248.72 description SVC2-FAB1_Loopback0
   neighbor 198.18.248.73 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.73 remote-as 65103
   neighbor 198.18.248.73 description DLF1-FAB1_Loopback0
   neighbor 198.18.248.74 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.74 remote-as 65103
   neighbor 198.18.248.74 description DLF2-FAB1_Loopback0
   neighbor 198.18.248.75 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.75 remote-as 65104
   neighbor 198.18.248.75 description DLF3-FAB1_Loopback0
   neighbor 198.18.248.76 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.76 remote-as 65104
   neighbor 198.18.248.76 description DLF4-FAB1_Loopback0
   neighbor 198.18.249.11 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.11 remote-as 65101
   neighbor 198.18.249.11 description BDR1-FAB1_Ethernet2
   neighbor 198.18.249.15 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.15 remote-as 65101
   neighbor 198.18.249.15 description BDR2-FAB1_Ethernet2
   neighbor 198.18.249.19 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.19 remote-as 65102
   neighbor 198.18.249.19 description SVC1-FAB1_Ethernet2
   neighbor 198.18.249.23 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.23 remote-as 65102
   neighbor 198.18.249.23 description SVC2-FAB1_Ethernet2
   neighbor 198.18.249.27 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.27 remote-as 65103
   neighbor 198.18.249.27 description DLF1-FAB1_Ethernet2
   neighbor 198.18.249.31 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.31 remote-as 65103
   neighbor 198.18.249.31 description DLF2-FAB1_Ethernet2
   neighbor 198.18.249.35 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.35 remote-as 65104
   neighbor 198.18.249.35 description DLF3-FAB1_Ethernet2
   neighbor 198.18.249.39 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.39 remote-as 65104
   neighbor 198.18.249.39 description DLF4-FAB1_Ethernet2
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 198.18.248.224/27 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 198.18.248.224/27 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

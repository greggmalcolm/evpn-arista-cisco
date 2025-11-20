# DLF1-FAB1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Virtual Source NAT](#virtual-source-nat)
  - [Virtual Source NAT Summary](#virtual-source-nat-summary)
  - [Virtual Source NAT Configuration](#virtual-source-nat-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | MGMT | 192.168.1.156/24 | - |

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
   ip address 192.168.1.156/24
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

## MLAG

### MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| DLF12-FAB1 | Vlan4094 | 198.18.248.141 | Port-Channel7 |

Dual primary detection is disabled.

### MLAG Device Configuration

```eos
!
mlag configuration
   domain-id DLF12-FAB1
   local-interface Vlan4094
   peer-address 198.18.248.141
   peer-link Port-Channel7
   reload-delay mlag 300
   reload-delay non-mlag 330
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **rapid-pvst**

#### Rapid-PVST Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 1-4094 | 4096 |

#### Global Spanning-Tree Settings

- Spanning Tree disabled for VLANs: **4093-4094**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode rapid-pvst
no spanning-tree vlan-id 4093-4094
spanning-tree vlan-id 1-4094 priority 4096
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

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 10 | VLAN10_PROD | - |
| 20 | VLAN20_PROD | - |
| 110 | VLAN110_DEV | - |
| 120 | VLAN120_DEV | - |
| 1100 | L2_VLAN1100 | - |
| 1110 | L2_VLAN1110 | - |
| 3009 | MLAG_L3_VRF_PROD | MLAG |
| 3010 | MLAG_L3_VRF_DEV | MLAG |
| 4093 | MLAG_L3 | MLAG |
| 4094 | MLAG | MLAG |

### VLANs Device Configuration

```eos
!
vlan 10
   name VLAN10_PROD
!
vlan 20
   name VLAN20_PROD
!
vlan 110
   name VLAN110_DEV
!
vlan 120
   name VLAN120_DEV
!
vlan 1100
   name L2_VLAN1100
!
vlan 1110
   name L2_VLAN1110
!
vlan 3009
   name MLAG_L3_VRF_PROD
   trunk group MLAG
!
vlan 3010
   name MLAG_L3_VRF_DEV
   trunk group MLAG
!
vlan 4093
   name MLAG_L3
   trunk group MLAG
!
vlan 4094
   name MLAG
   trunk group MLAG
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet3 | ROUTER_Testpoint1_G0/0 | *trunk | *10,20,1100,1110 | *4092 | *- | 3 |
| Ethernet7 | MLAG_DLF2-FAB1_Ethernet7 | *trunk | *- | *- | *MLAG | 7 |
| Ethernet8 | MLAG_DLF2-FAB1_Ethernet8 | *trunk | *- | *- | *MLAG | 7 |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_SPN1-FAB1_Ethernet5 | - | 198.18.249.25/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_SPN2-FAB1_Ethernet5 | - | 198.18.249.27/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_SPN1-FAB1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.25/31
!
interface Ethernet2
   description P2P_SPN2-FAB1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 198.18.249.27/31
!
interface Ethernet3
   description ROUTER_Testpoint1_G0/0
   no shutdown
   channel-group 3 mode active
!
interface Ethernet7
   description MLAG_DLF2-FAB1_Ethernet7
   no shutdown
   channel-group 7 mode active
!
interface Ethernet8
   description MLAG_DLF2-FAB1_Ethernet8
   no shutdown
   channel-group 7 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel3 | PortChannel Testpoint190 | trunk | 10,20,1100,1110 | 4092 | - | - | - | 3 | - |
| Port-Channel7 | MLAG_DLF2-FAB1_Port-Channel7 | trunk | - | - | MLAG | - | - | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel3
   description PortChannel Testpoint190
   no shutdown
   switchport trunk native vlan 4092
   switchport trunk allowed vlan 10,20,1100,1110
   switchport mode trunk
   switchport
   mlag 3
   spanning-tree portfast
!
interface Port-Channel7
   description MLAG_DLF2-FAB1_Port-Channel7
   no shutdown
   switchport mode trunk
   switchport trunk group MLAG
   switchport
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 198.18.248.73/32 |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | 198.18.248.9/32 |
| Loopback10 | DIAG_VRF_PROD | PROD | 10.255.255.9/32 |
| Loopback11 | DIAG_VRF_DEV | DEV | 10.255.255.41/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | - |
| Loopback10 | DIAG_VRF_PROD | PROD | - |
| Loopback11 | DIAG_VRF_DEV | DEV | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 198.18.248.73/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   no shutdown
   ip address 198.18.248.9/32
!
interface Loopback10
   description DIAG_VRF_PROD
   no shutdown
   vrf PROD
   ip address 10.255.255.9/32
!
interface Loopback11
   description DIAG_VRF_DEV
   no shutdown
   vrf DEV
   ip address 10.255.255.41/32
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan10 | VLAN10_PROD | PROD | - | False |
| Vlan20 | VLAN20_PROD | PROD | - | False |
| Vlan110 | VLAN110_DEV | DEV | - | False |
| Vlan120 | VLAN120_DEV | DEV | - | False |
| Vlan3009 | MLAG_L3_VRF_PROD | PROD | 1500 | False |
| Vlan3010 | MLAG_L3_VRF_DEV | DEV | 1500 | False |
| Vlan4093 | MLAG_L3 | default | 1500 | False |
| Vlan4094 | MLAG | default | 1500 | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan10 |  PROD  |  -  |  10.1.10.1/24  |  -  |  -  |  -  |
| Vlan20 |  PROD  |  -  |  10.1.20.1/24  |  -  |  -  |  -  |
| Vlan110 |  DEV  |  -  |  10.1.110.1/24  |  -  |  -  |  -  |
| Vlan120 |  DEV  |  -  |  10.1.120.1/24  |  -  |  -  |  -  |
| Vlan3009 |  PROD  |  198.18.248.204/31  |  -  |  -  |  -  |  -  |
| Vlan3010 |  DEV  |  198.18.248.204/31  |  -  |  -  |  -  |  -  |
| Vlan4093 |  default  |  198.18.248.204/31  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  198.18.248.140/31  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan10
   description VLAN10_PROD
   no shutdown
   vrf PROD
   ip address virtual 10.1.10.1/24
!
interface Vlan20
   description VLAN20_PROD
   no shutdown
   vrf PROD
   ip address virtual 10.1.20.1/24
!
interface Vlan110
   description VLAN110_DEV
   no shutdown
   vrf DEV
   ip address virtual 10.1.110.1/24
!
interface Vlan120
   description VLAN120_DEV
   no shutdown
   vrf DEV
   ip address virtual 10.1.120.1/24
!
interface Vlan3009
   description MLAG_L3_VRF_PROD
   no shutdown
   mtu 1500
   vrf PROD
   ip address 198.18.248.204/31
!
interface Vlan3010
   description MLAG_L3_VRF_DEV
   no shutdown
   mtu 1500
   vrf DEV
   ip address 198.18.248.204/31
!
interface Vlan4093
   description MLAG_L3
   no shutdown
   mtu 1500
   ip address 198.18.248.204/31
!
interface Vlan4094
   description MLAG
   no shutdown
   mtu 1500
   no autostate
   ip address 198.18.248.140/31
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Loopback1 |
| UDP port | 4789 |
| EVPN MLAG Shared Router MAC | mlag-system-id |

##### VLAN to VNI, Flood List and Multicast Group Mappings

| VLAN | VNI | Flood List | Multicast Group |
| ---- | --- | ---------- | --------------- |
| 10 | 10010 | - | - |
| 20 | 10020 | - | - |
| 110 | 10110 | - | - |
| 120 | 10120 | - | - |
| 1100 | 11100 | - | - |
| 1110 | 11110 | - | - |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Overlay Multicast Group to Encap Mappings |
| --- | --- | ----------------------------------------- |
| DEV | 11 | - |
| PROD | 10 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description DLF1-FAB1_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 10 vni 10010
   vxlan vlan 20 vni 10020
   vxlan vlan 110 vni 10110
   vxlan vlan 120 vni 10120
   vxlan vlan 1100 vni 11100
   vxlan vlan 1110 vni 11110
   vxlan vrf DEV vni 11
   vxlan vrf PROD vni 10
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### Virtual Router MAC Address

#### Virtual Router MAC Address Summary

Virtual Router MAC Address: 00:1c:73:00:00:99

#### Virtual Router MAC Address Device Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:00:99
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| DEV | True |
| MGMT | False |
| PROD | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf DEV
no ip routing vrf MGMT
ip routing vrf PROD
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| DEV | false |
| MGMT | false |
| PROD | false |

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65103 | 198.18.248.73 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
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

##### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65103 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 198.18.248.205 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - | - | - | - | - |
| 198.18.248.225 | 65100 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.248.226 | 65100 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 198.18.249.24 | 65100 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.249.26 | 65100 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 198.18.248.205 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | DEV | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - | - | - | - | - |
| 198.18.248.205 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | PROD | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Peer-tag In | Peer-tag Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ----------- | ------------ | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True | - | - | - | - | default | - |

#### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 10 | 198.18.248.73:10010 | 10010:10010 | - | - | learned |
| 20 | 198.18.248.73:10020 | 10020:10020 | - | - | learned |
| 110 | 198.18.248.73:10110 | 10110:10110 | - | - | learned |
| 120 | 198.18.248.73:10120 | 10120:10120 | - | - | learned |
| 1100 | 198.18.248.73:11100 | 11100:11100 | - | - | learned |
| 1110 | 198.18.248.73:11110 | 11110:11110 | - | - | learned |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute | Graceful Restart |
| --- | ------------------- | ------------ | ---------------- |
| DEV | 198.18.248.73:11 | connected | - |
| PROD | 198.18.248.73:10 | connected | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65103
   router-id 198.18.248.73
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
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
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65103
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER description DLF2-FAB1
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 <removed>
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor 198.18.248.205 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 198.18.248.205 description DLF2-FAB1_Vlan4093
   neighbor 198.18.248.225 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.225 remote-as 65100
   neighbor 198.18.248.225 description SPN1-FAB1_Loopback0
   neighbor 198.18.248.226 peer group EVPN-OVERLAY-PEERS
   neighbor 198.18.248.226 remote-as 65100
   neighbor 198.18.248.226 description SPN2-FAB1_Loopback0
   neighbor 198.18.249.24 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.24 remote-as 65100
   neighbor 198.18.249.24 description SPN1-FAB1_Ethernet5
   neighbor 198.18.249.26 peer group IPv4-UNDERLAY-PEERS
   neighbor 198.18.249.26 remote-as 65100
   neighbor 198.18.249.26 description SPN2-FAB1_Ethernet5
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 10
      rd 198.18.248.73:10010
      route-target both 10010:10010
      redistribute learned
   !
   vlan 20
      rd 198.18.248.73:10020
      route-target both 10020:10020
      redistribute learned
   !
   vlan 110
      rd 198.18.248.73:10110
      route-target both 10110:10110
      redistribute learned
   !
   vlan 120
      rd 198.18.248.73:10120
      route-target both 10120:10120
      redistribute learned
   !
   vlan 1100
      rd 198.18.248.73:11100
      route-target both 11100:11100
      redistribute learned
   !
   vlan 1110
      rd 198.18.248.73:11110
      route-target both 11110:11110
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf DEV
      rd 198.18.248.73:11
      route-target import evpn 11:11
      route-target export evpn 11:11
      router-id 198.18.248.73
      neighbor 198.18.248.205 peer group MLAG-IPv4-UNDERLAY-PEER
      neighbor 198.18.248.205 description DLF2-FAB1_Vlan3010
      redistribute connected route-map RM-CONN-2-BGP-VRFS
   !
   vrf PROD
      rd 198.18.248.73:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 198.18.248.73
      neighbor 198.18.248.205 peer group MLAG-IPv4-UNDERLAY-PEER
      neighbor 198.18.248.205 description DLF2-FAB1_Vlan3009
      redistribute connected route-map RM-CONN-2-BGP-VRFS
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

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 198.18.248.64/26 eq 32 |
| 20 | permit 198.18.248.0/26 eq 32 |

##### PL-MLAG-PEER-VRFS

| Sequence | Action |
| -------- | ------ |
| 10 | permit 198.18.248.204/31 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 198.18.248.64/26 eq 32
   seq 20 permit 198.18.248.0/26 eq 32
!
ip prefix-list PL-MLAG-PEER-VRFS
   seq 10 permit 198.18.248.204/31
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

##### RM-CONN-2-BGP-VRFS

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | deny | ip address prefix-list PL-MLAG-PEER-VRFS | - | - | - |
| 20 | permit | - | - | - | - |

##### RM-MLAG-PEER-IN

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | - | origin incomplete | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-CONN-2-BGP-VRFS deny 10
   match ip address prefix-list PL-MLAG-PEER-VRFS
!
route-map RM-CONN-2-BGP-VRFS permit 20
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| DEV | enabled |
| MGMT | disabled |
| PROD | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance DEV
!
vrf instance MGMT
!
vrf instance PROD
```

## Virtual Source NAT

### Virtual Source NAT Summary

| Source NAT VRF | Source NAT IPv4 Address | Source NAT IPv6 Address |
| -------------- | ----------------------- | ----------------------- |
| DEV | 10.255.255.41 | - |
| PROD | 10.255.255.9 | - |

### Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf DEV address 10.255.255.41
ip address virtual source-nat vrf PROD address 10.255.255.9
```

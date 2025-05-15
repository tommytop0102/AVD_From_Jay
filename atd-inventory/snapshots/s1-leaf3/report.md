# s1-leaf3 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            up             up                 MLAG_PEER_s1-leaf4_Ethernet1
Et2                            up             up                 P2P_LINK_TO_S1-SPINE1_Ethernet4
Et3                            up             up                 P2P_LINK_TO_S1-SPINE2_Ethernet4
Et4                            up             up                 Routed_Interface_4
Et6                            up             up                 MLAG_PEER_s1-leaf4_Ethernet6
Lo0                            up             up                 EVPN_Overlay_Peering
Lo1                            up             up                 VTEP_VXLAN_Tunnel_Source
Lo100                          up             up                 bluevrf_VTEP_DIAGNOSTICS
Ma0                            up             up                 oob_management
Po1                            up             up                 MLAG_PEER_s1-leaf4_Po1
Vl1199                         up             up                 
Vl2300                         up             up                 bluenet1
Vl2301                         up             up                 bluenet2
Vl3099                         up             up                 MLAG_PEER_L3_iBGP: vrf bluevrf
Vl4093                         up             up                 MLAG_PEER_L3_PEERING
Vl4094                         up             up                 MLAG_PEER
Vx1                            up             up                 s1-leaf3_VTEP
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------ ---------- -------
Ethernet2       192.168.51.9/31      up         up              1500           
Ethernet3       192.168.51.11/31     up         up              1500           
Ethernet4       10.192.195.21/24     up         up              9000           
Loopback0       192.168.246.5/32     up         up             65535           
Loopback1       192.168.236.5/32     up         up             65535           
Loopback100     10.255.1.5/32        up         up             65535           
Management0     192.168.0.14/24      up         up              1500           
Vlan1199        unassigned           up         up              9164           
Vlan2300        192.168.11.1/24      up         up              1500           
Vlan2301        192.168.12.1/24      up         up              1500           
Vlan3099        10.255.251.4/31      up         up              1500           
Vlan4093        10.255.251.4/31      up         up              1500           
Vlan4094        10.255.252.4/31      up         up              1500
```
## show lldp neighbors

```
Last table change time   : 0:00:28 ago
Number of table inserts  : 5
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port          Neighbor Device ID          Neighbor Port ID    TTL
---------- --------------------------- ---------------------- ---
Et1           s1-leaf4.tsmc.com.tw        Ethernet1           120
Et2           s1-spine1.tsmc.com.tw       Ethernet4           120
Et3           s1-spine2.tsmc.com.tw       Ethernet4           120
Et4           s1-host2.atd.lab            Ethernet1           120
Et6           s1-leaf4.tsmc.com.tw        Ethernet6           120
```
## show running-config

```
! Command: show running-config
! device: s1-leaf3 (cEOSLab, EOS-4.32.1F-37313256.4321F (engineering build))
!
no aaa root
!
username admin privilege 15 role network-admin secret 5 $1$5O85YVVn$HrXcfOivJEnISTMb6xrJc.
username arista privilege 15 role network-admin secret 5 $1$4VjIjfd1$XkUVulbNDESHFzcxDU.Tk1
username arista ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCjyBFJuXUDRPFV6eLHPBCYZ/YWyonAJxi5H6Hk2yEr50NgOkjt0KGaCnk13lHTc+fUqO2dW2luCSWYey3G2V9I7oTu/OlnJ8upatCJ+U7dfEceUFBAUpPLA89ZOa9OJ8R0wN7l8tD8eGUt52kIn2KKJh4fd8tytgD9oN6QL/WvqjfpC2Ha2ibWq7N71yKMm4akBJ8rvyTAoXFRu0Yp1Shrx461BNYWcs+b7aOyWcyp2xy3u17idBGRh2nsK/N4kVnPGLBZYQ6RcAL9l7MtWPh71ce/IW38IFL0mp/PTz/J8POo2+1ZKcPABbFobi+t397P9C0S/EgY6ppvAOxD+c+3 arista@tsmc-test-2-1-4a9cb9a9-eos
username test-admin privilege 15 role network-admin secret sha512 $6$7GTxsrRjnwheeKfR$zhJ8qycVjAJz41rf5JRSfWIzp93IL5WL7sMS/Taz1yfShz.MAnoajCf7R2n1/EZW7PN5QA3Huayl0lVQesBYN1
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvcompression=gzip -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -cvaddr=192.168.0.5:9910 -cvauth=token,/tmp/token -cvvrf=default -taillogs -disableaaa
   no shutdown
!
vlan internal order ascending range 1006 1199
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname s1-leaf3
ip name-server vrf default 8.8.8.8
ip name-server vrf default 192.168.2.1
dns domain tsmc.com.tw
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 16384
!
system l1
   unsupported speed action error
   unsupported error-correction action error
!
vlan 20
   name ExternalNetwork
!
vlan 2300
   name bluenet1
!
vlan 2301
   name bluenet2
!
vlan 3099
   name MLAG_iBGP_bluevrf
   trunk group LEAF_PEER_L3
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
!
vrf instance bluevrf
!
management api http-commands
   no shutdown
   !
   vrf default
      no shutdown
!
radius-server host 192.168.0.1 key 7 0207165218120E
!
aaa group server radius atds
   server 192.168.0.1
!
aaa authentication login default group atds local
aaa authorization exec default group atds local
aaa authorization commands all default local
!
interface Port-Channel1
   description MLAG_PEER_s1-leaf4_Po1
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
!
interface Ethernet1
   description MLAG_PEER_s1-leaf4_Ethernet1
   channel-group 1 mode active
!
interface Ethernet2
   description P2P_LINK_TO_S1-SPINE1_Ethernet4
   mtu 1500
   no switchport
   ip address 192.168.51.9/31
!
interface Ethernet3
   description P2P_LINK_TO_S1-SPINE2_Ethernet4
   mtu 1500
   no switchport
   ip address 192.168.51.11/31
!
interface Ethernet4
   description Routed_Interface_4
   mtu 9000
   no switchport
   vrf bluevrf
   ip address 10.192.195.21/24
!
interface Ethernet6
   description MLAG_PEER_s1-leaf4_Ethernet6
   channel-group 1 mode active
!
interface Loopback0
   description EVPN_Overlay_Peering
   ip address 192.168.246.5/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   ip address 192.168.236.5/32
!
interface Loopback100
   description bluevrf_VTEP_DIAGNOSTICS
   vrf bluevrf
   ip address 10.255.1.5/32
!
interface Management0
   description OOB_MANAGEMENT
   description oob_management
   ip address 192.168.0.14/24
!
interface Vlan2300
   description bluenet1
   vrf bluevrf
   ip address virtual 192.168.11.1/24
!
interface Vlan2301
   description bluenet2
   vrf bluevrf
   ip address virtual 192.168.12.1/24
!
interface Vlan3099
   description MLAG_PEER_L3_iBGP: vrf bluevrf
   mtu 1500
   vrf bluevrf
   ip address 10.255.251.4/31
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   mtu 1500
   ip address 10.255.251.4/31
!
interface Vlan4094
   description MLAG_PEER
   mtu 1500
   no autostate
   ip address 10.255.252.4/31
!
interface Vxlan1
   description s1-leaf3_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 20 vni 30002
   vxlan vlan 2300 vni 32300
   vxlan vlan 2301 vni 32301
   vxlan vrf bluevrf vni 100
!
ip virtual-router mac-address 02:04:02:04:02:04
ip address virtual source-nat vrf bluevrf address 10.255.1.5
!
ip routing
ip routing vrf bluevrf
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.246.0/24 eq 32
   seq 20 permit 192.168.236.0/24 eq 32
!
mlag configuration
   domain-id pod2
   local-interface Vlan4094
   peer-address 10.255.252.5
   peer-link Port-Channel1
   reload-delay mlag 300
   reload-delay non-mlag 330
!
ip route 0.0.0.0/0 192.168.0.1
!
ntp server 192.168.0.1 iburst source Management0
ntp server time.google.com prefer iburst
!
ip radius source-interface Management0
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
!
router bgp 65102
   router-id 192.168.246.5
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65102
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER description s1-leaf4
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 10.255.251.5 description s1-leaf4
   neighbor 192.168.51.8 peer group IPv4-UNDERLAY-PEERS
   neighbor 192.168.51.8 remote-as 64999
   neighbor 192.168.51.8 description s1-spine1_Ethernet4
   neighbor 192.168.51.10 peer group IPv4-UNDERLAY-PEERS
   neighbor 192.168.51.10 remote-as 64999
   neighbor 192.168.51.10 description s1-spine2_Ethernet4
   neighbor 192.168.246.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.246.1 remote-as 64999
   neighbor 192.168.246.1 description s1-spine1
   neighbor 192.168.246.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.246.2 remote-as 64999
   neighbor 192.168.246.2 description s1-spine2
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan-aware-bundle ExternalNetwork
      rd 192.168.246.5:30002
      route-target both 30002:30002
      redistribute learned
      vlan 20
   !
   vlan-aware-bundle bluevrf
      rd 192.168.246.5:100
      route-target both 100:100
      redistribute learned
      vlan 2300-2301
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf bluevrf
      rd 192.168.246.5:100
      route-target import evpn 100:100
      route-target export evpn 100:100
      router-id 192.168.246.5
      neighbor 10.255.251.5 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
!
router multicast
   ipv4
      routing
      software-forwarding sfe
!
end
```
## show version

```
Arista cEOSLab
Hardware version: 
Serial number: s1-leaf3
Hardware MAC address: 001c.73c0.c614
System MAC address: 001c.73c0.c614

Software image version: 4.32.1F-37313256.4321F (engineering build)
Architecture: i686
Internal build version: 4.32.1F-37313256.4321F
Internal build ID: 7a617a29-3c49-4a05-bc51-0bd347da9799
Image format version: 1.0
Image optimization: None

Kernel version: 5.14.0-503.21.1.el9_5.x86_64

Uptime: 30 minutes
Total memory: 49062216 kB
Free memory: 2322380 kB
```

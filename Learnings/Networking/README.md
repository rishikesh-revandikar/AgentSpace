# Networking

Notes for the roadmap below, grouped by what you are trying to learn. Watch the video linked in the note, then read the note and the article. Each note has a diagram, a worked example, and a short self-check.

Days 1–17 of Jeremy’s IT Lab are the early fundamentals, LAN switching, and static routing notes. The later fundamentals (DHCP, DNS, TCP reliability, wireless) and the campus services (EtherChannel, Layer 2 security, gateway redundancy, ACLs, NAT, policy, multicast, tunnels) sit in the same folders, because the service-provider notes assume them. OSPF through YANG is the rest of the roadmap.

## Find a note by the failure in front of you

| What you are looking at | Open |
|-------------------------|------|
| No address, 169.254.x.x, or a name that will not resolve | [DHCP and DNS](01-fundamentals/16-dhcp-and-dns.md) |
| A transfer hangs and a small ping works | [MTU and tunnels](03-routing/12-mtu-and-tunnels.md) |
| Ping works one way | [Static routing](03-routing/01-static-routing.md), then [life of a packet](03-routing/02-life-of-a-packet.md) |
| Two VLANs, no ping between them | [Trunks and router on a stick](02-lan-switching/02-vlans-trunks-and-roas.md) |
| A new switch erased the VLAN database | [VLANs](02-lan-switching/01-vlans-access-ports.md) (VTP section) |
| A broadcast storm, or the root bridge is an access switch | [Spanning tree](02-lan-switching/03-spanning-tree.md) |
| A second cable is idle | [EtherChannel](02-lan-switching/04-etherchannel.md) |
| The gateway router died and the PCs still point at it | [Gateway redundancy](03-routing/07-gateway-redundancy.md) |
| A desk port is offering DHCP or answering ARP | [Layer 2 security](02-lan-switching/05-layer2-security.md) |
| OSPF neighbor missing, or the wrong area | [OSPF](03-routing/03-ospf.md) |
| BGP stays Active, or the exit is the wrong one | [BGP](03-routing/05-bgp.md) and [TCP reliability](01-fundamentals/17-tcp-reliability.md) |
| The route exists in the wrong protocol, or a customer leaked prefixes | [Routing policy](03-routing/10-routing-policy.md) |
| Private addresses need to reach the Internet | [NAT](03-routing/09-nat.md) |
| OSPF hellos, or a stream nobody joined | [Multicast](03-routing/11-multicast.md) |
| Customer routes, and you do not want them in the core | [MPLS](04-mpls/01-architecture-ldp-and-labels.md), then [L3VPN](05-vpn-services/01-l3vpn.md) |
| The VPN route is in BGP and traffic is blackholed | [RIB, FIB, and LFIB](07-forwarding/01-rib-fib-lfib.md) and the L3VPN note |

Playlist for the CCNA days: [Free CCNA v1.1](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ).

## How to use the roadmap

| Approach | Detail |
|----------|--------|
| Order | Follow the phase numbers. VRF, BGP, and MPLS come before L3VPN. |
| Depth | One video and one article per topic, then the note in this folder. Add a lab when you will configure it. |
| Labs | Packet Tracer for the CCNA notes. EVE-NG, GNS3, or a virtual router (IOS-XR, Junos, Nokia vSIM) after that. |
| Paid, optional | [NetworkLessons MPLS](https://networklessons.com/mpls) covers LDP through L3VPN to traffic engineering in one subscription. |

## 01 — Fundamentals

| Note | Roadmap topic |
|------|----------------|
| [Network devices](01-fundamentals/01-network-devices.md) | What switches, routers, and firewalls each stop |
| [Interfaces and cables](01-fundamentals/02-interfaces-and-cables.md) | Copper, fiber, PoE |
| [TCP/IP model](01-fundamentals/03-tcp-ip-model.md) | OSI, encapsulation, ports. [Kurose videos](https://gaia.cs.umass.edu/kurose_ross/videos/1/) |
| [Command line](01-fundamentals/04-command-line.md) | IOS modes and saving a config |
| [Ethernet switching, part 1](01-fundamentals/05-ethernet-switching-1.md) | Frames and the MAC table |
| [Ethernet switching, part 2](01-fundamentals/06-ethernet-switching-2.md) | ARP |
| [IPv4 addressing, part 1](01-fundamentals/07-ipv4-addressing-1.md) | Masks, classes, private ranges |
| [IPv4 addressing, part 2](01-fundamentals/08-ipv4-addressing-2.md) | Addresses on interfaces |
| [Switch interfaces](01-fundamentals/09-switch-interfaces.md) | Speed, duplex, errors |
| [IPv4 header](01-fundamentals/10-ipv4-header.md) | TTL, fragmentation. [Wireshark Learn](https://www.wireshark.org/learn) |
| [Wireshark](01-fundamentals/11-wireshark.md) | Capture filters and a real ping |
| [Subnetting, part 1](01-fundamentals/12-subnetting-1.md) | Equal blocks inside a /24 |
| [Subnetting, part 2](01-fundamentals/13-subnetting-2.md) | Masks that cross octets |
| [VLSM](01-fundamentals/14-subnetting-vlsm.md) | Different sizes from one block |
| [IPv6](01-fundamentals/15-ipv6.md) | Address types, NDP, SLAAC |
| [DHCP and DNS](01-fundamentals/16-dhcp-and-dns.md) | DORA, relay, and how a name becomes an address |
| [TCP reliability](01-fundamentals/17-tcp-reliability.md) | Sequence numbers, windows, loss, MSS |
| [Wireless](01-fundamentals/18-wireless.md) | Association, channels, and the VLAN the SSID lands in |

## 02 — LAN switching

| Note | Roadmap topic |
|------|----------------|
| [VLANs, access ports](02-lan-switching/01-vlans-access-ports.md) | One broadcast domain per VLAN |
| [Trunks and router on a stick](02-lan-switching/02-vlans-trunks-and-roas.md) | 802.1Q and inter-VLAN routing |
| [Spanning tree](02-lan-switching/03-spanning-tree.md) | Loops, RSTP, root bridge |
| [EtherChannel](02-lan-switching/04-etherchannel.md) | LACP, and why both cables can forward |
| [Layer 2 security](02-lan-switching/05-layer2-security.md) | Port security, DHCP snooping, DAI |

## 03 — Routing

| Note | Roadmap topic |
|------|----------------|
| [Static routing](03-routing/01-static-routing.md) | RIB, longest match, static and default routes |
| [Life of a packet](03-routing/02-life-of-a-packet.md) | [Packet Traveling](https://www.youtube.com/watch?v=rYodcvhh7b8) |
| [OSPF](03-routing/03-ospf.md) | Areas, DR, LSAs. [Jeremy’s notes](https://www.jeremysitlab.com/ccna-resources/) |
| [IS-IS](03-routing/04-is-is.md) | Levels, NET, TLVs. [31-minute intro](https://www.youtube.com/watch?v=jWdD8SCwzHk) |
| [BGP](03-routing/05-bgp.md) | [Keith Barker playlist](https://www.youtube.com/playlist?list=PLwQhJUHSLJFUO5YzFH2wveh2zcHUKj11w), [how a path is chosen](https://www.practicalnetworking.net/stand-alone/bgp-oldest-path/) |
| [VRF](03-routing/06-vrf.md) | Separate tables, RD versus RT |
| [Gateway redundancy](03-routing/07-gateway-redundancy.md) | HSRP and VRRP, the virtual default gateway |
| [Access lists](03-routing/08-acls.md) | First match, implicit deny, direction |
| [NAT](03-routing/09-nat.md) | Inside local and global, PAT |
| [Routing policy](03-routing/10-routing-policy.md) | Prefix-lists, route-maps, redistribution |
| [Multicast](03-routing/11-multicast.md) | IGMP, PIM sparse, RPF |
| [MTU and tunnels](03-routing/12-mtu-and-tunnels.md) | PMTUD, GRE, and the bytes MPLS and VXLAN add |

## 04 — MPLS

| Note | Roadmap topic |
|------|----------------|
| [Architecture, LDP, and labels](04-mpls/01-architecture-ldp-and-labels.md) | Push, swap, pop, PHP. [RFC 3031](https://datatracker.ietf.org/doc/rfc3031/), [What is MPLS?](https://networklessons.com/mpls) |

## 05 — VPN services

| Note | Roadmap topic |
|------|----------------|
| [L3VPN](05-vpn-services/01-l3vpn.md) | [RFC 4364](https://datatracker.ietf.org/doc/rfc4364/), [RD vs RT PDF](https://www.sunsetlearning.com/wp-content/uploads/2016/11/L3VPNs-route-target-and-route-distinguisher-Part-1.pdf) |
| [PE-CE routing](05-vpn-services/02-pe-ce-routing.md) | [PE-CE OSPF](https://networklessons.com/mpls/mpls-layer-3-vpn-pe-ce-ospf) |
| [L2VPN, pseudowire, VPLS](05-vpn-services/03-l2vpn-vpls.md) | [AToM and pseudowire](https://networklessons.com/tag/ldp) |
| [EVPN](05-vpn-services/04-evpn.md) | [Juniper primer](https://www.juniper.net/documentation/en_US/day-one-books/topics/topic-map/evpn-primer.html), [Cisco EVPN PDF](https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000/evpn/evpn-config-cisco8000/fundamentals-and-core-features-of-evpn.pdf) |

## 06 — Traffic engineering

| Note | Roadmap topic |
|------|----------------|
| [RSVP-TE](06-traffic-engineering/01-rsvp-te.md) | [RFC 3209](https://datatracker.ietf.org/doc/html/rfc3209), [operation video](https://www.youtube.com/watch?v=LzkKaRATJyw) |
| [SR-MPLS](06-traffic-engineering/02-sr-mpls.md) | [RFC 8402](https://datatracker.ietf.org/doc/html/rfc8402), [Cisco Community intro](https://community.cisco.com/t5/video/gallerypage/video-id/6064655138001) |
| [SRv6](06-traffic-engineering/03-srv6.md) | [Explained](https://www.youtube.com/watch?v=c24v8CUDvzI), RFC 8986 |

## 07 — Forwarding

| Note | Roadmap topic |
|------|----------------|
| [RIB, FIB, and LFIB](07-forwarding/01-rib-fib-lfib.md) | Control plane versus the tables that actually forward |

## 08 — Operations

| Note | Roadmap topic |
|------|----------------|
| [QoS](08-operations/01-qos.md) | DiffServ, pipe mode, policing versus shaping |
| [High availability](08-operations/02-high-availability.md) | BFD, graceful restart, NSR |
| [Troubleshooting](08-operations/03-troubleshooting.md) | A repeatable L3VPN checklist |

## 09 — Automation

| Note | Roadmap topic |
|------|----------------|
| [YANG, NETCONF, RESTCONF, gNMI](09-automation/01-yang-netconf-gnmi.md) | [DevNet series](https://developer.cisco.com/video/net-prog-basics/00-intro/intro/), [course labs](https://github.com/CiscoDevNet/netprog_basics) |

## Phase sources still worth opening

These are the external pieces the notes cite, kept here so a phase can be studied even before the note.

**Foundations.** [Kurose chapter videos](https://gaia.cs.umass.edu/kurose_ross/videos/1/). [Jeremy CCNA](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) or [Keith Barker CCNA](https://www.youtube.com/playlist?list=PLQQoSBmrXmrysEaVNia7KVwf85qATIi1V). [Packet Traveling](https://www.practicalnetworking.net/series/packet-traveling/packet-traveling/) and the [finale](https://www.practicalnetworking.net/series/packet-traveling/packet-traveling-series-finale/). [Wireshark for beginners](https://www.youtube.com/playlist?list=PL6gx4Cwl9DGBI2ZFuyZOl5Q7sptR7PwYN).

**Routing.** [JNCIS-SP](https://learningportal.juniper.net/juniper/user_activity_info.aspx?id=EDU-JUN-WBT-JOL-JNCIS-SP) for IS-IS and OSPF. [Orhan Ergun](https://www.youtube.com/@OrhanErgunCCDE) for VRF.

**MPLS.** [LDP articles](https://networklessons.com/tag/ldp). [Keith Barker, advanced MPLS](https://www.youtube.com/watch?v=jE--F6GRCTg). [CBT Nuggets preview](https://www.cbtnuggets.com/it-training/skills/describe-mpls-operations). [Nokia MPLS syllabus](https://www.nokia.com/networks/training/src/courses/mpls/).

**VPNs.** [Keith Barker L3VPN](https://www.fiberopticvideos.com/watch.php?vid=1c115ba28). [Cisco Live on-demand](https://www.ciscolive.com/on-demand/on-demand-library.html?search=The+CCIE+Candidate%27s+Introduction+to+MPLS+L3VPN+Networks). [Juniper RD and RT](https://www.juniper.net/documentation/us/en/software/junos/multicast/topics/concept/ng-mvpn-concepts-terminology.html). [Why EVPN](https://www.networkingvideos.com/watch.php?vid=3c3d3abfe). [EVPN-VXLAN architecture](https://www.youtube.com/watch?v=EBjPve8AmR4). [VXLAN encapsulation](https://www.juniper.net/documentation/us/en/software/junos/evpn/topics/concept/evpn-vxlan-data-plane-encapsulation.html). Nokia VPLS sits in the [SRC catalog](https://www.nokia.com/networks/training/src/self-paced/).

**Traffic engineering.** [RSVP-TE article](https://networklessons.com/mpls/mpls-te-rsvp-te). [Explicit tunnel](https://www.youtube.com/watch?v=X8aVxnbJOVw). [SR lab](https://community.cisco.com/t5/service-providers-knowledge-base/cisco-mpls-segment-routing-introduction-lab-v1-is-now-available/ta-p/3636002). [SR community live](https://community.cisco.com/t5/videos-service-provider/video-introducci%C3%B3n-a-segment-routing/ba-p/5288954).

**Operations.** Nokia NRS II prep videos, including MPLS FRR, are linked from [SRC self-paced training](https://www.nokia.com/networks/training/src/self-paced/). Use the HA guide for the platform you actually ship.

**Automation.** [YANG playlist](https://www.youtube.com/playlist?list=PLpGt4hh32rCp_ocLmYAKlf3q3TqSJl6Mh). [Bombal and Preston](https://davidbombal.com/yang-netconf-restconf-demos-which-cisco-devices-are-supported-part-1/).

## Shortest path through the notes

```text
1. Fundamentals, through DHCP/DNS and TCP. Wireless when you touch an AP.
2. Life of a packet, then LAN switching: VLANs, STP, EtherChannel, Layer 2 security
3. Static routing, gateway redundancy, ACLs, NAT
4. OSPF and IS-IS. Multicast once OSPF’s groups are familiar.
5. BGP, routing policy, VRF
6. MTU and tunnels, then MPLS
7. L3VPN, PE-CE, L2VPN, EVPN
8. RSVP-TE, then SR-MPLS. SRv6 only if the product needs it
9. RIB/FIB/LFIB, QoS, HA, the troubleshooting checklist
10. YANG / NETCONF / gNMI
```

Routing policy is listed after BGP because the attributes it sets are BGP’s. The prefix-list syntax is worth reading the same day you configure the first neighbor.

## What these notes still do not replace

| Topic | Where to go next |
|--------|------------------|
| Full IS-IS labs | A vendor course after the intro note and JNCIS-SP |
| Carrier-grade TE and FRR | A Nokia, Junos, or IOS-XR lab. The RSVP and SR notes are the mechanism. |
| ASIC and SDK forwarding | Internal architecture docs. [RIB, FIB, and LFIB](07-forwarding/01-rib-fib-lfib.md) is the public model only. |
| IKE transform sets and PKI | The vendor’s current IPsec guide. [MTU and tunnels](03-routing/12-mtu-and-tunnels.md) is the header and the failure mode. |
| A wireless site survey | The wireless note stops at channels, association, and the VLAN map. |
| Product SD-WAN | The overlay idea is GRE, IPsec, and EVPN. The controller and the business policy are the product’s own course. |

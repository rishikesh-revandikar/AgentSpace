# Networking

Notes for the roadmap below, grouped by what you are trying to learn. Watch the video linked in the note, then read the note and the article. Each note has a diagram, a worked example, and a short self-check.

Days 1–17 of Jeremy’s IT Lab are the fundamentals, LAN switching, and static routing notes. Everything after that is the rest of the roadmap: OSPF through YANG.

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
| [Network devices](01-fundamentals/network-devices.md) | What switches, routers, and firewalls each stop |
| [Interfaces and cables](01-fundamentals/interfaces-and-cables.md) | Copper, fiber, PoE |
| [TCP/IP model](01-fundamentals/tcp-ip-model.md) | OSI, encapsulation, ports. [Kurose videos](https://gaia.cs.umass.edu/kurose_ross/videos/1/) |
| [Command line](01-fundamentals/command-line.md) | IOS modes and saving a config |
| [Ethernet switching, part 1](01-fundamentals/ethernet-switching-1.md) | Frames and the MAC table |
| [Ethernet switching, part 2](01-fundamentals/ethernet-switching-2.md) | ARP |
| [IPv4 addressing, part 1](01-fundamentals/ipv4-addressing-1.md) | Masks, classes, private ranges |
| [IPv4 addressing, part 2](01-fundamentals/ipv4-addressing-2.md) | Addresses on interfaces |
| [Switch interfaces](01-fundamentals/switch-interfaces.md) | Speed, duplex, errors |
| [IPv4 header](01-fundamentals/ipv4-header.md) | TTL, fragmentation. [Wireshark Learn](https://www.wireshark.org/learn) |
| [Wireshark](01-fundamentals/wireshark.md) | Capture filters and a real ping |
| [Subnetting, part 1](01-fundamentals/subnetting-1.md) | Equal blocks inside a /24 |
| [Subnetting, part 2](01-fundamentals/subnetting-2.md) | Masks that cross octets |
| [VLSM](01-fundamentals/subnetting-vlsm.md) | Different sizes from one block |
| [IPv6](01-fundamentals/ipv6.md) | Address types, NDP, SLAAC |

## 02 — LAN switching

| Note | Roadmap topic |
|------|----------------|
| [VLANs, access ports](02-lan-switching/vlans-access-ports.md) | One broadcast domain per VLAN |
| [Trunks and router on a stick](02-lan-switching/vlans-trunks-and-roas.md) | 802.1Q and inter-VLAN routing |
| [Spanning tree](02-lan-switching/spanning-tree.md) | Loops, RSTP, root bridge |

## 03 — Routing

| Note | Roadmap topic |
|------|----------------|
| [Static routing](03-routing/static-routing.md) | RIB, longest match, static and default routes |
| [Life of a packet](03-routing/life-of-a-packet.md) | [Packet Traveling](https://www.youtube.com/watch?v=rYodcvhh7b8) |
| [OSPF](03-routing/ospf.md) | Areas, DR, LSAs. [Jeremy’s notes](https://www.jeremysitlab.com/ccna-resources/) |
| [IS-IS](03-routing/is-is.md) | Levels, NET, TLVs. [31-minute intro](https://www.youtube.com/watch?v=jWdD8SCwzHk) |
| [BGP](03-routing/bgp.md) | [Keith Barker playlist](https://www.youtube.com/playlist?list=PLwQhJUHSLJFUO5YzFH2wveh2zcHUKj11w), [how a path is chosen](https://www.practicalnetworking.net/stand-alone/bgp-oldest-path/) |
| [VRF](03-routing/vrf.md) | Separate tables, RD versus RT |

## 04 — MPLS

| Note | Roadmap topic |
|------|----------------|
| [Architecture, LDP, and labels](04-mpls/architecture-ldp-and-labels.md) | Push, swap, pop, PHP. [RFC 3031](https://datatracker.ietf.org/doc/rfc3031/), [What is MPLS?](https://networklessons.com/mpls) |

## 05 — VPN services

| Note | Roadmap topic |
|------|----------------|
| [L3VPN](05-vpn-services/l3vpn.md) | [RFC 4364](https://datatracker.ietf.org/doc/rfc4364/), [RD vs RT PDF](https://www.sunsetlearning.com/wp-content/uploads/2016/11/L3VPNs-route-target-and-route-distinguisher-Part-1.pdf) |
| [PE-CE routing](05-vpn-services/pe-ce-routing.md) | [PE-CE OSPF](https://networklessons.com/mpls/mpls-layer-3-vpn-pe-ce-ospf) |
| [L2VPN, pseudowire, VPLS](05-vpn-services/l2vpn-vpls.md) | [AToM and pseudowire](https://networklessons.com/tag/ldp) |
| [EVPN](05-vpn-services/evpn.md) | [Juniper primer](https://www.juniper.net/documentation/en_US/day-one-books/topics/topic-map/evpn-primer.html), [Cisco EVPN PDF](https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000/evpn/evpn-config-cisco8000/fundamentals-and-core-features-of-evpn.pdf) |

## 06 — Traffic engineering

| Note | Roadmap topic |
|------|----------------|
| [RSVP-TE](06-traffic-engineering/rsvp-te.md) | [RFC 3209](https://datatracker.ietf.org/doc/html/rfc3209), [operation video](https://www.youtube.com/watch?v=LzkKaRATJyw) |
| [SR-MPLS](06-traffic-engineering/sr-mpls.md) | [RFC 8402](https://datatracker.ietf.org/doc/html/rfc8402), [Cisco Community intro](https://community.cisco.com/t5/video/gallerypage/video-id/6064655138001) |
| [SRv6](06-traffic-engineering/srv6.md) | [Explained](https://www.youtube.com/watch?v=c24v8CUDvzI), RFC 8986 |

## 07 — Forwarding

| Note | Roadmap topic |
|------|----------------|
| [RIB, FIB, and LFIB](07-forwarding/rib-fib-lfib.md) | Control plane versus the tables that actually forward |

## 08 — Operations

| Note | Roadmap topic |
|------|----------------|
| [QoS](08-operations/qos.md) | DiffServ, pipe mode, policing versus shaping |
| [High availability](08-operations/high-availability.md) | BFD, graceful restart, NSR |
| [Troubleshooting](08-operations/troubleshooting.md) | A repeatable L3VPN checklist |

## 09 — Automation

| Note | Roadmap topic |
|------|----------------|
| [YANG, NETCONF, RESTCONF, gNMI](09-automation/yang-netconf-gnmi.md) | [DevNet series](https://developer.cisco.com/video/net-prog-basics/00-intro/intro/), [course labs](https://github.com/CiscoDevNet/netprog_basics) |

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
1. Fundamentals folder, then life of a packet
2. LAN switching, including spanning tree
3. OSPF, IS-IS, BGP, VRF
4. MPLS architecture
5. L3VPN, then PE-CE, then L2VPN and EVPN
6. RSVP-TE, then SR-MPLS. SRv6 only if the product needs it
7. RIB/FIB/LFIB, QoS, HA, the troubleshooting checklist
8. YANG / NETCONF / gNMI
```

## Gaps

| Topic | What the note does not replace |
|--------|--------------------------------|
| Full IS-IS labs | A vendor course after the 31-minute intro and JNCIS-SP |
| Carrier-grade TE and FRR | A Nokia, Junos, or IOS-XR lab. The note is the mechanism. |
| ASIC and SDK forwarding | Internal architecture docs. [RIB, FIB, and LFIB](07-forwarding/rib-fib-lfib.md) is the public model only. |

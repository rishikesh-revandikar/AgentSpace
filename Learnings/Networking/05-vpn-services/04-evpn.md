# EVPN

EVPN carries Ethernet and IP advertisements in BGP. The data plane can be MPLS or VXLAN. The control plane is the same idea either way: MAC addresses and host routes are routes, so they can be advertised, filtered, and withdrawn, instead of being learned by flooding. That is the fix for the VPLS problems in [L2VPN and VPLS](03-l2vpn-vpls.md).

## References

### Videos

- [Why EVPN/VXLAN, Juniper](https://www.networkingvideos.com/watch.php?vid=3c3d3abfe)
- [Juniper EVPN-VXLAN architecture](https://www.youtube.com/watch?v=EBjPve8AmR4)

### Articles

- [Juniper EVPN primer (Day One)](https://www.juniper.net/documentation/en_US/day-one-books/topics/topic-map/evpn-primer.html)
- [Cisco EVPN fundamentals, IOS XR (PDF)](https://www.cisco.com/c/en/us/td/docs/iosxr/cisco8000/evpn/evpn-config-cisco8000/fundamentals-and-core-features-of-evpn.pdf)
- [Juniper, EVPN with VXLAN encapsulation](https://www.juniper.net/documentation/us/en/software/junos/evpn/topics/concept/evpn-vxlan-data-plane-encapsulation.html) — the concepts apply to MPLS encapsulation too
- [RFC 7432, BGP MPLS-based Ethernet VPN](https://datatracker.ietf.org/doc/html/rfc7432)

## Diagram

```mermaid
flowchart LR
  H1["Host MAC M, IP 10.1.1.10"] --- PE1
  PE1 ---|"BGP EVPN type 2: MAC M, IP, ESI"| RR["Route reflector"]
  RR --- PE2
  PE2 --- H2["Host that wants M"]
```

PE1 learns host M on a local port. It advertises an EVPN type 2 route. PE2 installs M pointing at PE1. When H2 sends a frame to M, PE2 already knows the egress PE. It does not flood the unknown unicast across the fabric.

## What is advertised

EVPN route types you will meet:

| Type | Name | What it is for |
|------|------|----------------|
| 1 | Ethernet auto-discovery | Fast withdraw of an entire segment, aliasing when a site is multihomed |
| 2 | MAC/IP | One MAC, and optionally the IP that sits on it. This is the host advertisement. |
| 3 | Inclusive multicast | Who needs BUM (broadcast, unknown unicast, multicast) for this VLAN or VNI |
| 4 | Ethernet segment | Which PEs attach to the same multihomed site, so they can elect a designated forwarder |
| 5 | IP prefix | A subnet, not a host. This is how EVPN carries L3VPN-style prefixes. |

Type 2 is the one to draw. Type 5 is the one that replaces “stretch the VLAN so that routing works.” If the requirement is “reach this subnet,” advertise a type 5 and route. If the requirement is “these two hosts must be in one L2 segment,” use type 2 and a stretched VLAN, and keep that stretch small.

## Data planes

The control plane does not change when the encapsulation does.

| Encapsulation | Where the identifier lives | Typical network |
|---------------|----------------------------|-----------------|
| MPLS | A label under the transport label, same shape as a VPN label | Service-provider WAN, and some data centers |
| VXLAN | A VNI in a UDP header, usually destined to a VTEP loopback | Data-center fabric |

VXLAN is often what the Juniper and Cisco primers use in pictures. An MPLS EVPN uses the same route types and puts a label in the advertisement instead of a VNI. Do not learn two protocols. Learn one control plane and two ways to write the tunnel header.

Underlay versus overlay:

- The **underlay** gets packets between PEs or VTEPs. It is the IGP plus LDP or SR, or it is IP reachability of VTEP loopbacks in a VXLAN fabric.
- The **overlay** is EVPN. It tells the PE which tunnel to use for which MAC or prefix.

If the underlay cannot reach the far VTEP, the EVPN route can still be in BGP and the traffic is blackholed. Same failure mode as an L3VPN next hop with no transport label.

## Multihoming

A CE connected to two PEs is an **Ethernet segment**, identified by an ESI. Both PEs advertise the same ESI in a type 4 route and elect a **designated forwarder** per VLAN. The designated forwarder is the one allowed to send flooded traffic toward that CE, so the CE does not receive duplicates.

If one PE loses the CE link, it withdraws the type 1 auto-discovery route. Remote PEs drop every MAC that was reachable only through that segment without waiting for each MAC to age out. VPLS cannot do that withdraw. This is the operational difference during a failure.

**Aliasing** lets a remote PE load-balance to both PEs of a segment even if it has only seen the MAC advertised by one of them. The type 1 route says “this ESI is also reachable here.”

## IRB and the anycast gateway

Integrated routing and bridging means the PE has both a bridge table for the VLAN and a routing interface in that VLAN. The gateway IP is configured on every PE with the **same** address and the **same** MAC (an anycast gateway). A host ARPs for the gateway and gets a local answer. The packet is routed at the first PE, not bridged across the fabric to a central firewall or a single gateway.

That is the default data-center design: bridge inside the rack or the VLAN if you must, route everywhere else, advertise host routes (type 2) or prefixes (type 5) so the return path is known.

## Spine and leaf, the fabric underneath VXLAN

A data-center picture of EVPN is usually a **leaf-spine** underlay, not a campus triangle of switches.

- **Leaves** attach the servers. Each leaf is a VTEP.
- **Spines** connect leaves to each other. Spines do not connect to servers, and in the classic design they do not connect to each other.
- Every leaf has a link to every spine. Those links are routed (/31 or /32-on-loopback with unnumbered), so spanning tree has nothing to block.
- The underlay IGP (or BGP) gives every leaf equal-cost paths to every other leaf’s loopback. Traffic spreads across the spines.
- EVPN on top decides which VNI and which VTEP a MAC or prefix uses.

If someone draws EVPN as one big VLAN stretched across a Layer 2 underlay, they have rebuilt the failure domain EVPN was brought in to leave. The underlay should already be able to route from leaf to leaf before the first EVPN route exists. MTU has to fit the VXLAN header. That arithmetic is in [MTU and tunnels](../03-routing/12-mtu-and-tunnels.md).

## What you give up if you stretch every VLAN everywhere

EVPN can stretch a VLAN across a data center. Doing it for every subnet recreates the VPLS failure domain: broadcasts, STP or its replacement, and a large BUM domain. Use EVPN’s ability to route. Stretch L2 only for the workloads that actually move and need the same address.

## Check yourself

1. Which route type advertises a single MAC?
2. A VXLAN primer and an MPLS EVPN design share which piece, the encapsulation or the control plane?
3. What problem does the designated forwarder solve?
4. The EVPN route is present and the far VTEP is not reachable in the underlay. Does traffic flow?
5. When do you advertise a type 5 instead of stretching the VLAN?

## Answers

1. Type 2, MAC/IP advertisement.
2. The control plane. The encapsulation is MPLS labels or a VXLAN VNI.
3. Two PEs attached to one multihomed CE would both flood toward it. The designated forwarder is the one that does, per VLAN.
4. No. EVPN tells you which PE. The underlay has to be able to carry the packet there.
5. When the requirement is IP reachability to a subnet. Type 5 is a prefix advertisement. Stretching the VLAN is for hosts that must share a broadcast domain.

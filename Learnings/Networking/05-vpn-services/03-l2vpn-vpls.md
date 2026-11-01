# L2VPN, pseudowire, and VPLS

An L3VPN carries IP prefixes. An L2VPN carries Ethernet frames, so the customer keeps a single subnet, a single broadcast domain, or a single router adjacency across sites. The provider still uses a transport label to cross the core. The inner label identifies a pseudowire instead of a VRF.

## References

### Videos

- [NetworkLessons, AToM and pseudowire topics](https://networklessons.com/tag/ldp)

### Articles

- [RFC 3985, pseudowire emulation edge to edge](https://datatracker.ietf.org/doc/html/rfc3985)
- [RFC 4762, VPLS using LDP](https://datatracker.ietf.org/doc/html/rfc4762)
- Juniper TechLibrary, search “VPLS”. Nokia’s syllabus is in the [SRC self-paced catalog](https://www.nokia.com/networks/training/src/self-paced/) (the PDFs are paid).

The transport under the pseudowire is the same MPLS core as [MPLS and LDP](../04-mpls/01-architecture-ldp-and-labels.md). The modern replacement for multipoint L2VPN is [EVPN](04-evpn.md).

## Diagram

```mermaid
flowchart LR
  CE1["CE1, one VLAN"] --- PE1
  PE1 ---|"outer: transport label, inner: VC label"| P
  P --- PE2
  PE2 --- CE2["CE2, same subnet"]
```

CE1 and CE2 believe they share a cable. PE1 pushes a **VC label** (also called a service or PW label) that PE2 allocated, then a transport label for PE2’s loopback. P swaps the transport label. PE2 pops the VC label and emits the original Ethernet frame toward CE2.

## Point to point: a pseudowire

A pseudowire emulates one wire between two PEs. Cisco’s older name is AToM (Any Transport over MPLS). The common case is Ethernet over MPLS, EoMPLS.

What the customer can do on it:

- Run a /30 or any other subnet between two routers, with no provider router in the middle.
- Extend one VLAN between two switches.
- Keep spanning tree, for better or worse. The provider is not routing, so the customer’s BPDUs cross the pseudowire unless someone stripped them.

What the provider configures, conceptually:

- An attachment circuit: the PE interface or VLAN that faces the CE.
- A pseudowire ID that both PEs agree on.
- Targeted LDP, or BGP, to exchange the VC label. The VC label is not the same as the LDP label for the loopback.

Two labels again. If you remember L3VPN, this is the same shape with a different meaning for the inner label: “emit this frame on that attachment circuit,” not “look up this VRF.”

MTU is the usual outage. The core must carry the customer frame plus two labels. A 1500-byte customer MTU needs a larger core MTU, or the pseudowire comes up and large packets disappear. Match MTU on both attachment circuits. A pseudowire that is up for small pings and down for applications is an MTU problem until proven otherwise.

## Multipoint: VPLS

VPLS emulates a switch. Many sites share one broadcast domain. Each PE is a virtual switch:

- It learns source MACs from frames that arrive on attachment circuits and from frames that arrive on pseudowires.
- It floods unknown unicasts, broadcasts, and multicasts.
- It builds a full mesh of pseudowires to the other PEs, or a hierarchical design (H-VPLS) with spoke PWs into a smaller full mesh.

**Split horizon** is what stops a loop. A frame that arrived on a pseudowire is not forwarded out another pseudowire in the same mesh. Flooding goes to attachment circuits and, if this PE is the source, out the mesh once. Without split horizon the full mesh is a permanent loop and customer STP cannot save you, because each PE would be re-flooding inside the provider.

The costs, which are why EVPN replaced VPLS for new designs:

- MAC learning is in the data plane. A new host is unknown until a frame arrives, and that frame is flooded to every site.
- Withdrawal is slow. A PE that dies is noticed when the pseudowire goes down, not by a BGP update.
- Multihoming an active-active site is awkward. Two PEs advertising the same MAC, or both flooding, need extra machinery VPLS does not have cleanly.
- The full mesh is `n*(n-1)/2` pseudowires. Fifty sites is over a thousand pseudowires.

## When you still use which

| Need | Fit |
|------|-----|
| Two routers, one logical link, no customer routing through the provider | Pseudowire |
| A handful of sites that must be one LAN, and EVPN is not available | VPLS |
| New multipoint, multihoming, or both L2 and L3 | EVPN |

A pseudowire is still the right tool for a point-to-point circuit. VPLS is the tool you will debug in networks that were built before EVPN. You should not pick it for a new multipoint service if EVPN is an option.

## Check yourself

1. What does the inner label select on a pseudowire, compared with an L3VPN?
2. Why does a full mesh of VPLS pseudowires not loop by itself?
3. A pseudowire passes a 64-byte ping and drops a 1500-byte ping. What do you compare?
4. Does the P router learn the customer’s MAC addresses?
5. Name two reasons a new design uses EVPN instead of VPLS.

## Answers

1. The attachment circuit to send the frame out of. An L3VPN inner label selects a VRF for an IP lookup.
2. Split horizon: traffic that arrived on a mesh pseudowire is not sent onto another mesh pseudowire.
3. The MTU on both attachment circuits and the core. Labels add bytes the customer frame did not have.
4. No. MAC learning happens on the PEs. The P router only swaps the transport label.
5. Data-plane flooding of unknown MACs, and weak active-active multihoming. EVPN learns MACs in BGP and can withdraw them quickly. The pseudowire count of a full mesh is a third reason.

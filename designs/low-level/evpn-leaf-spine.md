---
type: Low-Level Network Design
title: EVPN Leaf-Spine Network Design
description: BGP EVPN leaf-spine design with VXLAN overlays and tenant segmentation.
resource: urn:network-design:evpn_leaf_spine_design
tags: [evpn, vxlan, leaf-spine, bgp, security, automation]
timestamp: 2025-06-26T00:00:00Z
owner: Gary Woodward
status: approved
version: "1.0"
---

# Topology and addressing

The two-tier fabric gives every leaf a consistent two-hop path to every other leaf. The underlay uses `10.0.0.0/24` for router IDs, `10.100.100.0/24` for VTEPs, and dedicated point-to-point ranges. Tenant overlays use separate RFC 1918 prefixes.

# Design decisions

| Decision | Rationale |
|---|---|
| Unique BGP AS per leaf | Clear policy boundaries and simpler troubleshooting |
| Structured VLAN-to-VNI mapping | Predictable allocation and operational scale |
| Dedicated L3VNI | Efficient inter-VLAN routing within tenant VRFs |
| Dual spine connectivity | Path redundancy and load distribution |
| Fabric MTU of 9214 bytes | Carries a 9000-byte payload plus VXLAN overhead |

# Security

VRFs isolate tenant routing tables. Endpoint learning is distributed through EVPN rather than unrestricted flood-and-learn behavior. Management access, ACLs, and role-based controls follow the [network standards](../../standards/network.md).

# Operations

The design is intended for infrastructure-as-code delivery with templates, validation, telemetry, configuration backups, and tested rollback procedures. See the [runbook catalog](../../operations/network-runbooks.md).

# Related knowledge

* [Data-center fabric HLD](../high-level/dc-fabric.md)
* [DC1 implementation profile](dc1-evpn-vxlan.md)
* [Sample configurations](../../examples/sample-configs.md)

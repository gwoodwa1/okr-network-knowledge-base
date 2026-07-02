---
type: Low-Level Network Design
title: DC1 EVPN/VXLAN Fabric
description: Implementation profile for an automated, multi-tenant EVPN/VXLAN fabric in DC1.
resource: urn:network-design:LLD-DC1-EVPN-001
tags: [dc1, evpn, vxlan, bgp, gitops, multi-tenancy]
timestamp: 2026-07-02T00:00:00Z
owner: Network Engineering Team
status: draft-demo
version: "1.1"
---

# Design profile

| Area | Value |
|---|---|
| Underlay | eBGP unnumbered over IPv6 link-local addresses |
| Overlay | MP-BGP EVPN with VXLAN |
| Routing | Anycast gateway and distributed Layer 3 forwarding |
| Scale target | 65,536 endpoints, 512 VNIs, 128 tenants |
| VTEPs | Loopback1 addresses in `10.0.255.0/24` |
| VXLAN | UDP 4789, head-end replication, ARP suppression |
| Convergence | BFD at 300 ms with EVPN mass-withdraw |

# Tenant model

| Tenant | VRF | VNI range | Gateway |
|---|---|---|---|
| Tenant A | `TenantA` | 10100-10199 | Anycast |
| Tenant B | `TenantB` | 10200-10299 | Anycast |
| Shared services | `Shared-Services` | 10000 | Centralized |

# Automation and validation

Jinja2 templates render declarative configuration. Terraform provisions the underlay, Ansible deploys the overlay, and Batfish plus custom checks validate changes before and after deployment.

Required validation covers intra-VNI traffic, inter-VNI routing, VTEP failover, MAC mobility, and control-plane scale.

# Related knowledge

* Implements the [data-center fabric HLD](../high-level/dc-fabric.md).
* Uses the baseline [network standards](../../standards/network.md).
* Draws configuration patterns from [sample configurations](../../examples/sample-configs.md).
* Operational procedures are catalogued in [network runbooks](../../operations/network-runbooks.md).

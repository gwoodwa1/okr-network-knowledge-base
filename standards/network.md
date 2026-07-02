---
type: Engineering Standard
title: Baseline Network Standards
description: Naming, addressing, routing, security, and change-control conventions.
resource: urn:network-standard:NS-001
tags: [standards, naming, addressing, routing, security, change-control]
timestamp: 2026-07-02T00:00:00Z
owner: Network Standards Team
status: draft-demo
version: "1.0"
---

# Requirements

* Name devices using a site-role-sequence pattern such as `dc1-leaf-101`.
* Separate underlay, overlay, and management address spaces.
* Use BGP for underlay and overlay exchange where appropriate.
* Summarize routes when doing so improves stability and scale.
* Require strong management authentication and prefer SSH and HTTPS.
* Apply ACLs and role-based access consistently.
* Review and validate changes, back up current state, and define rollback criteria.

# Compliance checklist

- [ ] Naming convention applied
- [ ] Addressing plan reviewed
- [ ] Routing policy validated
- [ ] Security controls verified
- [ ] Change plan and rollback approved

# Applied by

* [Data-center fabric HLD](../designs/high-level/dc-fabric.md)
* [MPLS core HLD](../designs/high-level/mpls-core.md)
* [DC1 EVPN/VXLAN LLD](../designs/low-level/dc1-evpn-vxlan.md)

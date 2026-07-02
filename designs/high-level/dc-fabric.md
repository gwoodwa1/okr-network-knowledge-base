---
type: High-Level Network Design
title: Data Center Fabric
description: Scalable, automation-friendly five-stage Clos fabric using BGP EVPN/VXLAN.
resource: urn:network-design:HLD-DC-FAB-001
tags: [data-center, clos, evpn, vxlan, automation]
timestamp: 2026-07-02T00:00:00Z
owner: Network Architecture Team
status: draft-demo
version: "1.1"
---

# Purpose

Define a scalable and resilient data-center fabric with repeatable Day-0, Day-1, and Day-2 operations.

# Architecture

| Area | Decision |
|---|---|
| Topology | Five-stage Clos across eight pods |
| Underlay | eBGP unnumbered, with OSPF as a contingency |
| Overlay | VXLAN with an MP-BGP EVPN control plane |
| Gateway | Distributed anycast gateway |
| Resilience | N+2 at each layer with sub-second convergence |
| Operations | Git workflows, zero-touch provisioning, telemetry, and automated remediation |

The scale model contains four super-spines, 32 spines, and 128 leaves per pod. It targets 128,000 endpoints and large east-west traffic patterns.

# Design principles

* Scale horizontally across pods.
* Standardize deployment and troubleshooting.
* Enforce segmentation and secure management.
* Drain traffic for non-disruptive maintenance.

# Related knowledge

* [DC1 EVPN/VXLAN low-level design](../low-level/dc1-evpn-vxlan.md) implements this architecture.
* [EVPN leaf-spine design](../low-level/evpn-leaf-spine.md) explains the core design decisions.
* [Network standards](../../standards/network.md) define the baseline controls.
* [Operational runbooks](../../operations/network-runbooks.md) cover routine and incident operations.

# Risks

| Risk | Impact | Mitigation |
|---|---|---|
| 400G optics availability | High | Dual-source optics and keep buffer inventory. |
| Automation readiness | High | Train operators and maintain tested runbooks. |
| Power and cooling limits | Medium | Review rack-density and capacity models. |

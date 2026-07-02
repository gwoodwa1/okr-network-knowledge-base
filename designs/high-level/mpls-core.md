---
type: High-Level Network Design
title: MPLS Core
description: Resilient dual-core MPLS architecture for scalable carrier-grade services.
resource: urn:network-design:HLD-MPLS-CORE-001
tags: [mpls, core, l3vpn, traffic-engineering, resilience]
timestamp: 2026-07-02T00:00:00Z
owner: Core Network Architecture Team
status: draft-demo
version: "1.0"
---

# Purpose

Define a predictable, scalable MPLS core with standardized routing, protection, QoS, and operations.

# Architecture

| Area | Decision |
|---|---|
| Topology | Dual core with PE, P, and edge roles |
| Control plane | IS-IS or OSPF with MPLS label distribution |
| Data plane | MPLS forwarding with traffic-engineering options |
| Services | L3VPN, VPLS, and pseudowire transport |
| Scale | More than 200 PE routers and 10,000 LSPs |

Fast reroute protects link failures, the dual-plane design protects node failures, and graceful shutdown supports planned maintenance.

# Related knowledge

* [Network standards](../../standards/network.md) provide routing and change-control conventions.
* [Operational runbooks](../../operations/network-runbooks.md) define recovery and maintenance practices.
* [Sample configurations](../../examples/sample-configs.md) include illustrative MPLS LSP intent.

# Risks

| Risk | Mitigation |
|---|---|
| Route churn during maintenance | Use planned windows, graceful shutdown, and route dampening. |
| Vendor-specific feature gaps | Standardize on common capabilities. |
| Capacity exhaustion | Perform periodic forecasting and growth reviews. |

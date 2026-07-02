---
type: Runbook Catalog
title: Network Operational Runbooks
description: Standard procedures for EVPN troubleshooting, tenant onboarding, BGP recovery, and maintenance.
resource: urn:network-runbook-catalog:RUNBOOKS-001
tags: [operations, incident-response, evpn, bgp, maintenance]
timestamp: 2026-07-02T00:00:00Z
owner: Network Operations Team
status: draft-demo
version: "1.0"
---

# EVPN troubleshooting

1. Confirm control-plane adjacencies and route exchange.
2. Validate VNI mappings and MAC learning state.
3. Verify VTEP reachability and BUM handling.
4. Review logs for flapping or policy mismatches.

# Tenant onboarding

1. Allocate the VRF and VNIs.
2. Apply routing policy and gateway settings.
3. Validate reachability and segmentation.
4. Update inventory and documentation.

# BGP recovery

1. Confirm peer state and health.
2. Review advertisements and route reflectors.
3. Apply reviewed corrective changes.
4. Re-test convergence and stability.

# Planned maintenance

1. Capture pre-check evidence and confirm capacity.
2. Drain traffic and validate failover.
3. Execute the change with checkpoints and rollback criteria.
4. Confirm service restoration and update records.

# References

Procedures must follow the [network standards](../standards/network.md) and the relevant [design](../designs/).

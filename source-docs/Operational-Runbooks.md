# Operational-Runbooks: Standard Operational Procedures

**Document ID:** RUNBOOKS-001  
**Version:** 1.0 (Demo)  
**Date:** 2026-07-02  
**Owner:** Network Operations Team  
**Status:** Draft / Demo for Knowledge Base

## Purpose

This document provides a catalog of example operational runbooks for common network activities. It is structured for knowledge-base use and supports incident response, maintenance, and troubleshooting practices.

## Runbook Catalog

### 1. EVPN Troubleshooting

- Confirm control-plane adjacency and route exchange
- Validate VNI mapping and MAC learning state
- Verify VTEP reachability and BUM handling
- Review logs for flapping or policy mismatches

### 2. Tenant Onboarding

- Create VRF and VNI assignments
- Apply routing policy and gateway settings
- Validate reachability and segmentation behavior
- Update inventory and documentation records

### 3. BGP Recovery

- Confirm session state and peer health
- Review prefix advertisements and route reflectors
- Apply corrective config changes if required
- Re-test convergence and session stability

### 4. Planned Maintenance

- Pre-check device health and capacity
- Drain traffic and validate failover behavior
- Execute maintenance steps with checkpoints
- Confirm service restoration and documentation updates

## Operational Principles

- Use documented steps and checkpoints
- Capture evidence before and after change execution
- Prefer reversible actions with clear rollback guidance
- Keep runbooks aligned with current design standards

## Version History

- v1.0 – 2026-07-02 – Initial demo version

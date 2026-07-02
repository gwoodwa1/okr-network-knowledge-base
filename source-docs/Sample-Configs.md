# Sample-Configs: Illustrative Configuration Examples

**Document ID:** CFG-EX-001  
**Version:** 1.0 (Demo)  
**Date:** 2026-07-02  
**Owner:** Network Engineering Team  
**Status:** Draft / Demo for Knowledge Base

## Purpose

This document provides example configuration snippets for illustration in the knowledge base. The content is intentionally simplified and should not be used as-is for production environments.

## Example 1: BGP Underlay

```yaml
router bgp 65101
  router-id 10.0.0.101
  neighbor underlay peer-group
  neighbor underlay remote-as external
  neighbor Ethernet1-32 peer-group underlay
  address-family ipv4
    neighbor underlay activate
```

## Example 2: EVPN/VXLAN Overlay

```yaml
vlan 100
  name TenantA-Web
  vn-segment 10100

interface Vlan100
  vrf TenantA
  ip address virtual 172.16.100.1/24
```

## Example 3: Basic ACL Policy

```text
ip access-list extended mgmt-allow
  10 permit tcp any any eq 22
  20 permit tcp any any eq 443
```

## Example 4: MPLS LSP Intent

```text
mpls interface Ethernet3
mpls ldp igp sync
router ospf 1
  area 0
```

## Notes

- These examples are intentionally illustrative
- Replace values with environment-specific requirements before use
- Keep sample content aligned with design and standards documentation

## Version History

- v1.0 – 2026-07-02 – Initial demo version

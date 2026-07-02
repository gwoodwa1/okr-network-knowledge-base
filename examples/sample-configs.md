---
type: Configuration Reference
title: Sample Network Configurations
description: Illustrative snippets for BGP underlay, EVPN/VXLAN, management ACLs, and MPLS.
resource: urn:network-config-reference:CFG-EX-001
tags: [configuration, bgp, evpn, vxlan, acl, mpls]
timestamp: 2026-07-02T00:00:00Z
owner: Network Engineering Team
status: draft-demo
version: "1.0"
---

# BGP underlay

```text
router bgp 65101
  router-id 10.0.0.101
  neighbor underlay peer-group
  neighbor underlay remote-as external
  neighbor Ethernet1-32 peer-group underlay
```

# EVPN/VXLAN overlay

```text
vlan 100
  name TenantA-Web
  vn-segment 10100
interface Vlan100
  vrf TenantA
  ip address virtual 172.16.100.1/24
```

# Management ACL

```text
ip access-list extended mgmt-allow
  10 permit tcp any any eq 22
  20 permit tcp any any eq 443
```

# MPLS LSP intent

```text
mpls interface Ethernet3
mpls ldp igp sync
router ospf 1
  area 0
```

# Usage

These fragments are illustrative. Replace all values with environment-specific requirements and validate them against the [network standards](../standards/network.md) and applicable [design](../designs/) before use.

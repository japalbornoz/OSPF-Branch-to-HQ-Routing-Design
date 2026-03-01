# Baseline Validation

## Objective
Verify that the redesigned multi-segment OSPF topology is operating normally before performing failure testing.

This baseline confirms:
- interface health
- OSPF neighbor formation
- route learning
- DR/BDR election
- default route origination
- end-to-end reachability

---

## Scope
Baseline validation was performed for the following OSPF design elements:

- point-to-point serial OSPF adjacency
- Ethernet broadcast multiaccess OSPF adjacency
- DR/BDR election behavior
- OSPF authentication across transit links
- loopback advertisement
- passive-interface behavior
- default route origination from R5-WAN
- end-host reachability between HQ and Branch

---

## Interface Validation

### Commands Used
- `show ip interface brief`

### Result
Validated active interfaces were operational:

- **R1-HQ**
  - Fa0/0 up/up
  - S0/3/0 up/up

- **R2-HQ**
  - Fa0/0 up/up
  - S0/3/0 up/up

- **R3-BRANCH**
  - Fa0/0 up/up
  - S0/3/0 up/up

- **R4-BRANCH**
  - Fa0/0 up/up
  - S0/3/0 up/up

- **R5-WAN**
  - Fa0/0 up/up
  - Gi0/2/0 up/up

### Conclusion
All required forwarding-path interfaces were operational during baseline testing.

---

## OSPF Neighbor Validation

### Commands Used
- `show ip ospf neighbor`

### Point-to-Point Serial Adjacencies
Validated:
- **R1-HQ ↔ R2-HQ** formed FULL adjacency on `10.0.1.0/30`
- **R4-BRANCH ↔ R3-BRANCH** formed FULL adjacency on `10.0.2.0/30`

### Ethernet Multiaccess Adjacencies
Validated:
- **R2-HQ**, **R4-BRANCH**, and **R5-WAN** formed adjacencies on `10.0.3.0/29`

### DR/BDR Election Result
Validated expected OSPF election behavior based on configured priorities:

- **R5-WAN** = DR
- **R2-HQ** = BDR
- **R4-BRANCH** = DROTHER

### Conclusion
OSPF adjacency formation worked as expected across both serial and Ethernet segments.

---

## OSPF Authentication Validation

### Validation Method
OSPF authentication was configured on active transit interfaces and adjacency status was checked.

### Result
- serial adjacencies formed successfully where matching OSPF authentication was configured
- Ethernet multiaccess adjacencies formed successfully where matching OSPF authentication was configured

### Conclusion
OSPF simple authentication settings were correctly matched across active OSPF transit interfaces.

---

## Routing Table Validation

### Commands Used
- `show ip route`
- `show ip protocols`

### Result
Validated the following route-learning behavior:

- R1-HQ learned:
  - Branch LAN
  - internal transit networks
  - loopbacks
  - external default route

- R3-BRANCH learned:
  - HQ LAN
  - internal transit networks
  - loopbacks
  - external default route

- R2-HQ and R4-BRANCH learned:
  - site LAN routes
  - loopbacks
  - external default route from R5-WAN

- R5-WAN learned:
  - internal site routes through OSPF
  - maintained static default route toward ISPR1

### Conclusion
OSPF route propagation across the full topology was successful.

---

## Default Route Origination Validation

### Validation Method
Confirmed static default route on R5-WAN and checked downstream routing tables.

### Result
Internal routers installed:

- `O*E2 0.0.0.0/0`

This confirmed:
- R5-WAN operated as an ASBR
- `default-information originate` successfully injected the default route into OSPF

### Conclusion
Default route origination worked correctly.

---

## End-to-End Reachability

### Tests Performed
- PC-HQ to default gateway
- PC-BRANCH to default gateway
- PC-HQ to PC-BRANCH
- PC-BRANCH to PC-HQ

### Result
End-to-end host communication between HQ and Branch was successful during baseline testing.

### Conclusion
The baseline topology supported normal routed communication between both sites.

---

## Key Observations

- serial OSPF links formed direct FULL adjacencies without DR/BDR election
- Ethernet broadcast OSPF segment performed DR/BDR election
- interface priorities influenced the election result
- OSPF authentication was required for transit adjacency formation
- the WAN-edge router successfully injected a default route into Area 0

---

## Baseline Result
Baseline validation passed successfully.

The redesigned Project 03 topology operated as intended across both point-to-point serial links and the Ethernet broadcast segment. OSPF neighbors formed correctly, DR/BDR election matched design expectations, routes were learned dynamically, the default route was originated successfully from the WAN edge, and end-to-end communication between HQ and Branch was confirmed.

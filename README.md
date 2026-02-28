# CCNA Project 03 – OSPF Branch-to-HQ Routing Design

## Overview
This project demonstrates a small enterprise routed topology built in Cisco Packet Tracer using 3 routers and single-area OSPF. The lab simulates communication between an HQ site and a Branch site through a central WAN router.

The main objective was to configure dynamic routing, validate adjacency formation and route learning, verify end-to-end connectivity, and document link failure and recovery behavior in a non-redundant topology.

An optional enhancement was also added by simulating an ISP-facing uplink on the WAN router and originating a default route into OSPF.

---

## Objectives
- Build a 3-router branch-to-HQ routed topology
- Configure LAN and WAN IPv4 addressing
- Configure single-area OSPF (Area 0)
- Verify OSPF neighbor adjacencies
- Verify dynamic route learning between HQ and Branch
- Validate host-to-host connectivity
- Perform and document failure and recovery testing
- Maintain portfolio-ready project documentation

---

## Topology Summary
The topology uses a simple non-redundant routed design:

PC-HQ --- SW1-HQ --- R1-HQ --- R2-WAN --- R3-BRANCH --- SW2-BRANCH --- PC-BRANCH

### Device Roles
- **R1-HQ** – default gateway for the HQ LAN
- **R2-WAN** – transit/WAN router between HQ and Branch
- **R3-BRANCH** – default gateway for the Branch LAN
- **SW1-HQ** – Layer 2 access switch for HQ
- **SW2-BRANCH** – Layer 2 access switch for Branch

Because there is no redundancy, a routed WAN link failure causes loss of inter-site connectivity. This makes failure behavior easy to observe and document.

---

## IP Addressing Plan

### HQ LAN
- Network: `192.168.10.0/24`
- R1-HQ Fa0/0: `192.168.10.1`
- SW1-HQ VLAN 1: `192.168.10.2`
- PC-HQ: `192.168.10.10`
- Default gateway: `192.168.10.1`

### Branch LAN
- Network: `192.168.20.0/24`
- R3-BRANCH Fa0/0: `192.168.20.1`
- SW2-BRANCH VLAN 1: `192.168.20.2`
- PC-BRANCH: `192.168.20.10`
- Default gateway: `192.168.20.1`

### WAN Links
- **R1-HQ to R2-WAN**
  - Network: `10.0.1.0/30`
  - R1-HQ S0/3/0: `10.0.1.1`
  - R2-WAN S0/3/0: `10.0.1.2`

- **R2-WAN to R3-BRANCH**
  - Network: `10.0.2.0/30`
  - R2-WAN S0/3/1: `10.0.2.1`
  - R3-BRANCH S0/3/1: `10.0.2.2`

### Loopbacks
- R1-HQ Lo0: `1.1.1.1/32`
- R2-WAN Lo0: `2.2.2.2/32`
- R3-BRANCH Lo0: `3.3.3.3/32`

Loopbacks were used for stable router IDs and additional OSPF route verification.

---

## Routing Design
- Routing protocol: **OSPF**
- Process ID: **1**
- Area: **0**
- Design type: **Single-area OSPF**
- Redundancy: **None**

### OSPF Implementation Notes
- LAN-facing interfaces were configured as passive where appropriate
- WAN serial links were used to form active OSPF adjacencies
- HQ, Branch, WAN, and loopback routes were exchanged dynamically

---

## Build Notes
This project was built in **Cisco Packet Tracer** using:
- Cisco 2811 routers
- Cisco 2960 switches
- serial WAN links
- FastEthernet LAN connections

Since the Cisco 2811 router in Packet Tracer does not provide standard Gigabit LAN interfaces in this topology, FastEthernet interfaces were used for site LAN connections.

---

## Baseline Validation

### Interface Status
Verified that all required active interfaces were operational:

- **R1-HQ**
  - Fa0/0 = up/up
  - S0/3/0 = up/up

- **R2-WAN**
  - S0/3/0 = up/up
  - S0/3/1 = up/up

- **R3-BRANCH**
  - Fa0/0 = up/up
  - S0/3/1 = up/up

### OSPF Neighbor Validation
Verified full OSPF adjacency formation:

- R1-HQ formed adjacency with R2-WAN
- R2-WAN formed adjacency with R1-HQ and R3-BRANCH
- R3-BRANCH formed adjacency with R2-WAN

### Routing Table Validation
Verified OSPF route learning:

- R1-HQ learned Branch routes through R2-WAN
- R3-BRANCH learned HQ routes through R2-WAN
- R2-WAN learned both site LANs
- Loopback routes were also learned through OSPF

### End-to-End Connectivity Validation
Validated successful:
- PC-to-default-gateway reachability
- HQ-to-Branch host reachability
- Branch-to-HQ host reachability

Baseline OSPF routing was successfully established and verified.

---

## Optional Enhancement – ISP Simulation and Default Route Origination

A simulated ISP-facing uplink was added on R2-WAN as an optional enhancement beyond the original project scope.

### ISP Link
- R2-WAN Gi0/2/0: `203.0.113.1/30`

### Default Route Configuration
R2-WAN was configured with:
- a static default route toward the simulated ISP
- `default-information originate` under OSPF

### Validation
- R2-WAN generated a Type-5 external LSA for `0.0.0.0/0`
- downstream routers received the external LSA
- after resetting the OSPF process in Packet Tracer, R3-BRANCH installed:
  - `O*E2 0.0.0.0/0 via 10.0.2.1`

### Lab Note
During testing, Packet Tracer did not immediately install the external default route on the downstream router even though the Type-5 LSA was already present in the OSPF database. Resetting the OSPF process refreshed the routing state and the default route was then installed correctly.

This behavior appears to be related to Packet Tracer process/state handling rather than an OSPF design issue.

---

## Failure Testing Plan
This project includes the following failure and recovery scenarios:

1. **Failure Test 1** – R1-HQ to R2-WAN serial link failure
2. **Failure Test 2** – R2-WAN to R3-BRANCH serial link failure
3. **Recovery Test 1** – restore R1-HQ to R2-WAN link
4. **Recovery Test 2** – restore R2-WAN to R3-BRANCH link

Because the topology is non-redundant, failure of either routed WAN link causes loss of inter-site connectivity.

---

## What I Learned
- How to build and validate a 3-router single-area OSPF topology
- How to verify adjacencies, learned routes, and end-to-end connectivity
- How routed WAN failures affect OSPF neighbors and reachability
- How to document baseline, failure, and recovery behavior in a structured way
- How OSPF default-route origination works
- How to distinguish between routing design issues and Packet Tracer quirks

---

## Interview-Ready Summary
I built a 3-router branch-to-HQ routing lab in Cisco Packet Tracer using single-area OSPF. I configured LAN and WAN addressing, validated OSPF neighbor formation and dynamic route learning, verified end-to-end host communication, and documented baseline, failure, and recovery behavior. I also extended the lab by simulating an ISP uplink and testing OSPF default-route origination.

---

## Tools Used
- Cisco Packet Tracer
- Cisco IOS CLI
- Markdown documentation
- CLI validation commands
- Screenshot-based evidence capture

---

## Project Status
- [x] Topology built
- [x] LAN and WAN addressing configured
- [x] OSPF configured
- [x] Baseline validation completed
- [x] End-to-end connectivity verified
- [x] Optional ISP/default-route enhancement tested
- [ ] Failure Test 1 completed
- [ ] Failure Test 2 completed
- [ ] Recovery documentation completed
- [ ] Final screenshot set completed

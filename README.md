# CCNA Project 03 – OSPF Branch-to-HQ Routing Design

## Overview
This project demonstrates a basic routed enterprise topology using 3 routers and single-area OSPF. The lab simulates communication between an HQ site and a Branch site across a transit/WAN router.

The goal of the project was to configure dynamic routing with OSPF, validate end-to-end connectivity, and document routing behavior during link failures and recovery.

## Objectives
- Build a 3-router routed topology in Packet Tracer
- Configure IPv4 addressing for LAN and WAN links
- Configure single-area OSPF (Area 0)
- Verify OSPF neighbor adjacencies
- Verify route propagation between HQ and Branch
- Validate end-to-end connectivity
- Perform link failure and recovery testing
- Document results in a structured validation folder

## Topology Summary
- R1-HQ provides Layer 3 gateway services for the HQ LAN
- R2-WAN acts as the transit router between sites
- R3-BRANCH provides Layer 3 gateway services for the Branch LAN
- OSPF Area 0 is used across all routed links

## IP Addressing Plan

### HQ LAN
- Network: 192.168.10.0/24
- Gateway: 192.168.10.1

### Branch LAN
- Network: 192.168.20.0/24
- Gateway: 192.168.20.1

### WAN Links
- R1-HQ to R2-WAN: 10.0.12.0/30
- R2-WAN to R3-BRANCH: 10.0.23.0/30

## Routing Design
- Dynamic routing protocol: OSPF
- Process ID: 1
- Area: 0
- Design type: Single-area OSPF
- Redundancy: None

## Key Configuration Tasks
- Assigned IP addresses to all router interfaces
- Enabled interfaces and configured serial links
- Configured OSPF network statements on all routers
- Verified neighbor adjacency formation
- Verified OSPF-learned routes in routing tables
- Tested host-to-host connectivity between sites

## Validation Performed
Baseline validation included:
- Interface status checks
- OSPF neighbor verification
- Routing table verification
- Ping tests between routers
- Ping tests between end hosts
- Traceroute from HQ host to Branch host

Failure testing included:
1. R1-HQ to R2-WAN serial link failure
2. R2-WAN to R3-BRANCH serial link failure

Recovery testing included:
1. Restoring the R1-HQ to R2-WAN link
2. Restoring the R2-WAN to R3-BRANCH link

## Expected Behavior
Because the topology has no redundancy, a routed WAN link failure causes loss of connectivity between HQ and Branch. OSPF neighbor relationships drop on the affected link, and routes learned through that path are removed from the routing table.

When the failed link is restored, OSPF neighbor adjacency re-forms and route exchange resumes, restoring end-to-end connectivity.

## What I Learned
- How to design and configure a small multi-router OSPF topology
- How OSPF forms adjacencies across directly connected routed links
- How to verify dynamically learned routes in the routing table
- How link failures affect OSPF neighbors and reachability
- How to document baseline, failure, and recovery results in a structured way

## Interview-Ready Project Summary
I built a 3-router branch-to-HQ routed network in Packet Tracer using single-area OSPF. I configured router interfaces, advertised LAN and WAN networks into OSPF Area 0, verified adjacency formation and route learning, and then tested routing convergence behavior by simulating WAN link failures and recovery.

## Files Included
- Topology diagram
- IP addressing plan
- Device configurations
- Validation notes
- Failure and recovery test evidence
- Packet Tracer lab file

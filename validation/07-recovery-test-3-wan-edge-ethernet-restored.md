# Recovery Test 3 – R5-WAN Ethernet Uplink Restored

## Objective
Restore the WAN-edge router to the Ethernet OSPF segment and verify that the default route is re-originated and installed by internal routers.

---

## Recovery Action
Interface enabled on:
- **R5-WAN FastEthernet0/0**

### Command Used
- `interface fa0/0`
- `no shutdown`

---

## Expected Outcome
- R5-WAN re-forms OSPF adjacencies on the Ethernet segment
- external default route is re-originated
- internal routers reinstall `O*E2 0.0.0.0/0`

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`

---

## Expected Observations
- R2-HQ and R4-BRANCH show R5-WAN again as a neighbor
- default route reappears on internal routers
- WAN-edge dependency is restored

---

## Actual Result
The recovery was successful after enabling `FastEthernet0/0` on R5-WAN.

Observed results:
- R5-WAN interface state returned to up/up
- OSPF adjacencies between R5-WAN and both R2-HQ and R4-BRANCH re-formed successfully
- R2-HQ displayed R5-WAN again as an OSPF neighbor in FULL state
- R4-BRANCH displayed R5-WAN again as an OSPF neighbor in FULL state
- internal routers reinstalled the external default route
- `O*E2 0.0.0.0/0` returned on internal routers through R5-WAN
- internal site-to-site communication between HQ and Branch remained operational
- external reachability was restored from both HQ and Branch hosts
- brief packet loss was observed during reconvergence, then connectivity stabilized

---

## Conclusion
Recovery Test 3 behaved as expected.

Re-enabling the WAN-edge Ethernet interface on R5-WAN restored OSPF adjacencies on the broadcast segment and allowed the default route to be re-originated into the OSPF domain. Internal routers reinstalled the external default route, and both internal site-to-site communication and external reachability were restored successfully.

---

## Evidence (Screenshots)
- ![Recovery Test 3 - R5 Ethernet Restored](../screenshots/recovery-test-3-link-restored.png)
  
- ![Recovery Test 3 - R2 Neighbor and Default Route Restored](../screenshots/recovery-test-3-r2-neighbor-and-default-route-restored.png)

- ![Recovery Test 3 - R4 Neighbor and Default Route Restored](../screenshots/recovery-test-3-r4-neighbor-and-default-route-restored.png)
  
- ![Recovery Test 3 - PC-HQ Internal and External Reachability Restored](../screenshots/recovery-test-3-pc-hq-internal-and-external-restored.png)

- ![Recovery Test 3 - PC-BRANCH Internal and External Reachability Restored](../screenshots/recovery-test-3-pc-branch-internal-and-external-restored.png)

- ![Recovery Test 3 - PC-HQ and PC-BRANCH Internal and External Reachability Test](../screenshots/recovery-test-3-pc-hq-pc-branch.png)

# Failure Test 1 – R1-HQ to R2-HQ Serial Link Down

## Objective
Simulate failure of the HQ-side point-to-point serial OSPF link and observe neighbor loss, route withdrawal, and site impact.

---

## Failure Action
Shutdown performed on:
- **R1-HQ Serial0/3/0**

### Command Used
- `interface s0/3/0`
- `shutdown`

---

## Expected Outcome
- OSPF adjacency between R1-HQ and R2-HQ drops
- R1-HQ loses learned routes from the rest of the OSPF domain
- HQ LAN becomes isolated from Branch and WAN-edge routes
- default route on R1-HQ disappears
- Branch side should remain internally connected to the rest of the non-HQ topology

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`
- ping from PC-HQ to PC-BRANCH
- ping from PC-HQ to remote networks

---

## Expected Observations
- R1-HQ has no OSPF neighbor on Serial0/3/0
- R2-HQ no longer shows R1-HQ as a neighbor
- R1-HQ routing table contains only connected/local routes
- PC-HQ loses reachability to Branch and default-routed destinations

---

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

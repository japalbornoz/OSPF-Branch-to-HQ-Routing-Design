# Failure Test 2 – R4-BRANCH to R3-BRANCH Serial Link Down

## Objective
Simulate failure of the Branch-side point-to-point serial OSPF link and observe route loss and site isolation effects.

---

## Failure Action
Shutdown performed on either:
- **R4-BRANCH Serial0/3/0**
or
- **R3-BRANCH Serial0/3/0**

### Command Used
- `interface s0/3/0`
- `shutdown`

---

## Expected Outcome
- OSPF adjacency between R4-BRANCH and R3-BRANCH drops
- Branch LAN becomes isolated from HQ and WAN-edge routes
- R3-BRANCH loses remote OSPF routes and default route
- internal Ethernet OSPF segment between R2-HQ, R4-BRANCH, and R5-WAN remains functional

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`
- ping from PC-BRANCH to PC-HQ

---

## Expected Observations
- R3-BRANCH loses its only OSPF neighbor
- Branch router loses learned remote routes
- default route disappears from R3-BRANCH
- PC-BRANCH cannot reach HQ LAN

---

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

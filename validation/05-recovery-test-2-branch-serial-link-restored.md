# Recovery Test 2 – R4-BRANCH to R3-BRANCH Serial Link Restored

## Objective
Restore the Branch-side serial link and verify OSPF reconvergence and Branch reachability restoration.

---

## Recovery Action
Interface enabled on:
- **R4-BRANCH Serial0/3/0**
or
- **R3-BRANCH Serial0/3/0**

### Command Used
- `interface s0/3/0`
- `no shutdown`

---

## Expected Outcome
- adjacency between R4-BRANCH and R3-BRANCH returns
- Branch-side learned routes are reinstalled
- external default route returns on R3-BRANCH
- Branch-to-HQ communication is restored

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`
- ping from PC-BRANCH to PC-HQ

---

## Expected Observations
- R3-BRANCH shows FULL adjacency to R4-BRANCH
- learned routes reappear in the routing table
- `O*E2 0.0.0.0/0` returns on R3-BRANCH
- host communication succeeds again

---

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

# Recovery Test 1 – R1-HQ to R2-HQ Serial Link Restored

## Objective
Restore the HQ-side serial OSPF link and verify neighbor re-formation, route reinstallation, and end-to-end recovery.

---

## Recovery Action
Interface enabled on:
- **R1-HQ Serial0/3/0**

### Command Used
- `interface s0/3/0`
- `no shutdown`

---

## Expected Outcome
- OSPF adjacency between R1-HQ and R2-HQ returns
- learned OSPF routes reappear on R1-HQ
- external default route returns
- HQ-to-Branch connectivity is restored

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`
- ping from PC-HQ to PC-BRANCH

---

## Expected Observations
- R1-HQ shows R2-HQ neighbor in FULL state
- OSPF routes are repopulated on R1-HQ
- `O*E2 0.0.0.0/0` reappears on R1-HQ
- end-to-end host connectivity succeeds again

---

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

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

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

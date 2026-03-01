# Failure Test 3 – R5-WAN Ethernet Uplink to Internal OSPF Segment Down

## Objective
Simulate loss of the WAN-edge router from the internal Ethernet OSPF segment and observe the effect on default-route origination while keeping internal site routing under review.

---

## Failure Action
Shutdown performed on:
- **R5-WAN FastEthernet0/0**

### Command Used
- `interface fa0/0`
- `shutdown`

---

## Expected Outcome
- OSPF adjacency between R5-WAN and the internal Ethernet segment drops
- internal routers lose the OSPF external default route
- site-to-site internal OSPF routing between HQ and Branch may remain functional if R2-HQ and R4-BRANCH still share the Ethernet segment
- WAN-edge reachability is lost

---

## Verification Commands
- `show ip ospf neighbor`
- `show ip route`
- verify removal of `O*E2 0.0.0.0/0` on R1-HQ, R2-HQ, R3-BRANCH, and R4-BRANCH

---

## Expected Observations
- R5-WAN is no longer present in OSPF neighbor tables of R2-HQ and R4-BRANCH
- internal routers lose the external default route
- internal site LAN routes may still remain if R2-HQ and R4-BRANCH adjacency survives over the Ethernet segment

---

## Result
_To be completed after execution._

---

## Conclusion
_To be completed after execution._

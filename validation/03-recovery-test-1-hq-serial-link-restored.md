# Recovery Test 1 – R1-HQ to R2-HQ Serial Link Restored

## Objective
Restore the HQ-side serial OSPF link and verify neighbor re-formation, route reinstallation, and end-to-end connectivity recovery.

---

## Recovery Action
Interface enabled on:
- **R1-HQ Serial0/3/0**

### Command Used
```cisco
conf t
interface s0/3/0
no shutdown
end
```
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

## Actual Result
- R1-HQ re-formed an OSPF neighbor adjacency with R2-HQ on Serial0/3/0 (FULL state).
- OSPF-learned routes returned on R1-HQ, including:
  -Branch LAN `192.168.20.0/24`
  - transit networks `10.0.2.0/30` and `10.0.3.0/29`
  - remote loopbacks
  - external default route `O*E2 0.0.0.0/0`
- PC-HQ regained reachability to PC-BRANCH. During reconvergence, the first ping showed brief packet loss, then subsequent pings were stable.

---

## Conclusion
Recovery Test 1 behaved as expected. Restoring the HQ serial link allowed OSPF to re-establish adjacency, repopulate the routing table, restore the external default route, and recover end-to-end connectivity between HQ and Branch.

---

## Evidence (Screenshots)
- ![Recovery Test 1 - Neighbor Restored](../screenshots/recovery-test-1-neighbor-restored.png)
  
- ![Recovery Test 1 - Routes Restored](../screenshots/recovery-test-1-routes-restored.png)

- ![Recovery Test 1 - PC-HQ to PC-BRANCH Ping Success](../screenshots/recovery-test-1-pc-hq-to-pc-branch-success.png)

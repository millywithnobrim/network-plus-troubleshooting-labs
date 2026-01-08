# Lab 05 – Multi-Network Connectivity and Static Routing

## Scenario
PCs on the local network can communicate with their default gateway, but cannot reach a remote network hosted on another router.

Router1 simulates a remote site using a loopback interface.
Routing between the two routers is incomplete, preventing end-to-end connectivity.

Your task is to identify and correct missing static routes so that traffic can reach the remote network and return successfully.

---

## Objective
- Understand how static routing enables communication between remote networks
- Identify routing failures caused by missing return paths 
- Reinforce Layer 1, Layer 2, and Layer 3 troubleshooting methodology aligned with CompTIA Network+  

---

## CompTIA Network+ Objective Mapping

### Domain 1.0 – Networking Fundamentals
- 1.2: Compare and contrast network cables, connectors, and interfaces  
- 1.4: Configure IPv4 addressing and subnetting
- 1.6: Explain the purpose of routing

### Domain 2.0 – Network Implementations
- 2.3: Configure and verify routing technologies  

### Domain 5.0 – Network Troubleshooting
- 5.1: Troubleshoot common network connectivity issues 
- 5.3: Use appropriate network diagnostic tools (`ping`, `tracert`, `show ip route`)  

---

## Tasks
1. Verify Physical Connectivity and Cable Types.
2. Verify Host Connectivity `ping`.
3. Verify Router0 Routing Table `show ip route`.  
4. Configure Router0 to reach the remote network via Router1 `ip route`.
5. Verify Router1 Return Path `ping`.
6. Configure Router1 so replies can reach the local network `ip route`.
7. Verify End-to-End Connectivity `ping`.  

---

## Success Criteria
- Full bidirectional connectivity between local PCs and the remote network. 
- Correct cable types verified and functioning.  
- Static routes correctly configured on both routers.  
- The PC can ping Router1's default gateway.  
- All Packet Tracer assessment items pass.  

---

## Restrictions
- No dynamic routing protocols allowed.  
- PCs must not be configured with static routes.  
- Other configuration tabs (Config, Physical) are locked.  

---

## Recommended Commands
- `ipconfig`  
- `ping <IP>`
- `tracert <IP>`
- `show ip route`
- `show running-config | include ip route`
- `show vlan brief`
- `show interface status`  
- `show ip interface brief`  

---

## Notes
- Always verify **Layer 1 before Layer 3**.  
- Loopback interfaces simulate remote networks commonly used in WAN environments.  
- AMissing return routes are a very **common real-world routing failure**.

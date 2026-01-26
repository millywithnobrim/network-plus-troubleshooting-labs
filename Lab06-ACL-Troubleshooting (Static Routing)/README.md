# Lab 06 – ACL Troubleshooting (Static Routing)

## Scenario
PC0, PC1, and PC2 are connected to VLAN 10 and can successfully reach their default gateway on Router0.

PC0, PC1, and PC2 are connected to VLAN 10 and can successfully reach their default gateway on Router0.

Although routing between routers is configured correctly, PCs cannot reach the remote network due to an incorrectly configured Access Control List (ACL).

---

## Objective
- Diagnose ACL-related connectivity failures
- Reinforce ACL logic and processing order 
- Identify implicit deny behavior
- Restore secure, end-to-end connectivity without removing security

---

## CompTIA Network+ Objective Mapping

### Domain 1.0 – Networking Fundamentals 
- 1.4: Explain the characteristics of network topologies and traffic flow
  - ACLs control how traffic flows between network segments
- 1.5: Compare and contrast network ports, protocols, and services
  - ACLs filter traffic based on IP, protocol, and direction

### Domain 2.0 – Network Implementations
- 2.1: Configure switching and routing technologies
  - Static routing between Router0 and Router1
  - Traffic control using extended ACLs
- 2.3: Apply network segmentation concepts
  - VLAN traffic controlled at Layer 3 using ACLs

### Domain 3.0 – Network Operations
- 3.2: Given a scenario, apply network security features
  - Extended ACLs used to restrict traffic while maintaining connectivity 
- 3.4: Explain the purpose of monitoring and logging
  - ACL counters validate permitted and denied traffic 

### Domain 4.0 – Network Security
- 4.1: Explain security concepts
  - Principle of least privilege
  - Implicit deny behavior 
- 4.3: Given a scenario, apply network hardening techniques
  - Filtering inter-network traffic using ACLs instead of removing access

### Domain 5.0 – Network Troubleshooting
- 5.1: Troubleshoot common network connectivity issues
  - ACLs blocking legitimate traffic
  - Misplaced ACL direction (in vs out)
  - Incorrect ACL logic or ordering 
- 5.3: Use appropriate network diagnostic tools (`ping`, `show access-lists`, `show running-config`, `show ip interface`)  

---

## Tasks
1. Verify Host IP Configuration.
2. Verify Local Connectivity.
3. Test Remote Connectivity.  
4. Verify Router Connectivity.
5. Inspect ACL Configuration.
6. Correct the ACL Configuration.
7. Verify ACL Placement.
8. Verify End-to-End Connectivity

---

## Success Criteria
- PCs can ping `10.10.20.1`. 
- Router0 can ping Router1.  
- ACL 100 explicitly permits VLAN 10 traffic.  
- ACL includes a deny-any-any statement.
- ACL is applied to the correct interface and direction.
- All Packet Tracer assessment items pass.  

---

## Restrictions
- Do not modify physical cabling.  
- Do not remove the ACL — it must be corrected.  
- Use CLI tools only for troubleshooting and configuration.
- Desktop IP Configuration may only be used to view IP settings.
- Do not add dynamic routing protocols.
- Do not change VLAN or trunk configurations.

---

## Recommended Commands
- `ipconfig`  
- `ping <IP>`
- `tracert <IP>`
- `show ip route`
- `show running-config`
- `show access-lists`
- `access-list 100 permit ip <source-network> <wildcard> <destination-network> <wildcard>`  
- `access-list 100 deny ip any any`
- `ip access-group 100 out`  

---

## Notes
- ACL issues often resemble routing failures.  
- Implicit deny is a common real-world outage cause.
- Security controls should be corrected, not removed.
- Always verify ACL order, logic, and placement

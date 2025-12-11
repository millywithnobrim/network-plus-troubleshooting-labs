# Lab 02 – VLAN & DHCP Troubleshooting

## Scenario
Two workstations connected to a switch are unable to obtain IP addresses and cannot communicate across VLANs.  
Your task is to **identify and correct misconfigurations** involving VLANs, trunking, router subinterfaces, and DHCP.  
You must use **CLI verification tools** (e.g., `show vlan`, `show interfaces trunk`, `ipconfig`) to troubleshoot.

---

## Objective
- Practice identifying and fixing VLAN, trunking, and DHCP issues  
- Reinforce understanding of inter-VLAN routing and subnetting  
- Develop troubleshooting skills aligned with CompTIA Network+ objectives  

---

## CompTIA Network+ Objective Mapping

### Domain 1.0 – Networking Fundamentals
- 1.4: Configure IPv4 addressing and subnet masks  
- 1.8: Apply and configure VLANs  

### Domain 2.0 – Network Implementations
- 2.1: Configure switching components (VLANs, trunks)  
- 2.2: Configure routing technologies (router-on-a-stick)  

### Domain 5.0 – Network Troubleshooting
- 5.1: Troubleshoot common network service issues:  
  - Incorrect VLAN assignment  
  - Missing or incorrect trunking  
  - Misconfigured DHCP pools  
  - Incorrect router subinterface configuration  
- 5.3: Use appropriate network diagnostic tools (`ping`, `show vlan`, `show ip interface brief`)  

---

## Tasks
1. Use the **Command Prompt** on each PC to gather IP configuration details (`ipconfig`).  
2. Verify VLAN membership using `show vlan brief`.  
3. Check trunk status using `show interfaces trunk`.  
4. Inspect router subinterfaces and DHCP scopes.  
5. Identify and correct the misconfiguration(s).  
6. Verify both PCs obtain valid DHCP addresses.  
7. Confirm inter-VLAN connectivity using `ping`.  

---

## Success Criteria
- PC1 receives an IP in the **VLAN 10** subnet.  
- PC2 receives an IP in the **VLAN 20** subnet.  
- The switch trunk toward the router is operational.  
- Router subinterfaces for each VLAN are correctly configured.  
- Both PCs can ping their default gateways **and each other**.  
- Grading checks (if using Packet Tracer Activity Wizard) pass.  

---

## Restrictions
- All troubleshooting and verification must be done using CLI tools.  
- Desktop IP Configuration may be used only to verify DHCP operation.  
- Other configuration tabs (Config, Physical) are locked.  

---

## Recommended Commands
- `ipconfig`  
- `ping <IP>`  
- `show vlan brief`  
- `show interfaces trunk`  
- `show ip interface brief`  
- `show ip dhcp binding`  

---

## Notes
- This lab simulates a **real-world VLAN and DHCP troubleshooting scenario**.  
- Focus on identifying *why* the failures occur, not only applying commands.  
- All steps align with **Network+ troubleshooting objectives**.

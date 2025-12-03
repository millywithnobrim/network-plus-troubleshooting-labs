# Lab 01 – IP Connectivity Troubleshooting

## Scenario
Two workstations connected to the same switch cannot communicate.  
Your task is to **identify and correct the misconfiguration** to restore connectivity.  
You must use **CLI verification tools** (e.g., `ping`, `ipconfig`, `show interfaces`) to troubleshoot.

---

## Objective
- Practice identifying and fixing common network connectivity issues
- Reinforce IPv4 addressing and subnetting knowledge
- Develop troubleshooting skills aligned with CompTIA Network+ objectives

---

## CompTIA Network+ Objective Mapping

### Domain 1.0 – Networking Fundamentals
- 1.4: Configure IPv4 addressing and subnet masks
- 1.5: Compare and contrast network ports and interfaces

### Domain 2.0 – Network Implementations
- 2.1: Configure switching components (access ports)

### Domain 5.0 – Network Troubleshooting
- 5.1: Troubleshoot common network connectivity issues:
  - Incorrect IP configuration
  - Incorrect subnet mask
  - Disabled switch interface
- 5.3: Use appropriate network diagnostic tools (`ping`, `ipconfig`, `show interfaces`)

---

## Tasks
1. Use the **Command Prompt** on each PC to gather IP configuration details.
2. Test connectivity using `ping`.
3. Identify the misconfiguration.
4. Use the **Desktop IP Configuration** or CLI to correct the issue.
5. Verify end-to-end connectivity is restored.

---

## Success Criteria
- Both PCs can ping each other successfully.
- All locked switch interfaces are enabled.
- Correct IP addresses and subnet masks are applied.
- Grading checks (if using Packet Tracer Activity Wizard) pass.

---

## Restrictions
- All troubleshooting and verification must be done using CLI tools.
- Desktop IP Configuration may be used to set static IPs.
- Other configuration tabs (Config, Physical) are locked.

---

## Recommended Commands
- `ipconfig`
- `ping <IP>`
- `show ip interface brief`
- `show interfaces status`

---

## Notes
- This lab is designed to simulate a **real-world troubleshooting scenario**.
- Focus on understanding **why** connectivity failed, not just following steps.
- All actions should align with **Network+ objectives**.


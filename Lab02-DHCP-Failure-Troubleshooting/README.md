Lab 02 – VLAN & DHCP Troubleshooting
Scenario

Two workstations connected to a switch are unable to obtain IP addresses and cannot communicate across VLANs.
A router-on-a-stick configuration is partially implemented, but DHCP and VLAN assignments are misconfigured.
Your task is to identify and correct the issues so both PCs receive IP addresses and inter-VLAN communication works.

You must use CLI verification tools (e.g., ping, ipconfig, show vlan, show interfaces trunk, show ip dhcp binding) to troubleshoot.

Objective

Practice diagnosing VLAN and DHCP-related connectivity issues

Reinforce understanding of VLAN assignments, trunking, and router subinterfaces

Develop troubleshooting skills aligned with CompTIA Network+ objectives

CompTIA Network+ Objective Mapping
Domain 1.0 – Networking Fundamentals

1.4: Configure IPv4 addressing and subnet masks

1.5: Compare and contrast network topologies and types

1.8: Configure and apply VLAN segmentation

Domain 2.0 – Network Implementations

2.1: Configure and troubleshoot switching concepts (VLANs, trunks)

2.2: Configure routing technologies (router-on-a-stick, subinterfaces)

Domain 3.0 – Network Operations

3.1: Use appropriate documentation and diagrams

3.3: Apply interface and device monitoring tools

Domain 5.0 – Network Troubleshooting

5.1: Troubleshoot common network service issues:

Incorrect VLAN assignment

Missing/incorrect trunking

Misconfigured DHCP pools

Incorrect router subinterface settings

5.3: Use appropriate network diagnostic tools (ping, ipconfig, show vlan, show ip interface brief)

Tasks

Use the Command Prompt on each PC to check IP addressing (ipconfig).

Verify VLAN membership on the switch using show vlan brief.

Check the trunk link using show interfaces trunk.

Inspect router subinterfaces and DHCP configuration.

Correct all misconfigurations (VLANs, trunking, DHCP, or subinterfaces).

Ensure both PCs successfully obtain DHCP leases.

Test inter-VLAN connectivity using ping.

Success Criteria

PC1 receives a DHCP address in VLAN 10 (192.168.10.0/24).

PC2 receives a DHCP address in VLAN 20 (192.168.20.0/24).

Router subinterfaces for VLAN 10 and VLAN 20 are correctly configured.

Switch trunk to router is functioning.

PC1 and PC2 can ping their gateways and each other.

All Packet Tracer grading checks (if using a PKA) pass.

Restrictions

All troubleshooting must be done using CLI tools.

Desktop IP Configuration may only be used to verify DHCP (not to configure VLANs).

Config and Physical tabs are locked in the activity.

You must use the terminal on all devices for all configuration steps.

Recommended Commands
PCs

ipconfig

ping <IP>

Switch

show vlan brief

show interfaces trunk

show ip interface brief

Router

show ip interface brief

show run

show ip dhcp binding

show ip dhcp pool

Notes

This lab simulates a real-world troubleshooting situation where multiple small VLAN and DHCP issues combine to break network connectivity.
Focus on understanding the root cause of each failure rather than simply applying commands.
All tasks map directly to Network+ troubleshooting objectives.

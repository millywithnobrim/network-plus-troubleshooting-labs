# Lab 03 – Switch Port Security Troubleshooting Answer

### Scenario

PC0 is unable to communicate on the network and receives an APIPA address.
PC1 is a working reference host.

PC0 is connected to a switch port with port security enabled, but sticky MAC learning is missing, blocking DHCP traffic.
<br></br>

#### Intentional Faults

- Port security enabled on interface Fa0/1 (PC0’s port)

- Maximum MAC addresses set to 1

- Sticky MAC addressing not configured

- Violation mode set to shutdown

- PC0’s MAC address is not permitted on Fa0/1

- DHCP traffic from PC0 is blocked, resulting in an APIPA address
  
- Interface Fa0/1 remains administratively up, but traffic is blocked by port security
<br></br>

### Objective

- Diagnose switch port security violations

- Understand MAC address restrictions and violation modes

- Restore network access and renew DHCP

- Apply structured troubleshooting methodology
<br></br>

#### Step 1: Verify Host IP Configuration

On PC0:
```
ipconfig /all
```

Expected Finding:
- PC0 has a 169.254.x.x (APIPA) address.
- No default gateway

Concept:
- APIPA indicates a failure to reach a DHCP server, often caused by Layer 2 issues.
<br></br>

#### Step 2: Test Connectivity
On PC0:
```
ping <default-gateway>
```
Expected Result:
- Ping fails.

On PC1:
```
ping <default-gateway>
```

Expected Result:
- Ping suceeds.

Concept:
- A working reference host confirms the network and DHCP server are operational.
- Failure on PC0 isolates the problem to port security.
<br></br>

#### Step 3: Inspect Switch Interface Status

On the switch:
```
show interfaces status
```

Expected Finding:
- Interface Fa0/1 (PC0) shows connected / up

Concept:
- An interface can be up while still blocking traffic due to security policies.
<br></br>

#### Step 4: Inspect Port Security Configuration
```
show port-security
show port-security interface fa0/1
```

Expected Finding:
- Port security: enabled

- Maximum MAC addresses: 1

- Sticky MAC: disabled

- Secure MAC count: 0

Concept:
- Without sticky MAC enabled, the switch does not learn or permit PC0’s MAC address.
<br></br>

#### Step 5: Inspect MAC Address Table
```
show mac address-table
```

Expected Finding:
- PC0’s MAC address is not allowed to forward traffic.

Concept:
- Frames from unauthorized MAC addresses are dropped at Layer 2.
<br></br>

#### Step 6: Correct the Port Security Issue

Enable sticky MAC learning:
```
conf t
interface fa0/1
switchport port-security mac-address sticky
end
```
Expected Finding:
- PC0’s MAC address learned as secure sticky
<br></br>

Concept:
- Sticky MAC allows the switch to dynamically permit the connected host.
<br></br>

#### Step 7: Renew DHCP Lease

On PC0:
```
ipconfig /release
ipconfig /renew
```

Expected Result:
- PC0 receives a valid DHCP-assigned IPv4 address.

Concept:
- Packet Tracer does not automatically retry DHCP after a failure.
<br></br>

#### Step 8: Verify Connectivity
```
ipconfig
ping <PC1-IP>
ping <default-gateway>
```

Expected Result:
- End-to-end connectivity is restored.
<br></br>

### Success Criteria

- PC0 can communicate with PC1 and the default gateway

- Sticky MAC is correctly learned on Fa0/1

- Port security remains enabled and functional

- Interface Fa0/1 is active (not err-disabled)

- DHCP assigns a valid IPv4 address to PC0

- Grading checks (if using Packet Tracer Activity Wizard) pass
<br></br>

### Notes

- Port security can block traffic without disabling a port

- APIPA (169.254.x.x) indicates DHCP failure caused by Layer 2 access issues

- Sticky MAC is required for dynamically permitting devices on secured ports

- Always check the MAC address table when troubleshooting port security

- Focus on why PC0 cannot communicate, not just on executing commands

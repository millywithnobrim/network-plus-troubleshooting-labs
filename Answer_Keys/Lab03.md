# Lab 03 – Switch Port Security Troubleshooting Answer

### Scenario

PC0 cannot communicate on the network.
PC1 is a working reference host.

PC0 is connected to a switch port with port security configured incorrectly, preventing network access.
<br></br>

#### Intentional Faults

- Port security enabled on interface Fa0/1 (PC0’s port)

- Maximum MAC addresses set to 1

- Sticky MAC addressing not configured

- Violation mode set to shutdown

- Interface Fa0/1 is err-disabled

- DHCP traffic from PC0 is blocked, resulting in an APIPA address
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

Concept:
- APIPA indicates a failure to reach a DHCP server, often caused by Layer 2 issues.
<br></br>

#### Step 2: Test Connectivity
```
ping <default-gateway>
```

Expected Result:
- Ping fails.

Concept:
- Failure confirms the issue is not limited to PC-to-PC communication.
<br></br>

#### Step 3: Inspect Switch Interface Status

On the switch:
```
show interfaces status
```

Expected Finding:
- Interface Fa0/1 (PC0) is disabled or err-disabled

- Interface Fa0/2 (PC1) is operational

Concept:
- Port security violations can administratively shut down switch interfaces.
<br></br>

#### Step 4: Inspect Port Security Configuration
```
show port-security
show port-security interface fa0/1
```

Expected Finding:
- Violation count greater than zero

- Violation mode set to shutdown

Concept:
Port security enforces MAC-based access control and can disable interfaces when violations occur.
<br></br>

#### Step 5: Inspect MAC Address Table
```
show mac address-table
```

Expected Finding:
- PC0’s MAC address is not allowed to forward traffic.

Concept:
- If the MAC address is not permitted, frames are dropped at Layer 2.
<br></br>

#### Step 6: Correct the Port Security Issue

Remove the misconfigured security feature and reset the interface:
```
conf t
interface fa0/1
 no switchport port-security
 shutdown
 no shutdown
```

Concept:
- Removing port security clears the violation and restores Layer 2 connectivity.
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

- PC0 no longer has an APIPA address

- Switch interface Fa0/1 is operational

- PC0 can communicate with PC1 and the default gateway

- Packet Tracer grading checks pass
<br></br>

### Notes

- APIPA is a symptom of blocked network access

- Port security issues can silently prevent DHCP

- DHCP renewal is required after restoring connectivity in Packet Tracer

- This lab builds on concepts from Labs 1 and 2

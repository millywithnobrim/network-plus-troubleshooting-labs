# Lab 03 – Switch Port Security Troubleshooting Answer

### Scenario

PC0 cannot communicate.
PC1 works normally.
<br></br>

#### Intentional faults:

- Port security enabled on PC0’s port

- Maximum MAC addresses = 1

- Sticky MAC not configured

- Violation mode = shutdown

- Interface is err-disabled
<br></br>

### Objective

- Troubleshoot switch port security violations

- Understand MAC address restrictions, sticky MAC, and violation modes

- Restore secure access and verify connectivity
<br></br>

#### Step 1: Verify Connectivity Failure

On PC0:
```
ipconfig
ping <gateway>
```

Expected Finding:
- No connectivity.
<br></br>

#### Step 2: Inspect Port Security

On the switch:
```
show port-security
show port-security interface fa0/1
show mac address-table
```

Expected Finding:

- Interface shutdown due to violation

- MAC address not allowed
<br></br>

#### Step 3: Correct Port Security

Option A – Sticky MAC:
```
conf t
interface fa0/1
 switchport port-security mac-address sticky
 shutdown
 no shutdown
```

Option B – Disable Port Security:
```
conf t
interface fa0/1
 no switchport port-security
 shutdown
 no shutdown
```

Concept:
- Sticky MAC allows automatic learning of allowed MACs.
- Err-disabled state must be cleared for connectivity.
<br></br>

#### Step 4: Verify Connectivity
```
ping PC1-IP
ping default-gateway
show mac address-table
show port-security interface fa0/1
```
<br></br>


### Success Criteria:

- PC0 can communicate with PC1 and default gateway

- Interface is active

- MAC address learned correctly

- Packet Tracer grading checks pass
<br></br>

### Notes

- Err-disabled ≠ cable problem

- Port security blocks traffic silently; must be corrected before Layer 3 works

- Teaches real-world access-layer troubleshooting

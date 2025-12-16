# Lab 01 – IP Connectivity Troubleshooting Answer

### Scenario

Two PCs connected to the same switch cannot communicate.
PC1 is a working reference host.
<br></br>

#### Intentional faults:

One or more switch access ports are administratively down

One or more PCs have incorrect IP addresses or subnet masks
<br></br>

### Objective

Practice troubleshooting basic Layer 1–3 issues

Reinforce IPv4 addressing and subnetting concepts

Understand proper troubleshooting order: Interface → IP → Connectivity
<br></br>

#### Step 1: Inspect Interface Status

On the switch:
```
show interfaces status
```

Expected Finding:
Interfaces connected to PC0 or PC1 may be in disabled state.

Concept:
Disabled interfaces block traffic regardless of correct IP configuration.
<br></br>

#### Step 2: Enable Interfaces

```
conf t 
interface fa0/x 
no shutdown (or no shut)
```

Concept:
Restores Layer 2 connectivity and allows traffic to pass.
<br></br>

#### Step 3: Verify IP Configuration

On each PC:
```
ipconfig
```

Expected Finding:
IPs or subnet masks may still be incorrect.

Concept:
Devices on the same subnet must share the same network portion.
<br></br>

#### Step 4: Correct IP Addressing
PC0: 192.168.10.10 /24
PC1: 192.168.10.20 /24
<br></br>

#### Step 5: Verify Connectivity
```
ping <other-PC-IP>
```
<br></br>

### Success Criteria:

Both PCs can ping each other

Switch interfaces are active

Layer 1–3 connectivity verified
<br></br>

### Notes

Layer 2 must always be verified before Layer 3

Reinforces logical troubleshooting workflow



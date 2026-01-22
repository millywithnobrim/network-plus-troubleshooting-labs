# Lab 05 – Static Routing Troubleshooting

### Scenario

PC0, PC1, and PC2 are connected to a switch in VLAN 10.
The switch connects to Router0 via a trunk on Fa0/3.

Router0 is connected to Router1 using a transit network.
Router1 represents a remote internal network.

PCs can communicate within their local network and reach their default gateway, but cannot reach the remote network due to missing or incorrect static routing.
<br></br>

#### Intentional Faults

- No static route configured on Router0 to reach the remote network

- No return static route on Router1 back to VLAN 10

- Routers only know their directly connected networks
<br></br>

### Objective

- Diagnose routing failures between routers

- Reinforce static routing concepts

- Understand transit networks and return paths

- Restore end-to-end IPv4 connectivity using static routes
<br></br>

#### Step 1: Verify Host IP Configuration

On PC0, PC1, and PC2:
```
ipconfig /all
```

Expected Finding:
- PCs receive addresses in 192.168.10.0/24
- Default gateway is 192.168.10.1
<br></br>

Concept:
- PCs are correctly configured.
- Since local communication works, the issue is not DHCP or VLAN-related.
- Failure to reach remote networks indicates a Layer 3 routing issue.
<br></br>

#### Step 2: Verify VLAN and Trunk Configuration

On the switch:
```
show vlan brief
show interfaces trunk
```

Expected Result:
- Fa0/1, Fa0/2, Fa0/4 → VLAN 10
- Fa0/3 → trunk allowing VLAN 10
<br></br>

Concept:
- Layer 2 is functioning correctly.
- Traffic is successfully reaching Router0.
- Escalation to router-level troubleshooting is required.
<br></br>

#### Step 3: Inspect Router Interfaces

On Router0:
```
show ip interface brief
```

Expected:
- G0/0.10 → 192.168.10.1
- G0/1 → 10.10.10.1
<br></br>

On Router1:
```
show ip interface brief
```

Expected:
- G0/1 → 10.10.10.2
- Loopback0 → 10.10.20.1
<br></br>

Concept:
- Interfaces are up and correctly addressed.
- Transit network between routers is operational.
- Physical connectivity is confirmed.
<br></br>

#### Step 4: Test Router-to-Router Connectivity

From Router0:
```
ping 10.10.10.2
ping 10.10.20.1
```

Expected Finding:
- Ping to 10.10.10.2 succeeds
- Ping to 10.10.20.1 fails
<br></br>

Concept:
- Router0 can reach Router1 directly.
- Router0 does not know how to reach the remote network.
- Static routing is required for non-directly connected networks.
<br></br>

#### Step 5: Identify the Root Cause
- Router0 has no route to 10.10.20.0/24
- Router1 has no route back to 192.168.10.0/24
- Routing is not bidirectional
<br></br>

Concept:
- Static routes must exist on both routers
- Routing failures often occur due to missing return paths
<br></br>

#### Step 6: Add Static Route on Router0

On Router0:
```
config t
ip route 10.10.20.0 255.255.255.0 10.10.10.2
end
```
<br></br>

Concept:
- Router0 now forwards traffic for the remote network to Router1.
- The next-hop IP must be the directly connected router interface.
<br></br>

#### Step 7: Add Return Static Route on Router1

On Router1:
```
config t
ip route 192.168.10.0 255.255.255.0 10.10.10.1
end
```
<br></br>

Concept:
- Routing must be bidirectional.
- Without a return route, replies are dropped even if the forward path exists.
<br></br>

Step 8: Verify Connectivity

From Router0:
```
ping 10.10.20.1
```

From PC0:
```
ping 10.10.20.1
```
<br></br>

Expected Result:
- Pings succeed
- End-to-end communication is restored
<br></br>

### Expected Final Result

- Router0 and Router1 can reach each other
- Router0 knows how to reach the remote network
- Router1 knows how to return traffic to VLAN 10
- PCs can successfully ping remote network devices
<br></br>

### Success Criteria

- PCs can ping their default gateway

- Router0 can ping Router1

- PCs can ping 10.10.20.1

- Static routes exist on both routers

- Assessment Items pass grading
<br></br>

### Notes

- Static routing is required for non-directly connected networks

- Transit networks connect routers but do not provide routing logic

- Missing return routes are a common real-world outage cause

- Always verify router-to-router connectivity before troubleshooting hosts

- This lab reinforces Layer 3 escalation after VLANs and DHCP are confirmed working

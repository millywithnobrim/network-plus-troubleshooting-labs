# Lab 04 – Lab04-Inter-VLAN-Routing-Troubleshooting

### Scenario

PC0 and PC1 are in VLAN 10.
PC2 is in VLAN 20.

All PCs can communicate within their own VLAN, but devices in different VLANs cannot reach each other or their correct default gateways. The cause is incorrect trunking and router-on-a-stick configuration.
<br></br>

#### Intentional Faults

- Switch interface Fa0/3 (link to router) not configured as a trunk

- VLANs not explicitly allowed on the trunk

- Incorrect DHCP pool default gateway options
<br></br>

### Objective

- Diagnose inter-VLAN communication failures

- Reinforce trunk configuration concepts

- Correct router-on-a-stick implementation

- Restore end-to-end IPv4 connectivity
<br></br>

#### Step 1: Verify Host IP Configuration

On PC0:
```
ipconfig /all
```

Expected Finding:
- PC0, PC1: addresses in <b>192.168.10.0/24</b>
- PC2: address in <b>192.168.20.0/24</b>
- Default gateways may be incorrect or missing
<br></br>

Concept:
- IP addresses are correct, so the problem is not basic IPv4 configuration.
- Failure across VLANs usually indicates Layer 2 or routing issues.
<br></br>

#### Step 2: Verify VLAN Placement on the Switch

On the switch CLI:
```
show vlan brief
show interfaces status
```

Expected Result:
- Fa0/1 → VLAN 10 (PC0)
- Fa0/2 → VLAN 10 (PC1)
- Fa0/4 → VLAN 20 (PC2)
These ports are correctl assigned.
<br></br>

Concept:
- VLAN placement is correct, so the fault lies elsewhere.
- Proper VLANs alone do not provide routing – a router is required.
<br></br>

#### Step 3: Check Trunk Status

On the switch:
```
show interfaces trunk
```

Expected Finding:
- No trunk ports are listed
<br></br>

Concept:
- Without a trunk, VLAN 20 traffic never reaches the router.
- Router-on-a-stick requires:
  - Switch trunk port
  - Matching router subinterfaces
  - Correct encapsulation
<br></br>

#### Step 4: Inspect Router Interface

On the router CLI:
```
show ip iterface brief
show running-config
```

Expected Finding:
- Interface g0/0 is up
- Subinterfaces missing or using wrong VLAN IDs
- DHCP pools handing out wrong gateway
<br></br>

Concept:
- Each VLAN must map to a router subinterface with matching VLAN ID.
<br></br>

#### Step 5: Correct the Switch Trunk Configuration
```
config t
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown
end
```
<br></br>

Concept:
- The trunk link carries frames tagged with VLAN IDs.
- Explicit allowed VLAN list is required so the grader counts it as correct.
<br></br>

#### Step 6: Correct Router-on-a-Stick (if misconfigured)

On the router:
```
config t
interface g0/0
 no ip address
 no shutdown
```
Create subinterfaces:
```
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
end
```
<br></br>

Concept:
- A physical router interface cannot use the same subnet as a subinterface.
- Subinterfaces terminate VLANs and act as their gateways.
- Overlapping IPs cause the “subinterface overlaps with interface” error.
<br></br>

#### Step 7: Fix DHCP Pools

Correct DHCP configuration so gateways match subinterfaces:
```
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1

ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
```

Expected Result:
- PC0 receives a valid DHCP-assigned IPv4 address.

Concept:
- DHCP must advertise the correct gateway for each VLAN.
- If VLAN 20 PCs receive a 192.168.10.1 gateway, inter-VLAN pings will still fail.
<br></br>

#### Step 8: Renew IP Addresses (If Needed)
```
ipconfig /release
ipconfig /renew
ipconfig /all
```
<br></br>

Concept:
- APIPA occurs when DHCP broadcasts fail or the PC was blocked by port security.
- After trunk and routing are fixed, DHCP must be renewed.
<br></br>

#### Step 9: Verify Connectivity
From each PC:
```
ping 192.168.10.1
ping 192.168.20.1
ping <PC in other VLAN>
```
<br></br>
From the switch:
```
show mac address-table
show interfaces trunk
```
All devices should now communicate successfully.
<br></br>

### Expected Final Result

- VLAN 10 and VLAN 20 traffic reaches the router through trunk Fa0/3
- Router subinterfaces provide correct gateways
- PCs obtain IPs via DHCP with proper gateways
- Inter-VLAN ping tests succeed
<br></br>

### Success Criteria

- PC0, PC1, and PC2 can all ping each other

- PCs can ping their respective default gateways

- Trunk Fa0/3 shows VLANs 10 and 20 explicitly allowed

- Assessment Items in Packet Tracer grade as correct
<br></br>

### Notes

- Inter-VLAN communication requires both Layer 2 trunks and Layer 3 subinterfaces

- Always verify switch trunks before router configuration

- Overlapping IP addressing on physical interfaces breaks router-on-a-stick

- DHCP misconfiguration can mimic routing failure even when subinterfaces are correct

- Focus on why PC0 cannot communicate, not just on executing commands

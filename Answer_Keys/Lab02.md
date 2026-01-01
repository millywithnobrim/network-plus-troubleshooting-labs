# Lab 02 – DHCP Troubleshooting Answer

### Scenario

PC0 cannot obtain an IP address and displays an APIPA address.
PC1 is functioning normally.
<br></br>

#### Intentional faults:

- PC0 in wrong VLAN or on a shutdown interface

- DHCP broadcasts cannot reach the server

-   DHCP default gateway does not match router G0/0
<br></br>

### Objective

- Diagnose DHCP issues and APIPA addresses

- Reinforce VLAN and switch port concepts

- Practice structured troubleshooting
<br></br>

#### Step 1: Verify Host IP Configuration

On PC0 and PC1:
```
ipconfig /all
```

Expected Finding:

- PC0 has 169.254.x.x (APIPA)

- PC1 has valid DHCP-assigned IP

Concept:
- APIPA indicates DHCP failure.
<br></br>

#### Step 2: Verify VLAN Assignment

On the switch:
```
show vlan brief
show interfaces status
```

Expected Finding:

- PC0’s port may be in the wrong VLAN

- Interface may be shutdown
<br></br>

#### Step 3: Correct VLAN / Interface
```
conf t
interface fa0/1
 switchport mode access
 switchport access vlan 10
 no shutdown
```

Concept:
- Correct VLAN placement is required for DHCP broadcasts to reach the router.
<br></br>

#### Step 4: Verify DHCP Pool Configuration

On the router:
```
show run | section dhcp
```
Expected Finding:

- DHCP pool has an incorrect default gateway.
<br></br>

Concept:
- Correct VLAN placement is required for DHCP broadcasts to reach the router.
<br></br>

#### Step 5: Correct DHCP Default Gateway

On the router:
```
conf t
ip dhcp pool VLAN10
no default-router 192.168.10.254
default-router 192.168.10.1
end
```
<br></br>

Concept:
- DHCP clients install the `default-router` value as their gateway.
  
- If it does not match G0/0, hosts may get an IP but cannot route traffic.
<br></br>


#### Step 4: Renew DHCP Lease

On PC0:
```
ipconfig /release
ipconfig /renew
```
<br></br>

#### Step 5: Verify Connectivity
```
ipconfig
ping 192.168.10.1
ping PC1-IP
```
<br></br>

### Success Criteria:

- PC0 receives a valid DHCP address

- PC0 can ping the default gateway and PC1

- Lab grading checks pass
<br></br>

### Notes
- APIPA ≠ bad NIC  
- A working IP with a wrong gateway still breaks connectivity  
- Always verify **Layer 2 (VLAN)** before **Layer 3 (DHCP/gateway)** 

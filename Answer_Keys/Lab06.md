# Lab 06 – ACL Troubleshooting (Static Routing)

### Scenario

PC0, PC1, and PC2 are connected to VLAN 10 and can successfully reach their default gateway on Router0.

Router0 is connected to Router1, which represents a remote internal network.

Although VLANs, trunking, DHCP, and static routing are correctly configured, hosts on VLAN 10 cannot reach the remote network. The issue is caused by an incorrect extended ACL applied on Router0.
<br></br>

#### Intentional Faults

- Extended ACL blocks legitimate VLAN 10 traffic

- Missing or incorrect permit statements

- Implicit deny dropping packets

- ACL applied to the correct interface but with incorrect logic
<br></br>

### Objective

- Diagnose ACL-based connectivity failures

- Understand ACL processing order and implicit deny behavior

- Verify ACL placement and direction

- Restore secure end-to-end IPv4 connectivity
<br></br>

#### Step 1: Verify Host IP Configuration

On PC0, PC1, and PC2:
```
ipconfig /all
```

Expected Result:
- PCs receive addresses in 192.168.10.0/24
- Default gateway is 192.168.10.1
<br></br>

#### Step 2: Verify Local Connectivity

```
ping 192.168.10.1
```

Expected Result:
- Ping succeeds
<br></br>

Concept:
- Confirms VLAN, trunking, and default gateway are working
<br></br>

#### Step 3: Test Remote Connectivity

```
ping 10.10.20.1
```

Expected Result:
- Ping fails
<br></br>

Concept:
- Indicates routing exists but traffic is being filtered
<br></br>

#### Step 4: Verify Router Connectivity

From Router0:
```
ping 10.10.10.2
```

Expected Result:
- Ping succeeds
<br></br>

Concept:
- Confirms routing between routers is operational
<br></br>

#### Step 5: Inspect ACL Configuration

From Router0:
```
show access-lists
show running-config interface g0/1
```
<br></br>

Expected Finding:
- ACL exists
- VLAN 10 traffic is not explicitly permitted
- Implicit deny is blocking traffic
<br></br>

#### Step 6: Correct the ACL Configuration

Rebuild the ACL to allow VLAN 10 traffic to the remote network:
```
conf t
no access-list 100
access-list 100 permit ip 192.168.10.0 0.0.0.255 10.10.20.0 0.0.0.255
access-list 100 deny ip any any
end
```
<br></br>

#### Step 7: Verify ACL Placement

```
show running-config interface g0/1

```
<br></br>
```
interface g0/1
 ip access-group 100 out

```
<br></br>

Concept:
- Extended ACLs must be placed and ordered correctly to function
<br></br>

Step 8: Verify End-to-End Connectivity

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

- VLAN 10 hosts can reach the remote network
- Router0 and Router1 communicate successfully
- ACL security remains enforced
- No unnecessary permit statements exist
<br></br>

### Success Criteria

- PCs can ping 10.10.20.1

- Router0 can ping Router1

- ACL explicitly permits VLAN 10 traffic

- ACL includes a deny-any-any statement

- ACL applied to the correct interface and direction

- Assessment Items pass grading
<br></br>

### Notes

- ACL issues often resemble routing failures

- Implicit deny is a common real-world outage cause

- Security controls should be corrected, not removed

- Always verify ACL order, logic, and placement

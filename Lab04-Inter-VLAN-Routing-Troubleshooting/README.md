<html contenteditable="true"><head></head><body>

<h2>Lab 04 – Inter-VLAN Routing (Router-on-a-Stick) Troubleshooting</h2>

<h3>Scenario</h3>
<p>PCs are connected to multiple VLANs, but devices in different VLANs cannot communicate.
  
The switch connects to a router using a <b>trunk link</b>, however misconfigurations in <b>VLAN assignment, trunking, or router-on-a-stick configuration</b> are preventing inter-VLAN communication.</p>

<hr>

<h3>Objective</h3>
<ul>
  <li>Identify and correct VLAN assignment issues</li>
  <li>Diagnose trunk misconfigurations between the switch and router</li>
  <li>Troubleshoot router-on-a-stick subinterface configuration</li>
  <li>Restore full inter-VLAN connectivity and default gateway access</li>
</ul>

<hr>

<h3>CompTIA Network+ Objective Mapping</h3>

<h4>Domain 1.0 – Networking Fundamentals</h4>
<ul>
  <li>1.4: Configure IPv4 addressing and subnet masks</li>
  <li>1.8: Apply VLAN and switch port configuration concepts</li>
</ul>

<h4>Domain 2.0 – Network Implementations</h4>
<ul>
  <li>2.1: Configure switching components (access ports, port security</li>
  <li>2.2: Configure routing technologies (inter-VLAN routing)</li>
</ul>

<h4>Domain 5.0 – Network Troubleshooting</h4>
<ul>
  <li>5.1: Troubleshoot common network connectivity issues:
    <ul>
      <li>Incorrect VLAN assignment</li>
      <li>Trunk misconfiguration</li>
      <li>Missing or incorrect default gateway</li>
    </ul>
  </li>
  <li>5.3: Use appropriate network diagnostic tools (<code>ping</code>, <code>show ipconfig</code>, <code>show interfaces</code>, <code>show running-config</code>)</li>
</ul>

<hr>

<h3>Tasks</h3>
<ol>
  <li>
    Use the <b>Command Prompt</b> on PC0, PC1, and PC2 to check IP configuration (<code>ipconfig /all</code>)<br>
Test connectivity:    
    <pre>
         <code>ping &ltdefault-gateway></code>
         <code>ping &ltsame-VLAN PC></code>
         <code>ping &ltdifferent-VLAN PC></code>
    </pre>
  </li>
  <li>
    Verify VLAN Assignments on the Switch:
    <ul>
      <li><code>show vlan brief</code></li>
      <li><code>show interfaces status</code></li>
    </ul>
    <p>Expected VLAN placement:</p>
    <ul>
      <li>PC0,PC1 = Vlan 10</li>
      <li>PC2 = Vlan 20</li>
    </ul>
  </li>
  <li>
    Inspect Trunk Configuration (Switch → Router):
    <p>The trunk link is on Fa0/3. <code>showinterfaces trunk</code></p>
    <p>Verify: </p>
    <ul>
      <li>Interface is in <b>trunk mode</b></li>
      <li>VLANs <b>10 and 20</b> are explicitly allowed</li>
    </ul>
  </li>
  <p><pre>Assessment Note:
      Even if the switch states VLANs are allowed by default, you must           explicitly configure allowed VLANs for grading to pass.
  </pre></p>
  <li>Inspect Router-on-a-Stick Configuration</li>
    <p>On the router: <code>show running-config</code></p>
    <p>Verify:</p>
      <ul>
        <li>Subinterfaces exist for each VLAN</li>
        <li>Correct <code>encapsulation dot1Q</code> values</li>
        <li>Correct IP addressing per VLAN</li>
      </ul>
  <p>Example: </p>
  <pre>
         <code>
               interface g0/0.10
               encapsulation dot1Q 10
               ip address 192.168.10.1 255.255.255.0
         </code>
         <code>
               interface g0/0.20
               encapsulation dot1Q 20
               ip address 192.168.20.1 255.255.255.0
         </code>
    </pre>
  <li>Identify the Root Cause</li>
  <p>Possible issues include:</p>
      <ul>
        <li>Access ports assigned to the wrong VLAN</li>
        <li>Trunk not configured or VLANs not allowed</li>
        <li>Missing or incorrect router subinterfaces</li>
        <li>Incorrect or missing DHCP pool configuration</li>
      </ul>
  <li>Correct the Configuration</li>
  <p>Using CLI: </p>
   <ul>
        <li>Assign correct VLANs to PC access ports</li>
        <li>Configure Fa0/3 as a trunk and explicitly allow VLANs 10 and 20</li>
        <li>Correct router subinterfaces for VLAN 10 and VLAN 20</li>
      </ul>
  <li>Renew DHCP (If Needed)</li>
    <p>If any PC shows an APIPA address (169.254.x.x): </p>
    <pre>
      <code>ipconfig /release</code>
      <code>ipconfig /renew</code>
    </pre>
  <li>Verify Connectivity</li>
    <p>Successful completion means: </p>
   <ul>
        <li>PCs can ping their default gateways</li>
        <li>PCs in different VLANs can communicate</li>
        <li>Inter-VLAN routing functions correctly</li>
      </ul>
</ol>
  
<hr>

<h3>Success Criteria</h3>
<ul>
  <li>All PCs have valid IP addresses.</li>
  <li>Trunk link is correctly configured and graded as correct.</li>
  <li>Router-on-a-stick is properly configured.</li>
  <li>End-to-end inter-VLAN connectivity is restored.</li>
  <li>Packet Tracer assessment checks pass.</li>
</ul>

<hr>

<h3>Restrictions</h3>
<ul>
  <li>All troubleshooting and verification must be done using CLI tools.</li>
  <li>Do not modify physical connections.</li>
  <li>Desktop IP Configuration can only be used to check connectivity or refresh DHCP.</li>
</ul>

<hr>

<h3>Recommended Commands</h3>
<ul>
  <li><code>ipconfig</code></li>
  <li><code>ipconfig /release</code></li>
  <li><code>ipconfig /renew</code></li>
  <li><code>ping &lt;IP&gt;</code></li>
  <li><code>show vlan brief</code></li>
  <li><code>show interfaces status</code></li>
  <li><code>show interfaces trunk</code></li>
  <li><code>show running-config</code></li>
  <li><code>show port-security</code></li>
</ul>

<hr>

<h3>Notes</h3>
<ul>
  <li>This lab simulates a <b>real-world inter-VLAN routing troubleshooting scenario</b>.</li>
  <li>Always verify Layer 2 <b>(VLANs, trunks)</b> before troubleshooting <b>Layer 3 (routing)</b></li>
  <li>Explicit trunk configuration is required for Packet Tracer grading</li>
</ul>

</body></html>


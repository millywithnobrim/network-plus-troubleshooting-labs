<html contenteditable="true"><head></head><body>

<h2>Lab 03 – Switch Port Security Troubleshooting</h2>

<h3>Scenario</h3>
<p>PC0 cannot communicate on the network. PC1 is a working reference host.<br>
The switch has port security configured incorrectly, preventing PC0 from connecting.<br>
Your task is to <b>identify and correct switch port security issues</b> so that PC0 can communicate properly.</p>

<p><b>Hint:</b> If PC0 shows an APIPA address (169.254.x.x) after correcting port security, use the Command Prompt to refresh the DHCP lease.</p>

<hr>

<h3>Objective</h3>
<ul>
  <li>Practice diagnosing switch port security misconfigurations</li>
  <li>Reinforce understanding of MAC addresses, violation modes, and secure access ports</li>
  <li>Develop troubleshooting skills aligned with CompTIA Network+ objectives</li>
</ul>

<hr>

<h3>CompTIA Network+ Objective Mapping</h3>

<h4>Domain 1.0 – Networking Fundamentals</h4>
<ul>
  <li>1.5: Compare and contrast network ports and interfaces</li>
  <li>1.8: Apply VLAN and switch port configuration concepts</li>
</ul>

<h4>Domain 2.0 – Network Implementations</h4>
<ul>
  <li>2.1: Configure switching components (access ports, port security)</li>
</ul>

<h4>Domain 5.0 – Network Troubleshooting</h4>
<ul>
  <li>5.1: Troubleshoot common network connectivity issues:
    <ul>
      <li>Disabled interfaces due to security violations</li>
      <li>Misconfigured MAC addresses</li>
      <li>Unauthorized devices</li>
    </ul>
  </li>
  <li>5.3: Use appropriate network diagnostic tools (<code>ping</code>, <code>show mac address-table</code>, <code>show port-security</code>)</li>
</ul>

<hr>

<h3>Tasks</h3>
<ol>
  <li>
    Use the <b>Command Prompt</b> on PC0 and PC1 to check IP configuration (<code>ipconfig</code>) and ping test connectivity.<br>
    If PC0 shows APIPA (169.254.x.x) after fixing port security, run:
    <pre><code>ipconfig /release
ipconfig /renew</code></pre>
    Verify the new IP and default gateway with <code>ipconfig /all</code>.
  </li>
  <li>
    Inspect switch port security status using the switch CLI:
    <ul>
      <li><code>show port-security</code></li>
      <li><code>show interfaces status</code></li>
      <li><code>show mac address-table</code></li>
    </ul>
  </li>
  <li>
    Identify the root cause preventing PC0 from connecting:
    <ul>
      <li>MAC address not allowed</li>
      <li>Violation shutdown mode</li>
      <li>Sticky MAC misconfigured</li>
    </ul>
  </li>
  <li>Correct the port security configuration to allow PC0 access.</li>
  <li>Verify connectivity with <code>ping</code> and confirm PC0’s MAC address appears in the port security table.</li>
</ol>

<hr>

<h3>Success Criteria</h3>
<ul>
  <li>PC0 can communicate with PC1 and the default gateway.</li>
  <li>Port security is properly configured for PC0’s port.</li>
  <li>The switch interface is active (not in shutdown due to violations).</li>
  <li>Grading checks (if using Packet Tracer Activity Wizard) pass.</li>
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
  <li><code>show interfaces status</code></li>
  <li><code>show port-security</code></li>
  <li><code>show mac address-table</code></li>
</ul>

<hr>

<h3>Notes</h3>
<ul>
  <li>This lab simulates a <b>real-world switch port security troubleshooting scenario</b>.</li>
  <li>Focus on understanding <b>why PC0 cannot communicate</b>, not just on changing commands.</li>
  <li>All steps align with <b>Network+ objectives</b>.</li>
</ul>

</body></html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
</head>
<body>

  <h1>🔓 Server-Side Request Forgery (SSRF) — A Hidden Web Attack</h1>

  <h2>📌 For Beginners: What is SSRF?</h2>
  <p>
    Imagine you’re using a food delivery app that fetches restaurant images from an external website. The app allows users to input a URL to load an image. Now, an attacker manipulates this URL to access internal company systems or even steal sensitive data from the server!
  </p>
  <p>
    This type of attack is called <strong>Server-Side Request Forgery (SSRF)</strong>. It tricks the server into making requests to unintended or restricted locations, often leading to data leaks, unauthorized access, or internal system exposure.
  </p>
  <div class="highlight">
    💡 Think of SSRF like tricking a delivery person into entering a restricted area by giving them a fake delivery address!
  </div>

  <h2>🔍 Technical Explanation of SSRF</h2>
  <p>SSRF is a web security vulnerability where an attacker forces a server to make requests on its behalf. Since these requests originate from the server itself, attackers can abuse trusted connections to:</p>
  <ul>
    <li>✔️ Access internal networks not directly reachable from the internet</li>
    <li>✔️ Extract sensitive data from backend systems</li>
    <li>✔️ Scan internal infrastructure to identify services and vulnerabilities</li>
    <li>✔️ Bypass security controls like firewalls or VPN restrictions</li>
    <li>✔️ Abuse cloud metadata services to gain credentials</li>
  </ul>
  <p>
    SSRF is dangerous because the targeted server acts as a proxy, unknowingly helping the attacker execute malicious requests.
  </p>

  <h2>🚨 Real-World SSRF Attack Example</h2>
  <h3>🌍 Scenario: SSRF in a Cloud Application</h3>
  <ol>
    <li>A cloud-based web app allows users to upload profile pictures via a URL.</li>
    <li>The app’s backend fetches the image from the provided URL.</li>
    <li>An attacker inputs a special internal URL (e.g., <code>http://169.254.169.254/latest/meta-data/</code>).</li>
    <li>The server, assuming it's fetching an image, accesses the cloud metadata service and exposes sensitive credentials!</li>
  </ol>
  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> The attacker bypasses security controls and extracts internal cloud access tokens, leading to a complete system takeover!
  </div>

  <h2>🛡️ How to Prevent SSRF Attacks?</h2>
  <p>Web developers must apply strict security measures to prevent SSRF attacks.</p>

  <h3>✔️ 1. Restrict External Requests</h3>
  <ul>
    <li>Allow the server to fetch content only from trusted sources</li>
    <li>Implement an allowlist (whitelist) of permitted domains</li>
  </ul>

  <h3>✔️ 2. Block Internal IP Address Access</h3>
  <ul>
    <li>Prevent requests to internal IP ranges like <code>127.0.0.1</code>, <code>169.254.169.254</code>, and <code>192.168.0.0/16</code></li>
    <li>Use network segmentation to separate internal and external requests</li>
  </ul>

  <h3>✔️ 3. Validate & Sanitize User Input</h3>
  <ul>
    <li>Deny direct user input as request URLs</li>
    <li>Use regular expressions to block malicious URL patterns</li>
  </ul>

  <h3>✔️ 4. Use Web Application Firewalls (WAF)</h3>
  <ul>
    <li>Deploy a WAF to monitor and block SSRF attempts</li>
    <li>Set up rate-limiting to prevent brute-force SSRF attacks</li>
  </ul>

  <h3>✔️ 5. Disable Unnecessary Server Features</h3>
  <ul>
    <li>Block unused HTTP methods like PUT and DELETE</li>
    <li>Disable cloud metadata APIs if not required</li>
  </ul>

  <h3>✔️ 6. Least Privilege Access Control</h3>
  <ul>
    <li>Restrict server permissions to only allow necessary outbound requests</li>
    <li>Use IAM roles with limited privileges in cloud environments</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Server-Side Request Forgery (SSRF) is a powerful attack that exploits trust between a server and its internal services. It can lead to data breaches, infrastructure exposure, and unauthorized access to internal systems.
  </p>
  <p>
    💡 Developers must implement strict validation and network restrictions, while security teams should monitor for suspicious outbound requests!
  </p>
  <p>
    By using allowlists, input validation, firewalls, and access controls, we can reduce the risk of SSRF attacks.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

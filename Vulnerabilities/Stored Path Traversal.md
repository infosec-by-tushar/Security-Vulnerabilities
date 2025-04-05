<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>📂 Stored Path Traversal — The Persistent Exploit Hiding in Your System</h1>

  <h2>📌 For Beginners: What is Stored Path Traversal?</h2>
  <p>
    Imagine a file cabinet where every user can access only their designated folder. But what if someone secretly plants a note inside the cabinet that, when read, redirects employees to another folder containing sensitive company documents? This is how Stored Path Traversal works in web applications.
  </p>
  <div class="highlight">
    💡 <strong>Stored Path Traversal</strong> is an attack where an attacker injects malicious file paths into stored data, causing the application to access unauthorized files whenever that data is used later.
  </div>

  <h2>🔍 Technical Explanation of the Risk</h2>
  <p>
    Unlike traditional path traversal, which involves sending <code>../</code> sequences in a request, stored path traversal occurs when an attacker saves malicious file paths into the system, which later gets executed by another function.
  </p>

  <h2>🚨 The Risk? Attackers can:</h2>
  <ul>
    <li>📂 Access restricted files (e.g., <code>/etc/passwd</code>, <code>config.php</code>, <code>database.env</code>).</li>
    <li>✍️ Modify system-critical files that impact application behavior.</li>
    <li>🚀 Execute unauthorized scripts leading to Remote Code Execution (RCE).</li>
    <li>🕵️ Extract sensitive user data from backup directories or hidden files.</li>
  </ul>

  <h2>🚨 Real-World Example: Stored Path Traversal in a File Management System</h2>
  <h3>🔍 What Happened?</h3>
  <ol>
    <li>A web application allows users to upload profile pictures and stores the file path in a database.</li>
    <li>An attacker uploads a file with a manipulated path, such as:
      <br><code>../../../../var/www/html/admin/config.php</code>
    </li>
    <li>When an admin views the uploaded file, the system retrieves the malicious path from the database and tries to load the file.</li>
    <li>🚨 <strong>Result?</strong> The attacker gains access to sensitive admin configurations.</li>
  </ol>
  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> If an application stores and later processes user-supplied file paths without validation, attackers can exploit it for unauthorized access.
  </div>

  <h2>🛡️ How to Prevent Stored Path Traversal?</h2>

  <h3>✔️ 1. Validate and Sanitize User Inputs</h3>
  <ul>
    <li>✅ Reject any file paths containing <code>../</code>, <code>/</code>, or <code>\</code> sequences.</li>
    <li>✅ Use whitelisting to allow only specific file paths.</li>
  </ul>

  <h3>✔️ 2. Store File Metadata Instead of File Paths</h3>
  <ul>
    <li>✅ Instead of saving absolute paths, store hashed filenames or unique IDs.</li>
    <li>✅ Example:
      <br><code>/uploads/secure/abc123xyz.jpg</code> — <code>abc123xyz.jpg</code> is a hashed filename or UUID.
    </li>
  </ul>

  <h3>✔️ 3. Implement Secure Access Controls</h3>
  <ul>
    <li>✅ Restrict access to critical directories using OS-level permissions.</li>
    <li>✅ Enforce least privilege principles for file access.</li>
  </ul>

  <h3>✔️ 4. Use a Secure File Handling Mechanism</h3>
  <ul>
    <li>✅ Restrict uploaded files to a dedicated directory (e.g., <code>/uploads</code>).</li>
    <li>✅ Prevent file retrieval outside the allowed directory.</li>
  </ul>

  <h3>✔️ 5. Perform Security Testing</h3>
  <ul>
    <li>✅ Use tools like Burp Suite, OWASP ZAP to identify stored path traversal vulnerabilities.</li>
    <li>✅ Conduct manual penetration testing to check if malicious paths are executed.</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Stored Path Traversal is a dangerous vulnerability because it allows attackers to store malicious paths that can be executed later, leading to data exposure, file manipulation, or even complete system compromise.
  </p>
  <p>
    💡 Developers must enforce strict input validation, secure file storage, and strong access controls to prevent stored path traversal attacks.
  </p>
  <p>
    By sanitizing inputs, storing metadata instead of raw paths, and restricting file access, we can eliminate this persistent threat and ensure application security.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

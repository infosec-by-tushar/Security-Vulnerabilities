<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>💀 SQL Injection (SQLi) – The Silent Database Killer</h1>

  <h2>👶 For Beginners: What is SQL Injection?</h2>
  <p>
    Imagine a login page where you enter your username and password. If the website directly processes your input without validation, an attacker could enter:
  </p>
  <pre><code>' OR '1'='1</code></pre>
  <p>
    This tricks the database into thinking the password check is always true, granting access without needing a real password! 😱
  </p>

  <p>
    💡 <strong>SQL Injection (SQLi)</strong> is an attack that allows hackers to manipulate a website’s database by injecting malicious SQL queries.
  </p>

  <h2>🔍 Technical Explanation of SQL Injection</h2>
  <p>
    SQL Injection happens when unsanitized user input is embedded into SQL queries, allowing attackers to:
  </p>

  <ul>
    <li>✔️ <strong>Bypass Authentication</strong> – Log in as an admin without knowing the credentials.</li>
    <li>✔️ <strong>Extract Sensitive Data</strong> – Steal usernames, passwords, emails, or credit card details.</li>
    <li>✔️ <strong>Modify or Delete Data</strong> – Change account balances, delete user records, or alter sensitive information.</li>
    <li>✔️ <strong>Take Full Control</strong> – In some cases, attackers can gain root access to the database server.</li>
  </ul>

  <div class="highlight">
    🚨 <strong>SQL Injection</strong> is listed in the OWASP Top 10 and has been responsible for major data breaches worldwide!
  </div>

  <h2>🚨 Real-World SQL Injection Attack Example</h2>
  <h3>🏦 Scenario: Bypassing Login Authentication</h3>
  <ol>
    <li>A vulnerable login system runs the following query:</li>
  </ol>
  <pre><code>SELECT * FROM users WHERE username = 'admin' AND password = 'password';</code></pre>
  <ol start="2">
    <li>An attacker enters this as the username:</li>
  </ol>
  <pre><code>' OR '1'='1</code></pre>
  <ol start="3">
    <li>The SQL query now becomes:</li>
  </ol>
  <pre><code>SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';</code></pre>
  <ol start="4">
    <li>Since '1'='1' is always TRUE, the database grants access without a password! 🔥</li>
  </ol>

  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> If the website used prepared statements, this attack wouldn’t work!
  </div>

  <h2>🛡️ How to Prevent SQL Injection?</h2>

  <h3>✔️ 1. Use Prepared Statements (Parameterized Queries)</h3>
  <ul>
    <li>✅ Always use parameterized queries instead of directly inserting user input into SQL statements.</li>
    <li><strong>Vulnerable Query:</strong></li>
  </ul>
  <pre><code>query = "SELECT * FROM users WHERE username = '" + user_input + "';"</code></pre>
  <ul>
    <li><strong>Secure Query Using Prepared Statements:</strong></li>
  </ul>
  <pre><code>cursor.execute("SELECT * FROM users WHERE username = ?", (user_input,))</code></pre>

  <h3>✔️ 2. Use Stored Procedures</h3>
  <ul>
    <li>✅ Instead of executing raw SQL queries, use predefined stored procedures in the database.</li>
  </ul>

  <h3>✔️ 3. Validate & Sanitize Input</h3>
  <ul>
    <li>✅ Reject input containing SQL keywords (SELECT, DROP, UNION, --, ' OR '1'='1')</li>
    <li>✅ Use allowlists for expected input formats (e.g., numbers only for IDs).</li>
  </ul>

  <h3>✔️ 4. Implement Least Privilege for Database Users</h3>
  <ul>
    <li>✅ Use a restricted database account with limited permissions.</li>
    <li>✅ Prevent the web application from executing DROP, DELETE, UPDATE unless necessary.</li>
  </ul>

  <h3>✔️ 5. Enable Web Application Firewalls (WAFs)</h3>
  <ul>
    <li>✅ A WAF can detect and block SQLi attempts before they reach the database.</li>
  </ul>

  <h3>✔️ 6. Avoid Displaying Detailed Error Messages</h3>
  <ul>
    <li>✅ Generic errors prevent attackers from learning about database structure.</li>
    <li><strong>Vulnerable:</strong></li>
  </ul>
  <pre><code>SQL Error: Incorrect syntax near '1'.</code></pre>
  <ul>
    <li><strong>Secure:</strong></li>
  </ul>
  <pre><code>Invalid credentials. Please try again.</code></pre>

  <h2>🚀 Final Thoughts</h2>
  <p>
    SQL Injection is one of the most dangerous web vulnerabilities, allowing attackers to steal data, manipulate databases, and gain unauthorized access.
  </p>
  <p>
    💡 Developers must use prepared statements, validate input, and restrict database permissions to prevent SQLi attacks!
  </p>
  <p>
    By implementing secure coding practices, proper authentication, and WAF protection, we can eliminate SQL Injection risks and protect sensitive data.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

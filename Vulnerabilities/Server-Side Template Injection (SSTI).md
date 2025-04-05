<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🖥️ Server-Side Template Injection (SSTI) — A Silent Yet Dangerous Web Exploit</h1>

  <h2>📌 For Beginners: What is SSTI?</h2>
  <p>
    Imagine you’re using a website that allows users to customize their profile by entering text. But instead of just displaying your name, the website executes whatever you enter as code! 😱
  </p>

  <p>
    💡 <strong>Server-Side Template Injection (SSTI)</strong> occurs when an attacker injects malicious input into a template engine, causing the server to execute unintended commands.
  </p>

  <h2>🔍 Technical Explanation of the Risk</h2>
  <p>
    Many modern web applications use template engines (like Jinja2, Twig, Freemarker, or Pug) to dynamically render web pages.
  </p>

  <div class="highlight">
    🚨 <strong>The Risk?</strong> If user input is not properly sanitized before being processed by the template engine, an attacker can:
  </div>

  <ul>
    <li>🏴‍☠️ Execute arbitrary code on the server (Remote Code Execution — RCE).</li>
    <li>🛠️ Read sensitive files, such as database credentials or API keys.</li>
    <li>📡 Take full control of the application, leading to data breaches and system compromise.</li>
  </ul>

  <h2>🚨 Real-World Example: SSTI in a Flask-Jinja2 Application</h2>
  <h3>🔍 What Happened?</h3>
  <ol>
    <li>A vulnerable web application uses the Jinja2 template engine in Flask:</li>
    <div class="highlight">
      <code>
from flask import Flask, request, render_template_string<br>
app = Flask(__name__)<br><br>

@app.route("/greet")<br>
def greet():<br>
    name = request.args.get("name")<br>
    return render_template_string("Hello, " + name)
      </code>
    </div>
    <li>The application directly injects user input (name) into the template without sanitization.</li>
    <li>An attacker enters the following payload:</li>
    <div class="highlight">
      <code>{{ 7*7 }}</code>
    </div>
    <li>Instead of displaying “{{ 7*7 }}”, the server processes the template logic and returns:</li>
    <div class="highlight">
      <code>49</code>
    </div>
    <li>🚨 Result? This confirms SSTI exists! Now, an attacker can execute system commands, like:</li>
    <div class="highlight">
      <code>{{ self.__class__.__mro__[1].__subclasses__()[400]('/etc/passwd').read() }}</code>
    </div>
    <li>This could leak sensitive files or even allow remote code execution (RCE)!</li>
  </ol>

  <div class="highlight">
    💡 <strong>Key Takeaway:</strong> If a template engine processes user input directly, attackers can inject malicious payloads and take control of the system.
  </div>

  <h2>🛡️ How to Prevent SSTI Attacks?</h2>

  <h3>✔️ 1. Avoid Direct User Input in Templates</h3>
  <ul>
    <li>✅ Do not pass user input directly into template rendering functions.</li>
    <li>✅ Use context variables instead.</li>
  </ul>
  <div class="highlight">
    🚫 Vulnerable Code:
  </div>
  <div class="example">
    <code>
render_template_string("Hello, " + name)
    </code>
  </div>

  <div class="highlight">
    ✅ Secure Approach:
  </div>
  <div class="example">
    <code>
render_template_string("Hello, {{ user }}", user=name)
    </code>
  </div>

  <h3>✔️ 2. Enable Sandboxing in Template Engines</h3>
  <ul>
    <li>✅ Many template engines provide sandboxing options to prevent dangerous function execution.</li>
    <li>✅ Example for Jinja2:</li>
    <div class="highlight">
      <code>
from jinja2.sandbox import SandboxedEnvironment<br>
env = SandboxedEnvironment()
      </code>
    </div>
  </ul>

  <h3>✔️ 3. Use Strict Input Validation</h3>
  <ul>
    <li>✅ Restrict user input to expected values only (e.g., letters and numbers).</li>
    <li>✅ Use allowlists instead of blocklists for filtering input.</li>
  </ul>

  <h3>✔️ 4. Disable Unnecessary Template Features</h3>
  <ul>
    <li>✅ If the template engine supports executing functions, disable this feature unless required.</li>
    <li>✅ Example: In Twig (PHP), disable automatic function calls.</li>
  </ul>

  <h3>✔️ 5. Implement a Web Application Firewall (WAF)</h3>
  <ul>
    <li>✅ A WAF can detect and block SSTI attack patterns before they reach the server.</li>
  </ul>

  <h3>✔️ 6. Keep Your Template Engine Updated</h3>
  <ul>
    <li>✅ Regularly update your template engine to patch known vulnerabilities.</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Server-Side Template Injection (SSTI) is a critical vulnerability that can lead to remote code execution, data leaks, and full server compromise.
  </p>
  <p>
    💡 Developers must validate user input, restrict template engine capabilities, and avoid unsafe rendering practices to prevent SSTI attacks.
  </p>
  <p>
    By following secure coding practices, enabling sandboxing, and implementing input validation, we can effectively mitigate SSTI risks and keep applications safe.
  </p>

  <h3>🔐 Stay Secure, Stay Vigilant!</h3>

</body>
</html>

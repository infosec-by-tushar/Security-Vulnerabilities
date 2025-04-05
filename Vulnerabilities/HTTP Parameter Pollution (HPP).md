<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🧪 HTTP Parameter Pollution (HPP) – The Hidden Query Hack</h1>

  <h2>👶 For Beginners: What is HTTP Parameter Pollution?</h2>
  <p>
    HTTP Parameter Pollution (HPP) is a web attack where an attacker injects multiple parameters with the same name in a single HTTP request to confuse the server or bypass security controls.
  </p>
  <p>
    💡 Think of it like filling a form that asks for your email, but you secretly submit two emails — one legit and one malicious. The server may get confused and process the wrong one.
  </p>

  <h2>🌐 What Are HTTP Parameters?</h2>
  <p>HTTP parameters are the key-value pairs in:</p>
  <ul>
    <li>URLs: <code>example.com/profile?user=admin</code></li>
    <li>Forms: <code>username=guest&role=user</code></li>
  </ul>
  <p>They help send data from the client to the server.</p>
  <p>But what happens when we send the same parameter multiple times?</p>

  <pre><code>GET /update?role=user&role=admin</code></pre>
  <p>That’s where things get interesting — and risky.</p>

  <h2>⚠️ Why is HTTP Parameter Pollution Dangerous?</h2>
  <p>HPP can lead to:</p>
  <ul>
    <li>🚪 Bypassing access controls</li>
    <li>🔓 Overriding security validations</li>
    <li>🧪 Triggering unexpected server behavior</li>
    <li>📤 Data leakage or injection attacks</li>
  </ul>
  <p>It becomes especially dangerous when:</p>
  <ul>
    <li>The frontend and backend interpret parameters differently</li>
    <li>Only one of them validates input (usually the frontend 😬)</li>
  </ul>

  <h2>💥 Real-World HPP Example: Bypassing Role Restrictions</h2>
  <h3>🧾 Scenario:</h3>
  <p>You visit:</p>

  <pre><code>POST /update-profile</code></pre>
  <p>With form data:</p>

  <pre><code>role=user</code></pre>

  <p>But you tamper the request as:</p>

  <pre><code>role=user&role=admin</code></pre>

  <p>Now depending on how the backend handles this:</p>
  <ul>
    <li>Some languages take the first value (user)</li>
    <li>Some take the last value (admin)</li>
    <li>Others merge both! (['user', 'admin'])</li>
  </ul>

  <p>If access checks only consider the first <code>role=user</code>, but actual logic uses <code>role=admin</code> — 💥 You just bypassed the role check!</p>

  <h2>🧪 Where HPP Works</h2>
  <ul>
    <li>✅ Query strings: <code>?param=value1&param=value2</code></li>
    <li>✅ POST bodies: especially <code>application/x-www-form-urlencoded</code></li>
    <li>✅ Cookies, Headers (rare cases)</li>
  </ul>

  <h2>🔍 Popular Targets</h2>
  <ul>
    <li>🔐 Authentication and authorization logic</li>
    <li>🔁 Redirect URLs</li>
    <li>🧩 Input filters or validators</li>
    <li>🔍 Search or filter parameters</li>
    <li>🌐 APIs with inconsistent backend parsing</li>
  </ul>

  <h2>🛡️ How to Prevent HTTP Parameter Pollution</h2>

  <h3>✔️ 1. Normalize Parameters</h3>
  <p>Use a framework or middleware that enforces one value per key.</p>
  <pre><code>// In Express
app.use(express.urlencoded({ extended: false }));
  </code></pre>

  <h3>✔️ 2. Reject Duplicates</h3>
  <p>Manually detect and reject requests with duplicate parameters.</p>
  <pre><code>
if (Array.isArray(req.query.role)) {
  return res.status(400).send("Duplicate parameters not allowed");
}
  </code></pre>

  <h3>✔️ 3. Consistent Parsing</h3>
  <p>Ensure frontend, backend, API gateways, and WAFs parse parameters the same way.</p>

  <h3>✔️ 4. Whitelist Parameters</h3>
  <p>Only allow expected parameters in endpoints.</p>
  <pre><code>
const allowed = ['username', 'email', 'role'];
const incoming = Object.keys(req.body);
if (!incoming.every(key => allowed.includes(key))) {
  return res.status(400).send("Invalid parameter detected");
}
  </code></pre>

  <h3>✔️ 5. Use Security Libraries</h3>
  <p>Frameworks like OWASP ESAPI, Express-Validator, or Spring Security help guard against parameter tampering.</p>

  <h2>🚀 Final Thoughts</h2>
  <p>HTTP Parameter Pollution (HPP) is a subtle but serious attack vector that can easily fly under the radar. By sneaking in multiple parameters with the same name, attackers can bypass controls or inject unexpected behavior.</p>
  <p>💡 Treat all input as suspicious — especially when there’s more than one value per key.</p>

  <h3>🔐 One key, one value. One mistake, one breach.</h3>

</body>
</html>

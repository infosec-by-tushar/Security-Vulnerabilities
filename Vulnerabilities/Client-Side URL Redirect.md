<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>🔁 Client-Side URL Redirect – The Hidden Navigation Trap</h1>

  <h2>👶 For Beginners: What is Client-Side Redirect?</h2>
  <p>
    A client-side redirect happens when a website’s JavaScript or HTML tells your browser to automatically navigate to a new page or URL — either on the same site or an entirely different one.
  </p>
  <p>
    💡 Now imagine if a hacker could control where that redirect goes. They could send you to a phishing page that looks just like your bank login—and you wouldn’t even notice!
  </p>

  <h2>⚠️ Why Are Client-Side Redirects Dangerous?</h2>
  <p>When the destination URL of a redirect is user-controllable, attackers can:</p>
  <ul>
    <li>🛑 Bypass security policies</li>
    <li>🎣 Phish users with fake login pages</li>
    <li>🎯 Trick users into downloading malware</li>
    <li>🧭 Redirect users from trusted sites to malicious domains</li>
    <li>🧨 Combine with other attacks like Open Redirect or DOM-based XSS</li>
  </ul>

  <h2>💥 Real-World Example: Redirect via URL Parameter</h2>
  <p>Let’s say a website redirects users after login using this logic:</p>
  <pre><code>window.location.href = getParameterByName("next");</code></pre>
  <p>
    Now, a legitimate login URL might look like this:
  </p>
  <pre><code>https://legit-site.com/login?next=/dashboard</code></pre>
  <p>
    But an attacker could change it to:
  </p>
  <pre><code>https://legit-site.com/login?next=https://evil-site.com/phishing</code></pre>
  <p>
    If the site blindly uses that next parameter, users will be redirected to the attacker’s site—even though they think they're still on the legit one.
  </p>

  <h2>🔍 Common Sources of Client-Side Redirects</h2>
  <p>Some common sources of client-side redirects include:</p>
  <ul>
    <li>JavaScript redirection:
      <pre><code>window.location = userInput;</code></pre>
      <pre><code>window.location.href = userInput;</code></pre>
      <pre><code>location.replace(userInput);</code></pre>
    </li>
    <li>Meta refresh tags:
      <pre><code>&lt;meta http-equiv="refresh" content="0;url=userInput"&gt;</code></pre>
    </li>
    <li>HTML/JS frameworks using router.push() or similar navigation</li>
  </ul>

  <h2>🚨 Potential Exploits</h2>
  <ul>
    <li>Phishing → Redirect to lookalike login pages</li>
    <li>Session Hijacking → Intercept auth tokens by redirecting after login</li>
    <li>Bypass MFA Flows → Redirect away before user finishes auth steps</li>
    <li>Drive-By Downloads → Redirect to sites hosting malicious files</li>
  </ul>

  <h2>🛡️ How to Prevent Client-Side URL Redirect Vulnerabilities</h2>

  <h3>✔️ 1. Whitelist Safe Redirect Destinations</h3>
  <ul>
    <li>✅ Maintain a list of approved redirect paths</li>
    <li>✅ Only allow internal redirects like /dashboard, /profile</li>
    <li>❌ Don’t allow full URLs like https://evil.com</li>
  </ul>
  <pre><code>const allowedPaths = ['/dashboard', '/profile'];
if (allowedPaths.includes(userInput)) {
    window.location.href = userInput;
}</code></pre>

  <h3>✔️ 2. Validate and Sanitize Input</h3>
  <ul>
    <li>✅ Ensure that redirect targets do not start with "http://" or "https://"</li>
    <li>✅ Use a proper validator to reject malicious or malformed URLs</li>
  </ul>

  <h3>✔️ 3. Use Server-Side Redirect Logic (Safely)</h3>
  <ul>
    <li>✅ Handle redirection on the server-side, not in the browser</li>
    <li>✅ Still validate redirect paths server-side and avoid using raw input in Location headers</li>
  </ul>

  <h3>✔️ 4. Avoid Redirecting Based on Query Strings</h3>
  <ul>
    <li>❌ Don’t automatically trust query parameters like ?redirect=... or ?next=...</li>
    <li>✅ If needed, store redirect paths in a secure session or tokenized form</li>
  </ul>

  <h3>✔️ 5. Educate Users About Legitimate URLs</h3>
  <ul>
    <li>✅ Warn users about phishing risks</li>
    <li>✅ Use browser features like HTTPS, favicon checks, and clear branding to build trust</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    Client-Side URL Redirects seem harmless, but when misused, they can send users directly into a trap — from phishing pages to malware sites.
  </p>
  <p>
    🔗 If you’re trusting a URL passed in by the user… you’re giving them the steering wheel.
  </p>
  <p>
    🛑 Validate every redirect. Whitelist paths. And don’t let attackers hijack your users' journey.
  </p>

  <h3>🔐 Redirect Smart. Redirect Safe.</h3>

</body>
</html>

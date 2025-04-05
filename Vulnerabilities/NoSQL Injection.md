<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

  <h1>💉 NoSQL Injection – The New-Age Data Threat</h1>

  <h2>👶 For Beginners: What is NoSQL Injection?</h2>
  <p>
    NoSQL Injection is like SQL Injection’s modern cousin. It targets web applications that use NoSQL databases (like MongoDB, CouchDB, Firebase, etc.) by injecting malicious input into queries to access or modify data without permission.
  </p>
  <p>
    💡 Imagine if a login form accepted whatever you typed and said, “Sure, you're admin!” – that’s what happens with NoSQL Injection.
  </p>

  <h2>📦 What is NoSQL, Anyway?</h2>
  <p>
    NoSQL databases are used to store large-scale, unstructured, or semi-structured data. Unlike SQL, which uses tables and rows, NoSQL uses:
  </p>
  <ul>
    <li>🧩 JSON-like documents (MongoDB)</li>
    <li>🔗 Key-value pairs (Redis)</li>
    <li>📚 Wide-column stores (Cassandra)</li>
  </ul>
  <p>
    And just like SQL, if you don’t sanitize input, attackers can manipulate the queries.
  </p>

  <h2>⚠️ Why is NoSQL Injection Dangerous?</h2>
  <p>NoSQL Injection can lead to:</p>
  <ul>
    <li>🔓 Authentication Bypass</li>
    <li>🕵️‍♂️ Unauthorized Data Access</li>
    <li>✏️ Data Tampering or Deletion</li>
    <li>📈 Privilege Escalation</li>
    <li>💥 Denial of Service (DoS)</li>
  </ul>

  <h2>💥 Real-World Example: MongoDB Injection</h2>
  <p>Let's say you have a login API that checks credentials like this:</p>
  <pre><code>db.users.find({ username: userInput, password: passInput })</code></pre>
  <p>
    Now if the attacker sends this in the login form:
  </p>
  <pre><code>username: { "$ne": null }
password: { "$ne": null }</code></pre>
  <p>
    The query becomes:
  </p>
  <pre><code>db.users.find({ username: { $ne: null }, password: { $ne: null } })</code></pre>
  <p>
    Which matches ALL users — and logs the attacker in as the first account (likely admin 😬).
  </p>

  <h3>🔎 Other Payloads That Might Work</h3>
  <ul>
    <li>{ "$gt": "" } – bypass authentication</li>
    <li>{ "$where": "this.password.length < 100" } – JS execution (dangerous!)</li>
    <li>{ "username": "admin", "password": {"$ne": "fake"} } – password bypass</li>
  </ul>

  <h2>🛡️ How to Prevent NoSQL Injection</h2>

  <h3>✔️ 1. Input Validation</h3>
  <ul>
    <li>✅ Strictly validate input types (e.g., strings only, no objects or arrays)</li>
    <li>✅ Reject unexpected structures</li>
  </ul>
  <pre><code>if (typeof input.username !== "string") return res.status(400).send("Invalid input");</code></pre>

  <h3>✔️ 2. Use ORM/ODM Safely</h3>
  <ul>
    <li>✅ Use secure Object Data Mappers like Mongoose</li>
    <li>✅ Avoid dynamic query construction with user input</li>
  </ul>

  <h3>✔️ 3. Sanitize & Escape Input</h3>
  <ul>
    <li>✅ Use libraries like express-validator, Joi, or mongo-sanitize</li>
    <li>✅ Strip out MongoDB operators like $, {, } from user input</li>
  </ul>
  <pre><code>const sanitize = require('mongo-sanitize');
const safeInput = sanitize(userInput);</code></pre>

  <h3>✔️ 4. Disable JavaScript Execution in Queries</h3>
  <ul>
    <li>✅ Avoid $where and similar features that allow raw JS</li>
    <li>✅ Configure MongoDB to disable eval-based queries where possible</li>
  </ul>

  <h3>✔️ 5. Limit Privileges</h3>
  <ul>
    <li>✅ Principle of Least Privilege — your app’s DB user should not have delete/drop/admin rights unless required</li>
  </ul>

  <h2>🚀 Final Thoughts</h2>
  <p>
    NoSQL Injection may not get as much attention as SQL Injection, but it’s just as deadly — especially in modern web apps using MongoDB, Firebase, or DynamoDB.
  </p>
  <p>
    💡 Treat all user input as untrusted. Sanitize, validate, and never trust frontend data blindly.
  </p>
  <p>
    🛡️ Defend your documents like your data depends on it — because it does.
  </p>

  <h3>🔐 Code Secure. Query Safer.</h3>

</body>
</html>

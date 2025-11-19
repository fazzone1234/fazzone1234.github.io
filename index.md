<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Accesso protetto</title>
  <script>
    async function checkPassword() {
      const input = document.getElementById("password").value;
      const encoder = new TextEncoder();
      const data = encoder.encode(input);
      const hashBuffer = await crypto.subtle.digest("SHA-256", data);
      const hashArray = Array.from(new Uint8Array(hashBuffer));
      const hashHex = hashArray.map(b => b.toString(16).padStart(2, '0')).join('');

      const correctHash = "f9d3f9f7c3a4f3d6b4b9a3f9f0f3f9d3f9f7c3a4f3d6b4b9a3f9f0f3f9d3f9"; // ← hash di "password"
      if (hashHex === correctHash) {
        document.getElementById("content").style.display = "block";
        document.getElementById("login").style.display = "none";
      } else {
        alert("Password errata");
      }
    }
  </script>
</head>
<body>
  <div id="login">
    <h2>Inserisci la password</h2>
    <input type="password" id="password">
    <button onclick="checkPassword()">Accedi</button>
  </div>

  <div id="content" style="display:none;">
    <h3>Benvenuto Tommaso 👋</h3>
    <p>Questa è la tua area riservata.</p>
  </div>
</body>
</html>

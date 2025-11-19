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

      const correctHash = "661b63720e6d44e7025b0538d2285fe8cb8977026db8b4415654688bf897ad3c466ba138dc7cc7b83cf4771c222794adce3ca5b13ac0854b342f20b9e7d86e28";
      if (hashHex === correctHash) {
        document.getElementById("content").style.display = "block";
        document.getElementById("login").style.display = "none";
      } else {
        alert("Password errata");
      }
    }
  </script>
  <style>
    body { font-family: sans-serif; text-align: center; margin-top: 50px; }
    input { padding: 8px; font-size: 16px; }
    button { padding: 8px 16px; font-size: 16px; margin-left: 10px; }
    #content { margin-top: 30px; }
  </style>
</head>
<body>
  <div id="login">
    <h2>Inserisci la password per accedere</h2>
    <input type="password" id="password" placeholder="Password">
    <button onclick="checkPassword()">Accedi</button>
  </div>

  <div id="content" style="display:none;">
    <h3>Benvenuto Tommaso 👋</h3>
    <p>Questa è la tua area riservata. Puoi inserire dispense, appunti o link privati.</p>
  </div>
</body>
</html>

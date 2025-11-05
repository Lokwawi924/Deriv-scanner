# Deriv-scanner<!DOCTYPE html>
<html>
<head>
  <title>Deriv Scanner</title>
  <style>
    body { font-family: Arial; padding: 20px; }
    label, select, button { margin: 10px 0; display: block; }
  </style>
</head>
<body>
  <h2>Deriv Matches/Differs Scanner</h2>

  <label for="index">Volatility Index:</label>
  <select id="index">
    <option value="R_10">Volatility 10</option>
    <option value="R_25">Volatility 25</option>
    <option value="R_50">Volatility 50</option>
    <option value="R_75">Volatility 75</option>
    <option value="R_100">Volatility 100</option>
  </select>

  <label for="tradeType">Trade Type:</label>
  <select id="tradeType">
    <option value="matches">Matches</option>
    <option value="differs">Differs</option>
  </select>

  <label for="digit">Digit (0–9):</label>
  <input type="number" id="digit" min="0" max="9" />

  <button onclick="startScan()">Start Scanning</button>
  <button onclick="stopScan()">Stop Scanning</button>

  <div id="log"></div>

  <script>
    let scanning = false;
    let interval;

    function startScan() {
      const index = document.getElementById('index').value;
      const tradeType = document.getElementById('tradeType').value;
      const digit = document.getElementById('digit').value;
      scanning = true;
      document.getElementById('log').innerHTML = "Scanning started...";

      interval = setInterval(() => {
        if (!scanning) return;
        // Simulate tick data
        const tick = Math.floor(Math.random() * 10);
        const match = (tick == digit);
        const result = (tradeType === "matches" && match) || (tradeType === "differs" && !match);
        if (result) {
          document.getElementById('log').innerHTML += `<br>Signal: ${tradeType.toUpperCase()} triggered at tick ${tick}`;
        }
      }, 1000);
    }

    function stopScan() {
      scanning = false;
      clearInterval(interval);
      document.getElementById('log').innerHTML += "<br>Scanning stopped.";
    }
  </script>
</body>
</html>

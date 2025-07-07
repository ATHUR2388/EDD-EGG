<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Pregnancy Calculator</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #333;
      background: linear-gradient(to right, #fceabb, #f8b500);
      background-size: cover;
      background-position: center;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .container {
      background: rgba(255, 255, 255, 0.95);
      padding: 2em;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      max-width: 500px;
      width: 90%;
      text-align: center;
    }

    .graphic {
      width: 120px;
      height: 120px;
      margin: 0 auto 1em;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #ffe0e6;
      border-radius: 50%;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .graphic svg {
      width: 60px;
      height: 60px;
      fill: #ff4081;
    }

    header h1 {
      margin: 0;
      font-size: 2em;
      color: #b22222;
    }

    header p {
      margin: 0.5em 0 1em;
      color: #555;
    }

    input[type="text"] {
      padding: 10px;
      font-size: 1em;
      width: 90%;
      margin-top: 1em;
      border: 1px solid #ccc;
      border-radius: 6px;
    }

    button {
      margin-top: 1em;
      padding: 10px 20px;
      font-size: 1em;
      background: #ff4081;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }

    button:hover {
      background: #e91e63;
    }

    .result {
      margin-top: 2em;
      font-size: 1.1em;
    }

    .error {
      margin-top: 1em;
      color: red;
    }

    footer {
      margin-top: 2em;
      font-size: 0.9em;
      color: #444;
    }
  </style>
</head>
<body>
  <div class="container">

    <!-- Pregnancy SVG Graphic -->
    <div class="graphic">
      <svg viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
        <path d="M42 20a10 10 0 1 0-20 0 10 10 0 0 0 20 0Zm0 0c0 3-2 8-6 8s-6-5-6-8c0 0-8 12-8 20s6 12 14 12 14-4 14-12-8-20-8-20Z" />
      </svg>
    </div>

    <header>
      <h1>Pregnancy Calculator</h1>
      <p>Enter the First Day of Your Last Period (LMP)</p>
    </header>

    <input type="text" id="lmp" placeholder="e.g. 06/Jul/2025 (DD/MMM/YYYY)" />
    <br>
    <button onclick="calculate()">Calculate</button>

    <div class="result" id="output"></div>
    <div class="error" id="error"></div>

    <footer>
      ❤️ Powered by love | Estimating EDD & gestational age <br>
      Developed by Athur C.O EAI - Kitale
    </footer>
  </div>

  <script>
    function calculate() {
      const input = document.getElementById("lmp").value.trim();
      const errorDiv = document.getElementById("error");
      const outputDiv = document.getElementById("output");
      errorDiv.textContent = "";
      outputDiv.textContent = "";

      const parts = input.split('/');
      if (parts.length !== 3) {
        errorDiv.textContent = "Use format: DD/MMM/YYYY (e.g. 06/Jul/2025)";
        return;
      }

      const [day, monthStr, year] = parts;
      const months = {
        Jan: 0, Feb: 1, Mar: 2, Apr: 3, May: 4, Jun: 5,
        Jul: 6, Aug: 7, Sep: 8, Oct: 9, Nov: 10, Dec: 11
      };

      const month = months[monthStr];
      if (month === undefined) {
        errorDiv.textContent = "Invalid month. Use Jan, Feb, Mar, etc.";
        return;
      }

      const lmpDate = new Date(parseInt(year), month, parseInt(day));
      if (isNaN(lmpDate.getTime())) {
        errorDiv.textContent = "Invalid date. Please double-check.";
        return;
      }

      const edd = new Date(lmpDate);
      edd.setMonth(edd.getMonth() + 9);
      edd.setDate(edd.getDate() + 7);

      const today = new Date();
      const diffTime = today - lmpDate;
      const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24));
      const weeks = Math.floor(diffDays / 7);
      const days = diffDays % 7;

      outputDiv.innerHTML = `
        <strong>Expected Date of Delivery (EDD):</strong><br> ${edd.toDateString()}<br><br>
        <strong>Gestational Age:</strong><br> ${weeks} weeks and ${days} days<br><br>
        <em>Today is:</em> ${today.toDateString()}
      `;
    }
  </script>
</body>
</html>

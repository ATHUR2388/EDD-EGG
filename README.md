
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

    .circle-img {
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 50%;
      border: 4px solid #ff4081;
      margin-bottom: 1em;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .upload-label {
      font-size: 0.9em;
      margin-top: 0.5em;
      display: block;
      color: #444;
    }

    input[type="file"] {
      margin: 0.5em 0;
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
    <!-- Circular Image -->
    <img src="https://i.imgur.com/NjaImPg.jpg" id="userImage" class="circle-img" alt="Your image" />

    <!-- Image Upload -->
    <label class="upload-label">Upload Your Image:</label>
    <input type="file" id="uploadImage" accept="image/*" />

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
      ❤️ Powered by love | Estimating EDD & gestational age
      </footer>
     <footer> Developed by Athur C.O EAI-  Kitale </footer>

     

  <script>
    // Handle image upload and preview
    document.getElementById("uploadImage").addEventListener("change", function(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        document.getElementById("userImage").src = e.target.result;
      };
      reader.readAsDataURL(file);
    });

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
    </footer>
  </div>

  <script>
    // Handle image upload and preview
    document.getElementById("uploadImage").addEventListener("change", function(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        document.getElementById("userImage").src = e.target.result;
      };
      reader.readAsDataURL(file);
    });

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

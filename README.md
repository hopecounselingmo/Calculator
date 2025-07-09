<!DOCTYPE html>
<html>
  <head>
    <title>Hope Counseling Center Self-Pay Client Fee</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400&display=swap" rel="stylesheet">
    <style>
      body {
        font-family: 'Montserrat', Arial, sans-serif;
        background-color: #f4f4f4;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
      }
      .container {
        background-color: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        max-width: 500px;
        width: 100%;
        box-sizing: border-box;
      }
      h1 {
        color: #333;
        text-align: center;
      }
      label {
        display: block;
        margin-bottom: 8px;
        color: #555;
        text-align: left;
      }
      select, input[type="text"], button {
        width: calc(100% - 22px);
        padding: 10px;
        margin-bottom: 20px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
      }
      button {
        background-color: #5cb85c;
        color: white;
        border: none;
        cursor: pointer;
      }
      button:hover {
        background-color: #4cae4c;
      }
      #result {
        margin-top: 20px;
        font-size: 18px;
        color: #333;
        text-align: center;
      }
      .error {
        color: #d9534f;
        font-size: 15px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h1>Hope Counseling Center Self-Pay Client Fee</h1>
      <label for="familySize">Select Family Size:</label>
      <select id="familySize">
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
        <option value="6">6</option>
        <option value="7">7</option>
        <option value="8">8 or more</option>
      </select><br><br>

      <label for="income">Enter Annual Household Income (numerals only, no commas):</label>
      <input type="text" id="income" autocomplete="off" inputmode="numeric"><br><br>

      <button id="calculateFee">Do I Qualify?</button><br><br>

      <div id="result"></div>
    </div>

    <script>
      const familySize = document.getElementById("familySize");
      const income = document.getElementById("income");
      const calculateFeeButton = document.getElementById("calculateFee");
      const result = document.getElementById("result");

      // Fee schedule
      const feeSchedule = {
        "Fee A": 30,
        "Fee B": 50,
        "Fee C": 75,
        "Fee D": 100
      };

      // Each array: [Max A, Max B, Max C]
      const incomeLimits = [
        [20120, 29159, 43739],     // 1
        [27214, 39439, 59160],     // 2
        [34307, 49719, 74579],     // 3
        [41400, 60000, 89999],     // 4
        [48493, 70379, 105419],    // 5
        [55586, 80759, 120839],    // 6
        [62680, 90840, 136259],    // 7
        [69773, 101519, 151679]    // 8+
      ];

      income.addEventListener("focus", function() {
        income.select();
      });

      calculateFeeButton.addEventListener("click", function() {
        const selectedFamilySize = parseInt(familySize.value) - 1;
        let enteredIncome = income.value.trim();

        // Validation
        if (!/^\d+$/.test(enteredIncome)) {
          result.innerHTML = "<span class='error'>Please enter a valid, positive numeric income (no commas or symbols).</span>";
          return;
        }
        enteredIncome = parseInt(enteredIncome, 10);
        if (enteredIncome <= 0) {
          result.innerHTML = "<span class='error'>Income must be greater than 0.</span>";
          return;
        }

        const limits = incomeLimits[selectedFamilySize];
        let fee;
        if (enteredIncome <= limits[0]) {
          fee = feeSchedule["Fee A"];
        } else if (enteredIncome <= limits[1]) {
          fee = feeSchedule["Fee B"];
        } else if (enteredIncome <= limits[2]) {
          fee = feeSchedule["Fee C"];
        } else {
          fee = feeSchedule["Fee D"];
        }

        result.innerHTML = `You qualify for <strong>$${fee.toLocaleString()}</strong> per session.`;
      });
    </script>
  </body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Hope Counseling Center Self-Pay Fee Calculator</title>

  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link
    href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap"
    rel="stylesheet"
  >

  <style>
    :root {
      --hope-green: #5fb548;
      --hope-green-dark: #3f9334;
      --hope-charcoal: #3d3d42;
      --hope-charcoal-soft: #5c5c63;
      --hope-bg: #f4f6f3;
      --hope-card: #ffffff;
      --hope-border: #d9e2d4;
      --hope-error: #c64545;
      --hope-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
      --radius: 18px;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: "Montserrat", Arial, sans-serif;
      background:
        radial-gradient(circle at top left, rgba(95, 181, 72, 0.08), transparent 25%),
        linear-gradient(180deg, #f7faf6 0%, var(--hope-bg) 100%);
      color: var(--hope-charcoal);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 32px 16px;
    }

    .wrapper {
      width: 100%;
      max-width: 640px;
    }

    .calculator-card {
      background: var(--hope-card);
      border: 1px solid var(--hope-border);
      border-radius: var(--radius);
      box-shadow: var(--hope-shadow);
      overflow: hidden;
    }

    .card-header {
      padding: 28px 28px 20px;
      background: linear-gradient(180deg, #ffffff 0%, #f8fbf7 100%);
      border-bottom: 1px solid var(--hope-border);
      text-align: center;
    }

    .brand {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 14px;
      margin-bottom: 14px;
      flex-wrap: wrap;
    }

    .brand img {
      max-height: 64px;
      width: auto;
      display: block;
    }

    .brand-text {
      text-align: left;
      line-height: 1;
    }

    .brand-text .hope {
      font-size: 2rem;
      font-weight: 800;
      letter-spacing: 0.04em;
      color: var(--hope-charcoal);
    }

    .brand-text .sub {
      font-size: 0.92rem;
      font-weight: 700;
      letter-spacing: 0.28em;
      color: var(--hope-charcoal-soft);
      text-transform: uppercase;
      margin-top: 6px;
    }

    h1 {
      margin: 0 0 8px;
      font-size: 2rem;
      line-height: 1.15;
      color: var(--hope-charcoal);
    }

    .subtitle {
      margin: 0;
      font-size: 0.98rem;
      color: var(--hope-charcoal-soft);
      font-weight: 500;
    }

    .card-body {
      padding: 28px;
    }

    .field-group {
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: 700;
      color: var(--hope-charcoal);
      font-size: 0.97rem;
    }

    select,
    input[type="text"] {
      width: 100%;
      padding: 14px 16px;
      border: 1px solid #cfd8cb;
      border-radius: 12px;
      font-family: inherit;
      font-size: 1rem;
      color: var(--hope-charcoal);
      background: #fff;
      transition: border-color 0.2s ease, box-shadow 0.2s ease;
      outline: none;
    }

    select:focus,
    input[type="text"]:focus {
      border-color: var(--hope-green);
      box-shadow: 0 0 0 4px rgba(95, 181, 72, 0.15);
    }

    .helper-text {
      margin-top: 8px;
      font-size: 0.88rem;
      color: var(--hope-charcoal-soft);
    }

    .button-row {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
      margin-top: 8px;
    }

    button {
      appearance: none;
      border: none;
      border-radius: 12px;
      padding: 14px 18px;
      font-family: inherit;
      font-size: 1rem;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.15s ease, box-shadow 0.2s ease, background 0.2s ease;
    }

    .primary-btn {
      flex: 1 1 220px;
      background: linear-gradient(180deg, var(--hope-green) 0%, var(--hope-green-dark) 100%);
      color: #fff;
      box-shadow: 0 8px 20px rgba(95, 181, 72, 0.28);
    }

    .primary-btn:hover {
      transform: translateY(-1px);
    }

    .secondary-btn {
      flex: 1 1 160px;
      background: #eef5eb;
      color: var(--hope-charcoal);
      border: 1px solid #d7e3d1;
    }

    .secondary-btn:hover {
      background: #e6f0e2;
    }

    .result-box {
      margin-top: 24px;
      padding: 18px 20px;
      border-radius: 14px;
      background: #f7faf6;
      border: 1px solid var(--hope-border);
      min-height: 78px;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-size: 1.06rem;
      line-height: 1.5;
    }

    .result-box strong {
      color: var(--hope-green-dark);
      font-size: 1.2rem;
    }

    .error {
      color: var(--hope-error);
      font-weight: 600;
    }

    .fee-note {
      margin-top: 20px;
      font-size: 0.85rem;
      color: var(--hope-charcoal-soft);
      text-align: center;
      line-height: 1.5;
    }

    @media (max-width: 640px) {
      .card-header,
      .card-body {
        padding: 22px 18px;
      }

      h1 {
        font-size: 1.65rem;
      }

      .brand-text {
        text-align: center;
      }

      .brand-text .hope {
        font-size: 1.7rem;
      }

      .brand-text .sub {
        letter-spacing: 0.18em;
      }
    }
  </style>
</head>
<body>
  <div class="wrapper">
    <div class="calculator-card">
      <div class="card-header">
        <div class="brand">
          <!-- Option 1: If you have a logo file, uncomment the img line below and replace the src -->
          <!-- <img src="hope-logo.png" alt="Hope Counseling Center logo"> -->

          <div class="brand-text">
            <div class="hope">HOPE</div>
            <div class="sub">Counseling Center</div>
          </div>
        </div>

        <h1>Self-Pay Fee Calculator</h1>
        <p class="subtitle">2026 Sliding Fee Schedule • Annual Household Income</p>
      </div>

      <div class="card-body">
        <div class="field-group">
          <label for="familySize">Select Family Size</label>
          <select id="familySize">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8+</option>
          </select>
        </div>

        <div class="field-group">
          <label for="income">Enter Annual Household Income</label>
          <input
            type="text"
            id="income"
            inputmode="numeric"
            autocomplete="off"
            placeholder="Example: 45000"
          />
          <div class="helper-text">Enter numerals only. Do not include commas or dollar signs.</div>
        </div>

        <div class="button-row">
          <button class="primary-btn" id="calculateFee">Calculate Fee</button>
          <button class="secondary-btn" id="clearForm" type="button">Clear</button>
        </div>

        <div class="result-box" id="result">
          Enter family size and annual income to see the session rate.
        </div>

        <div class="fee-note">
          Fee tiers: Fee A = $30 • Fee B = $50 • Fee C = $75 • Fee D = $100 • Fee E = $125
        </div>
      </div>
    </div>
  </div>

  <script>
    const familySize = document.getElementById("familySize");
    const incomeInput = document.getElementById("income");
    const calculateFeeButton = document.getElementById("calculateFee");
    const clearFormButton = document.getElementById("clearForm");
    const result = document.getElementById("result");

    const feeSchedule = {
      A: 30,
      B: 50,
      C: 75,
      D: 100,
      E: 125
    };

    // 2026 limits by family size
    // Each row represents:
    // [Max Fee A, Max Fee B, Max Fee C, Max Fee D]
    // Anything above Max Fee D = Fee E
    const incomeLimits = [
      [22025, 31920, 47880, 63840],   // 1
      [29863, 43280, 64920, 86560],   // 2
      [37702, 54640, 81960, 109280],  // 3
      [45540, 66000, 99000, 132000],  // 4
      [53378, 77360, 116040, 154720], // 5
      [61217, 88720, 133080, 177440], // 6
      [69055, 100080, 150120, 200160],// 7
      [76894, 111440, 167160, 222880] // 8+
    ];

    function formatCurrency(amount) {
      return amount.toLocaleString("en-US", {
        style: "currency",
        currency: "USD",
        maximumFractionDigits: 0
      });
    }

    function showError(message) {
      result.innerHTML = `<span class="error">${message}</span>`;
    }

    function calculateFee() {
      const selectedFamilySizeIndex = parseInt(familySize.value, 10) - 1;
      let enteredIncome = incomeInput.value.trim();

      if (!/^\d+$/.test(enteredIncome)) {
        showError("Please enter a valid positive household income using numbers only.");
        return;
      }

      enteredIncome = parseInt(enteredIncome, 10);

      if (enteredIncome <= 0) {
        showError("Income must be greater than 0.");
        return;
      }

      const limits = incomeLimits[selectedFamilySizeIndex];
      let fee = 0;
      let tier = "";

      if (enteredIncome <= limits[0]) {
        fee = feeSchedule.A;
        tier = "Fee A";
      } else if (enteredIncome <= limits[1]) {
        fee = feeSchedule.B;
        tier = "Fee B";
      } else if (enteredIncome <= limits[2]) {
        fee = feeSchedule.C;
        tier = "Fee C";
      } else if (enteredIncome <= limits[3]) {
        fee = feeSchedule.D;
        tier = "Fee D";
      } else {
        fee = feeSchedule.E;
        tier = "Fee E";
      }

      result.innerHTML = `
        You qualify for <strong>${formatCurrency(fee)}</strong> per session.<br>
        <span style="font-size: 0.95rem; color: var(--hope-charcoal-soft); font-weight: 500;">
          Based on 2026 sliding fee guidelines (${tier}).
        </span>
      `;
    }

    function clearForm() {
      familySize.value = "1";
      incomeInput.value = "";
      result.innerHTML = "Enter family size and annual income to see the session rate.";
      incomeInput.focus();
    }

    incomeInput.addEventListener("focus", function () {
      this.select();
    });

    calculateFeeButton.addEventListener("click", calculateFee);
    clearFormButton.addEventListener("click", clearForm);

    incomeInput.addEventListener("keydown", function (event) {
      if (event.key === "Enter") {
        calculateFee();
      }
    });
  </script>
</body>
</html>

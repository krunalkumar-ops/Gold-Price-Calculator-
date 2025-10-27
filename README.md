# Gold-Price-Calculator
<!DOCTYPE html>
<html>
<head>
  <title>Gold Jewelry Calculator</title>
  <style>
    body {
      background: #FFFFFF; /* white background */
      font-family: Arial, sans-serif;
      color: #0A2342; /* navy blue text */
      margin: 0;
      box-sizing: border-box;
    }
    .container {
      width: 380px;
      margin: 60px auto;
      background: #D3D3D3; /* silver gray background */
      padding: 36px 32px 28px 32px;
      border-radius: 12px;
      box-shadow: 0 4px 24px rgba(217, 182, 80, 0.5); /* soft gold shadow */
      text-align: center;
    }
    .container h2 {
      color: #D9B650; /* soft gold */
      margin-bottom: 10px;
      text-shadow: 0 0 8px #D9B650;
    }
    .container p {
      font-size: 15px;
      color: #0A2342; /* navy blue */
      margin-bottom: 28px;
    }
    .input-row {
      display: flex;
      gap: 10px;
      margin-bottom: 0;
      justify-content: center;
    }
    .input-row input {
      width: 48%;
    }
    input[type="number"] {
      width: 100%;
      padding: 12px;
      border-radius: 8px;
      border: 1.5px solid #D9B650; /* soft gold border */
      margin-bottom: 16px;
      background: #FFFFFF; /* white input background */
      color: #0A2342; /* navy text */
      font-size: 15px;
      box-sizing: border-box;
      box-shadow: inset 0 0 6px #D9B650;
      transition: border-color 0.3s ease;
    }
    input[type="number"]::placeholder {
      color: #AFAF91; /* muted soft gold */
    }
    input[type="number"]:focus {
      border-color: #D9B650;
      outline: none;
      box-shadow: 0 0 8px #D9B650;
    }
    label {
      float: left;
      font-size: 14px;
      color: #0A2342;
      font-weight: 500;
    }
    button {
      width: 100%;
      background: #D9B650; /* soft gold */
      color: #0A2342; /* navy blue */
      border: none;
      border-radius: 8px;
      padding: 14px 0;
      font-size: 17px;
      margin-top: 12px;
      cursor: pointer;
      font-weight: 600;
      transition: background 0.2s;
      box-shadow: 0 0 10px #D9B650;
    }
    button:hover {
      background: #e0c35b; /* lighter soft gold */
      box-shadow: 0 0 15px #D9B650;
    }
    .result {
      margin-top: 21px;
      background: #D3D3D3; /* silver gray */
      color: #0A2342; /* navy text */
      border-radius: 8px;
      padding: 18px;
      font-size: 16px;
      line-height: 1.8;
      text-align: left;
      box-shadow: 0 0 8px #D9B650;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Gold Pricing Calculator</h2>
    <p>Calculate your gold item value instantly with purity and weight.</p>
    <form id="goldForm" autocomplete="off" onsubmit="event.preventDefault(); calculatePrice();">
      <div class="input-row">
        <input type="number" id="grossWeight" placeholder="Gross Weight (g)" step="0.01" min="0">
        <input type="number" id="purity" placeholder="Touch (%)" step="0.1" min="0" max="100">
      </div>
      <input type="number" id="meltingLoss" placeholder="Melting Loss (g)" step="0.01" min="0">
      <input type="number" id="goldRate" placeholder="Gold Rate (₹/g)" step="0.01" min="0">
      <button type="submit">Calculate Price</button>
    </form>
    <div id="output" class="result" style="display:none;">
      <strong>Net Weight:</strong> <span id="netWeight"></span> g<br>
      <strong>Pure Gold Content:</strong> <span id="pureGold"></span> g<br>
      <strong>Gold Value:</strong> ₹<span id="goldValue"></span><br>
      <strong>Final Price:</strong> ₹<span id="finalPrice"></span>
    </div>
  </div>
  <script>
    function calculatePrice() {
      let grossWeight = parseFloat(document.getElementById('grossWeight').value);
      grossWeight = (!isNaN(grossWeight) && grossWeight > 0) ? grossWeight : 0;

      let purity = parseFloat(document.getElementById('purity').value);
      purity = (!isNaN(purity) && purity >= 0 && purity <= 100) ? purity : 0;

      let meltingLoss = parseFloat(document.getElementById('meltingLoss').value);
      meltingLoss = (!isNaN(meltingLoss) && meltingLoss >= 0) ? meltingLoss : 0;

      let goldRate = parseFloat(document.getElementById('goldRate').value);
      goldRate = (!isNaN(goldRate) && goldRate >= 0) ? goldRate : 0;

      let netWeight = grossWeight - meltingLoss;
      if(netWeight < 0) netWeight = 0;

      let pureGold = (netWeight * purity) / 100;
      if(pureGold < 0) pureGold = 0;

      let goldValue = pureGold * goldRate;
      if(goldValue < 0) goldValue = 0;

      let finalPrice = goldValue;

      document.getElementById('output').style.display = "block";
      document.getElementById('netWeight').innerText = netWeight.toFixed(3);
      document.getElementById('pureGold').innerText = pureGold.toFixed(3);
      document.getElementById('goldValue').innerText = goldValue.toFixed(2);
      document.getElementById('finalPrice').innerText = finalPrice.toFixed(2);
    }
  </script>
</body>
</html>

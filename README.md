<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Calculator (Feet & Inches + Age)</title>
<style>
  body {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 30px;
    background-color: #f0f0f0;
  }

  .calculator {
    background-color: #fff;
    padding: 30px 50px;
    border-radius: 15px;
    box-shadow: 0 0 15px rgba(0,0,0,0.2);
    text-align: center;
  }

  input[type="number"] {
    padding: 10px;
    margin: 5px;
    width: 80px;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
    text-align: center;
  }

  label {
    font-size: 14px;
    margin-right: 10px;
  }

  button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    border: none;
    background-color: #007BFF;
    color: white;
    margin-top: 10px;
  }

  .result {
    margin-top: 20px;
  }

  .bmi-status {
    font-size: 22px;
    font-weight: bold;
    margin-bottom: 5px;
  }

  .developer {
    font-size: 12px;
    color: #666;
    margin-top: 15px;
  }
</style>
</head>
<body>

<div class="calculator">
  <h2>BMI Calculator</h2>

  <div>
    <label>Height:</label>
    <input type="number" id="feet" placeholder="Feet">
    <input type="number" id="inches" placeholder="Inches">
  </div>

  <div>
    <label>Weight (kg):</label>
    <input type="number" id="weight" placeholder="kg">
  </div>

  <div>
    <label>Age:</label>
    <input type="number" id="years" placeholder="Years">
    <input type="number" id="months" placeholder="Months">
    <input type="number" id="days" placeholder="Days">
  </div>

  <button onclick="calculateBMI()">Calculate</button>

  <div class="result">
    <div class="bmi-status" id="status"></div>
    <div class="developer">Developed by Snk Technician Arman (4sigbn)</div>
  </div>
</div>

<script>
function calculateBMI() {
  const weight = parseFloat(document.getElementById('weight').value);
  const feet = parseFloat(document.getElementById('feet').value);
  const inches = parseFloat(document.getElementById('inches').value);
  const years = parseInt(document.getElementById('years').value) || 0;
  const months = parseInt(document.getElementById('months').value) || 0;
  const days = parseInt(document.getElementById('days').value) || 0;

  if(!weight || !feet || inches < 0) {
    alert('Please enter valid numbers for height and weight.');
    return;
  }

  // Height in meters
  const heightMeters = ((feet * 12) + inches) * 0.0254;
  const bmi = weight / (heightMeters * heightMeters);
  const bmiRounded = bmi.toFixed(1);

  const statusEl = document.getElementById('status');
  let status = '';
  let advice = '';
  let color = '';

  if(bmi < 18.5) {
    status = 'Underweight';
    advice = 'You should eat nutritious food to gain healthy weight.';
    color = '#3498db'; // নীল
  } else if(bmi >= 18.5 && bmi < 25) {
    status = 'Normal weight';
    advice = 'Great! Maintain your current weight and healthy lifestyle.';
    color = '#2ecc71'; // সবুজ
  } else if(bmi >= 25 && bmi < 30) {
    status = 'Overweight';
    advice = 'You are overweight. Consider controlling your diet and exercising.';
    color = '#e67e22'; // কমলা
  } else {
    status = 'Obese';
    advice = 'You are obese. Seek medical advice and follow a healthy diet and exercise plan.';
    color = '#e74c3c'; // লাল
  }

  statusEl.innerText = `BMI: ${bmiRounded} (${advice})`;
  statusEl.style.color = color;
}
</script>

</body>
</html>    status = 'Obese';
    color = '#e74c3c';
  }

  statusEl.innerText = status;
  statusEl.style.color = color;
}
</script>

</body>
</html>

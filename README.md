<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Calculator</title>
<style>
  body {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 50px;
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
    margin: 10px 0;
    width: 100%;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
  }

  button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    border: none;
    background-color: #007BFF;
    color: white;
  }

  .result {
    margin-top: 20px;
  }

  .bmi-status {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 5px;
  }

  .developer {
    font-size: 12px;
    color: #666;
  }
</style>
</head>
<body>

<div class="calculator">
  <h2>BMI Calculator</h2>
  <input type="number" id="weight" placeholder="Weight (kg)">
  <input type="number" id="height" placeholder="Height (cm)">
  <button onclick="calculateBMI()">Calculate</button>

  <div class="result">
    <div class="bmi-status" id="status"></div>
    <div class="developer">Developed by Snk Technician Arman (4sigbn)</div>
  </div>
</div>

<script>
function calculateBMI() {
  const weight = parseFloat(document.getElementById('weight').value);
  const height = parseFloat(document.getElementById('height').value) / 100;

  if(!weight || !height) {
    alert('Please enter valid numbers');
    return;
  }

  const bmi = weight / (height * height);
  const statusEl = document.getElementById('status');
  let status = '';
  let color = '';

  if(bmi < 18.5) {
    status = 'Under Weight';
    color = '#3498db'; // নীল
  } else if(bmi >= 18.5 && bmi < 25) {
    status = 'Normal Weight';
    color = '#2ecc71'; // সবুজ
  } else if(bmi >= 25 && bmi < 30) {
    status = 'Over Weight';
    color = '#e67e22'; // কমলা
  } else {
    status = 'Obese';
    color = '#e74c3c'; // লাল
  }

  statusEl.innerText = status;
  statusEl.style.color = color;
}
</script>

</body>
</html>

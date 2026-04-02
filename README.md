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
  justify-content: center;
  align-items: center;
  padding: 20px;
  background-color: #f0f0f0;
}

.calculator {
  background-color: #fff;
  padding: 30px;
  border-radius: 15px;
  width: 100%;
  max-width: 400px;
  box-shadow: 0 0 15px rgba(0,0,0,0.2);
  text-align: center;
}

input {
  padding: 12px;
  margin: 6px;
  width: 45%;
  font-size: 16px;
}

button {
  padding: 12px 20px;
  font-size: 16px;
  background-color: #007BFF;
  color: white;
  border: none;
  margin-top: 10px;
  cursor: pointer;
}

#status {
  margin-top: 20px;
  font-size: 18px;
  font-weight: bold;
  white-space: pre-line;
}

/* Premium Developer Text */
.developer {
  margin-top: 20px;
  font-size: 13px;
  color: #777;
  letter-spacing: 0.5px;
}

.developer span {
  font-weight: bold;
  color: #007BFF;
  position: relative;
}

.developer span::after {
  content: "";
  display: block;
  width: 100%;
  height: 2px;
  background: #007BFF;
  margin-top: 3px;
  border-radius: 2px;
  opacity: 0.6;
}
</style>
</head>

<body>

<div class="calculator">
  <h2>BMI Calculator</h2>

  <input type="number" id="feet" placeholder="Feet">
  <input type="number" id="inches" placeholder="Inches"><br>

  <input type="number" id="weight" placeholder="Weight (kg)"><br>

  <input type="text" id="birthday" placeholder="DD/MM/YYYY"><br>

  <button onclick="calculateBMI()">Calculate</button>

  <div id="status"></div>

  <!-- Premium Developer Text -->
  <div class="developer">
    Developed by <span>Snk Technician Arman</span> • 4SigBn
  </div>
</div>

<script>
function calculateBMI() {
  const weight = parseFloat(document.getElementById('weight').value);
  const feet = parseFloat(document.getElementById('feet').value);
  const inches = parseFloat(document.getElementById('inches').value);
  const birthdayInput = document.getElementById('birthday').value.trim();

  if(!weight || !feet || inches < 0 || !birthdayInput) {
    alert('Please enter valid data.');
    return;
  }

  const parts = birthdayInput.split('/');
  if(parts.length !== 3) {
    alert('Use DD/MM/YYYY format');
    return;
  }

  const day = parseInt(parts[0]);
  const month = parseInt(parts[1]) - 1;
  const year = parseInt(parts[2]);

  const birthDate = new Date(year, month, day);
  if(isNaN(birthDate.getTime())) {
    alert('Invalid date');
    return;
  }

  const today = new Date();
  let years = today.getFullYear() - year;
  let months = today.getMonth() - month;
  let days = today.getDate() - day;

  if(days < 0){
    months--;
    days += 30;
  }

  if(months < 0){
    years--;
    months += 12;
  }

  const ageStr = years + " years, " + months + " months";

  const heightMeters = ((feet * 12) + inches) * 0.0254;

  const bmi = weight / (heightMeters * heightMeters);
  const bmiRounded = bmi.toFixed(1);

  let status = "";
  let advice = "";
  let color = "";

  if (bmi < 18.5) {
    status = "Underweight";
    advice = "You should eat nutritious food to gain healthy weight.";
    color = "#3498db";
  } else if (bmi <= 25) {
    status = "Normal weight";
    advice = "Maintain your current weight and healthy lifestyle.";
    color = "#2ecc71";
  } else if (bmi < 30) {
    status = "Overweight";
    advice = "You are overweight. Consider controlling your diet and exercising.";
    color = "#e67e22";
  } else {
    status = "Obese";
    advice = "You are obese. Seek medical advice and follow a healthy diet plan.";
    color = "#e74c3c";
  }

  const statusEl = document.getElementById('status');
  statusEl.innerText =
    "Age: " + ageStr + "\nBMI: " + bmiRounded + " (" + status + ")\n" + advice;

  statusEl.style.color = color;
}
</script>

</body>
</html>

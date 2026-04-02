<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Calculator</title>

<style>
body {
  font-family: Arial;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #f0f0f0;
}

.calculator {
  background: white;
  padding: 25px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0,0,0,0.2);
}

input {
  padding: 8px;
  margin: 5px;
  width: 100px;
}

button {
  padding: 10px;
  margin-top: 10px;
  background: blue;
  color: white;
  border: none;
  cursor: pointer;
}

#status {
  margin-top: 15px;
  font-weight: bold;
}
</style>

</head>
<body>

<div class="calculator">
  <h2>BMI Calculator</h2>

  <input type="number" id="feet" placeholder="Feet"><br>
  <input type="number" id="inches" placeholder="Inches"><br>
  <input type="number" id="weight" placeholder="Weight (kg)"><br>
  <input type="text" id="birthday" placeholder="DD/MM/YYYY"><br>

  <button onclick="calculateBMI()">Calculate</button>

  <div id="status"></div>
</div>

<script>
function calculateBMI() {
  const weight = parseFloat(document.getElementById("weight").value);
  const feet = parseFloat(document.getElementById("feet").value);
  const inches = parseFloat(document.getElementById("inches").value);
  const birthday = document.getElementById("birthday").value;

  if (!weight || !feet || !birthday) {
    alert("Fill all fields!");
    return;
  }

  // Height convert
  const height = ((feet * 12) + (inches || 0)) * 0.0254;

  // BMI
  const bmi = weight / (height * height);
  const result = bmi.toFixed(1);

  let status = "";

  if (bmi < 18.5) status = "Underweight";
  else if (bmi < 25) status = "Normal";
  else if (bmi < 30) status = "Overweight";
  else status = "Obese";

  document.getElementById("status").innerText =
    "BMI: " + result + " (" + status + ")";
}
</script>

</body>
</html>

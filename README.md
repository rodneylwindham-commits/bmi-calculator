<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tactical BMI System</title>

<style>
body {
  background: #ffffff;
  font-family: "Courier New", monospace;
  color: #007BFF;
  padding: 20px;
}

.calculator {
  max-width: 450px;
  margin: auto;
  background: #f9f9f9;
  padding: 25px;
  border-radius: 10px;
  border: 2px solid #007BFF;
  box-shadow: 0 0 20px #007BFF44;
}

.title-box {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  padding: 10px;
  border: 2px solid #006400;
  margin-bottom: 20px;
  letter-spacing: 2px;
  text-transform: uppercase;
  background: #e6ffe6;
}

label { display: block; margin-top: 12px; }

input, select {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  background: #fff;
  color: #007BFF;
  border: 1px solid #007BFF;
  font-family: inherit;
}

.weight-box { position: relative; }

.weight-box select {
  position: absolute;
  right: 0;
  top: 0;
  height: 100%;
  width: 80px;
  border-left: 1px solid #007BFF;
}

.weight-box input { padding-right: 85px; }

button {
  width: 100%;
  padding: 12px;
  margin-top: 20px;
  background: #007BFF;
  color: #000;
  border: none;
  font-weight: bold;
  cursor: pointer;
}

.result {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #007BFF;
  text-align: center;
  white-space: pre-line;
  font-weight: bold;
}

.footer {
  text-align: center;
  margin-top: 20px;
  font-size: 14px;
  color: #000;
  opacity: 0.7;
}
</style>
</head>

<body>

<div class="calculator">
  <div class="title-box">BMI CALCULATOR</div>

  <label>DOB</label>
  <input id="dob" placeholder="DD/MM/YYYY">

  <label>Gender</label>
  <select id="gender">
    <option value="male">Male</option>
    <option value="female">Female</option>
  </select>

  <label>Weight</label>
  <div class="weight-box">
    <input type="number" id="weight" placeholder="Enter weight">
    <select id="unit">
      <option value="kg">KG</option>
      <option value="lb">LB</option>
    </select>
  </div>

  <label>Height</label>
  <input id="heightFeet" placeholder="Feet">
  <input id="heightInch" placeholder="Inch">

  <button onclick="calculateBMI()">RUN ANALYSIS</button>

  <div id="result" class="result"></div>
</div>

<div class="footer">Developed By Snk Technician Arman</div>

<script>
function getAge(dob){
  let parts = dob.split("/");
  if(parts.length !== 3) return null;
  let d = new Date(parts[2], parts[1]-1, parts[0]);
  let diff = Date.now() - d.getTime();
  return new Date(diff).getUTCFullYear() - 1970;
}

function calculateBMI(){

let w = parseFloat(document.getElementById("weight").value);
let unit = document.getElementById("unit").value;
let f = parseFloat(document.getElementById("heightFeet").value);
let i = parseFloat(document.getElementById("heightInch").value);

if(isNaN(i)) i = 0;

let dob = document.getElementById("dob").value;
let gender = document.getElementById("gender").value;

if(!w || !f){
document.getElementById("result").innerText = "INPUT ERROR";
return;
}

let age = getAge(dob);
if(!age){
document.getElementById("result").innerText = "INVALID DOB";
return;
}

let kg = unit == "lb" ? w * 0.453592 : w;
let h = (f * 12 + i) * 0.0254;

let bmi = kg / (h * h);
bmi = bmi.toFixed(1);

let minBMI = 18.5;
let maxBMI = 24.9;

if(gender === "female"){
  minBMI = 18;
  maxBMI = 24;
}

if(age < 18){
  minBMI = 17;
  maxBMI = 23;
}

let minWeight = minBMI * h * h;
let maxWeight = maxBMI * h * h;

let output = "";
let color = "";

if(bmi < minBMI){
let need = minWeight - kg;
output = `STATUS: UNDERWEIGHT
BMI: ${bmi}
NEED: +${need.toFixed(1)} kg (${(need*2.205).toFixed(1)} lb)
AGE: ${age}
ACTION: INCREASE CALORIE INTAKE & STRENGTH TRAINING`;
color = "#e6b800";
}
else if(bmi <= maxBMI){
output = `STATUS: NORMAL
BMI: ${bmi}
AGE: ${age}
CONDITION: GOOD
ACTION: MAINTAIN FITNESS`;
color = "green";
}
else{
let extra = kg - maxWeight;
output = `STATUS: OVERWEIGHT
BMI: ${bmi}
EXCESS: ${extra.toFixed(1)} kg (${(extra*2.205).toFixed(1)} lb)
AGE: ${age}
ACTION: CARDIO + FAT LOSS TRAINING`;
color = "red";
}

let resultBox = document.getElementById("result");
resultBox.innerText = output;
resultBox.style.color = color;

}
</script>

</body>
</html>

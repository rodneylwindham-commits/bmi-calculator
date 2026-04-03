<!Bangladesh Army Weight Calculator>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tactical BMI System</title>

<style>
body {
  background: #0a0f0a;
  font-family: "Courier New", monospace;
  color: #00ff9c;
  padding: 20px;
}

/* Main box */
.calculator {
  max-width: 450px;
  margin: auto;
  background: #020402;
  padding: 25px;
  border-radius: 10px;
  border: 2px solid #00ff9c;
  box-shadow: 0 0 20px #00ff9c44;
}

/* Title */
.title-box {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  padding: 10px;
  border: 2px solid #00ff9c;
  margin-bottom: 20px;
  letter-spacing: 2px;
  text-transform: uppercase;
  background: #001a00;
}

/* Label */
label {
  display: block;
  margin-top: 12px;
}

/* Inputs */
input, select {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  background: #000;
  color: #00ff9c;
  border: 1px solid #00ff9c;
  font-family: inherit;
}

/* Button */
button {
  width: 100%;
  padding: 12px;
  margin-top: 20px;
  background: #00ff9c;
  color: #000;
  border: none;
  font-weight: bold;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  background: #00cc7a;
}

/* Result */
.result {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #00ff9c;
  text-align: center;
  white-space: pre-line;
}

/* Footer */
.footer {
  text-align: center;
  margin-top: 20px;
  font-size: 14px;
  color: #00ff9c;
  opacity: 0.7;
}
</style>
</head>

<body>

<div class="calculator">

<div class="title-box">BMI CALCULATOR</div>

<label>DOB</label>
<input id="dob" placeholder="DD/MM/YYYY">

<label>Weight</label>
<input id="weight" type="number">

<select id="unit">
<option value="kg">KG</option>
<option value="lb">POUND</option>
</select>

<label>Height</label>
<input id="heightFeet" placeholder="Feet">
<input id="heightInch" placeholder="Inch">

<button onclick="calculateBMI()">RUN ANALYSIS</button>

<div id="result" class="result"></div>

</div>

<div class="footer">Developed By Snk Technician Arman</div>

<script>
function calculateBMI(){

let w = parseFloat(document.getElementById("weight").value);
let unit = document.getElementById("unit").value;
let f = parseFloat(document.getElementById("heightFeet").value);
let i = parseFloat(document.getElementById("heightInch").value);

if(!w || !f || !i){
document.getElementById("result").innerHTML="INPUT ERROR";
return;
}

// convert
let kg = unit=="lb" ? w*0.453592 : w;

// height meter
let h = (f*12+i)*0.0254;

// bmi
let bmi = kg/(h*h);
bmi = bmi.toFixed(1);

// range
let min = 18.5*h*h;
let max = 24.9*h*h;

let output="";

if(bmi<18.5){
let need = min-kg;
output = `STATUS: UNDERWEIGHT
BMI: ${bmi}
REQUIRED: +${need.toFixed(1)} kg (${(need*2.205).toFixed(1)} lb)
ACTION: INCREASE CALORIE INTAKE`;
}
else if(bmi<=24.9){
output = `STATUS: NORMAL
BMI: ${bmi}
ACTION: MAINTAIN CURRENT CONDITION`;
}
else{
let extra = kg-max;
output = `STATUS: OVERWEIGHT
BMI: ${bmi}
EXCESS: ${extra.toFixed(1)} kg (${(extra*2.205).toFixed(1)} lb)
ACTION: INITIATE TRAINING`;
}

document.getElementById("result").innerText = output;

}
</script>

</body>
</html>

<!Bangladesh Army Weight Calculator>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tactical BMI System</title><style>
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
</style></head><body>
<div class="calculator">
<div class="title-box">BMI CALCULATOR</div><label>DOB</label> <input id="dob" placeholder="DD/MM/YYYY">

<label>Gender</label> <select id="gender">

  <option value="male">Male</option>
  <option value="female">Female</option>
</select><label>Weight</label>

<div class="weight-box">
    <input type="number" id="weight" placeholder="Enter weight">
    <select id="unit">
        <option value="kg">KG</option>
        <option value="lb">LB</option>
    </select>
</div><label>Height</label> <input id="heightFeet" placeholder="Feet"> <input id="heightInch" placeholder="Inch">

<button onclick="calculateBMI()">RUN ANALYSIS</button>

<div id="result" class="result"></div>
</div><script>
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
let dob = document.getElementById("dob").value;
let gender = document.getElementById("gender").value;

if(!w || !f || i===null){
document.getElementById("result").innerHTML="INPUT ERROR";
return;
}

let age = getAge(dob);
if(!age){
document.getElementById("result").innerHTML="INVALID DOB";
return;
}

let kg = unit=="lb" ? w*0.453592 : w;
let h = (f*12+i)*0.0254;
let bmi = (kg/(h*h)).toFixed(1);

let minBMI = 18.5;
let maxBMI = 24.9;

// Gender adjustment
if(gender === "female"){
  minBMI = 18;
  maxBMI = 24;
}

// Age adjustment
if(age < 18){
  minBMI = 17;
  maxBMI = 23;
}

let minWeight = minBMI * h * h;
let maxWeight = maxBMI * h * h;

let output="";
let color="";

if(bmi < minBMI){
let need = minWeight - kg;
output = `STATUS: UNDERWEIGHT\nBMI: ${bmi}\nNEED: +${need.toFixed(1)} kg (${(need*2.205).toFixed(1)} lb)\nAGE: ${age}\nACTION: INCREASE CALORIE INTAKE & STRENGTH TRAINING`;
color = "#e6b800";
}
else if(bmi <= maxBMI){
output = `STATUS: NORMAL\nBMI: ${bmi}\nAGE: ${age}\nCONDITION: GOOD\nACTION: MAINTAIN DIET & FITNESS`;
color = "green";
}
else{
let extra = kg - maxWeight;
output = `STATUS: OVERWEIGHT\nBMI: ${bmi}\nEXCESS: ${extra.toFixed(1)} kg (${(extra*2.205).toFixed(1)} lb)\nAGE: ${age}\nACTION: FAT LOSS + CARDIO TRAINING`;
color = "red";
}

let resultBox = document.getElementById("result");
resultBox.innerText = output;
resultBox.style.color = color;
}
<div class="footer">Developed By Snk Technician Arman</div>
</script></body>


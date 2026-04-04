<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Army Standard Weight Calculator</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: linear-gradient(135deg, #013220, #6fbf73);
}

/* Header */
.header {
    text-align: center;
    padding: 15px;
    border: 3px solid black;
    background: #014421;
    color: white;
    font-size: 24px;
    font-weight: bold;
}

/* Container */
.container {
    width: 90%;
    max-width: 500px;
    margin: 20px auto;
    padding: 20px;
}

/* Inputs */
label {
    color: white;
    font-weight: bold;
}

input, select {
    width: 100%;
    padding: 10px;
    margin: 8px 0 15px;
    border-radius: 6px;
    border: none;
    background: white;
    color: black;
}

/* Height */
.height-box {
    display: flex;
    gap: 10px;
}

/* Button */
button {
    width: 100%;
    padding: 12px;
    background: #003366;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
}

button:hover {
    background: #0055aa;
}

/* Result */
.result {
    margin-top: 20px;
    padding: 15px;
    border-radius: 8px;
    font-weight: bold;
    text-align: center;
}

/* Footer */
.footer {
    text-align: center;
    padding: 15px;
    color: black;
    font-weight: bold;
}
</style>
</head>

<body>

<div class="header">
Army Standard Weight Calculator
</div>

<div class="container">

<label>Date of Birth (dd/mm/yyyy)</label>
<input type="text" id="dob" placeholder="dd/mm/yyyy">

<label>Weight</label>
<input type="number" id="weight" placeholder="Enter weight">
<select id="unit">
    <option value="kg">KG</option>
    <option value="lb">Pound</option>
</select>

<label>Height</label>
<div class="height-box">
    <input type="number" id="feet" placeholder="Feet">
    <input type="number" id="inch" placeholder="Inch">
</div>

<label>Gender</label>
<select>
    <option>Male</option>
    <option>Female</option>
</select>

<button onclick="calculate()">Calculate</button>

<div id="result" class="result"></div>

</div>

<div class="footer">
Developed By Snk Technician Arman
</div>

<script>

// MIN weight
const minW = {
"5-2":47,"5-3":49,"5-4":50,"5-5":52,"5-6":53,"5-7":55,
"5-8":57,"5-9":58,"5-10":60,"5-11":62,
"6-0":64,"6-1":65,"6-2":67
};

// MAX weight
const maxW = {
u30:{
"5-2":62,"5-3":64,"5-4":66,"5-5":68,"5-6":70,"5-7":72,
"5-8":75,"5-9":77,"5-10":79,"5-11":81,
"6-0":84,"6-1":86,"6-2":88
},
a31:{
"5-2":66,"5-3":68,"5-4":70,"5-5":72,"5-6":74,"5-7":77,
"5-8":79,"5-9":81,"5-10":84,"5-11":86,
"6-0":89,"6-1":91,"6-2":94
},
a41:{
"5-2":67,"5-3":69,"5-4":71,"5-5":74,"5-6":76,"5-7":78,
"5-8":81,"5-9":83,"5-10":85,"5-11":88,
"6-0":90,"6-1":93,"6-2":95
},
a50:{
"5-2":68,"5-3":70,"5-4":73,"5-5":75,"5-6":77,"5-7":80,
"5-8":82,"5-9":84,"5-10":87,"5-11":89,
"6-0":92,"6-1":95,"6-2":97
}
};

// AGE
function getAge(d){
let p = d.split("/");
if(p.length!==3) return null;
let b = new Date(p[2],p[1]-1,p[0]);
let t = new Date();
let age = t.getFullYear()-b.getFullYear();
return age;
}

function calculate(){

let dob = document.getElementById("dob").value;
let w = parseFloat(document.getElementById("weight").value);
let unit = document.getElementById("unit").value;
let f = document.getElementById("feet").value;
let i = document.getElementById("inch").value;
let res = document.getElementById("result");

// validation
if(!dob || !w || !f){
res.innerHTML="সব তথ্য সঠিকভাবে দিন!";
res.style.background="orange";
return;
}

// convert lb → kg
if(unit==="lb") w = w/2.20462;

let key = f+"-"+i;

if(!minW[key]){
res.innerHTML="এই height সাপোর্টেড না!";
res.style.background="orange";
return;
}

let age = getAge(dob);
if(age===null){
res.innerHTML="DOB ভুল!";
res.style.background="orange";
return;
}

let min = minW[key];
let max;

if(age<=30) max = maxW.u30[key];
else if(age<=40) max = maxW.a31[key];
else if(age<=50) max = maxW.a41[key];
else max = maxW.a50[key];

// UNDER
if(w < min){
res.style.background="yellow";
res.style.color="black";
res.innerHTML="Under Weight ⚠️<br>পুষ্টিকর খাবার খান";
}

// OVER
else if(w > max){
let diff = (w-max).toFixed(2);
let lb = (diff*2.20462).toFixed(2);

res.style.background="red";
res.style.color="white";
res.innerHTML=`
Over Weight ❌<br>
Extra: ${diff} KG (${lb} LB)<br>
খাওয়া কমান + এক্সারসাইজ করুন
`;
}

// NORMAL
else{
res.style.background="green";
res.style.color="white";
res.innerHTML="Normal Weight ✅";
}

}

</script>

</body>
</html>

<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<title>Army Weight Calculator</title>

<style>
body{
    font-family: Arial;
    text-align: center;
    background:#0f172a;
    color:white;
}
input,select,button{
    padding:10px;
    margin:8px;
    border-radius:8px;
    border:none;
}
button{
    background:green;
    color:white;
}
#result{
    margin-top:20px;
    padding:15px;
    border-radius:10px;
}
</style>
</head>

<body>

<h2>Army Standard Weight Calculator</h2>

<input type="date" id="dob"><br>

<input type="number" id="weight" placeholder="Enter Weight"><br>

<select id="unit">
    <option value="kg">KG</option>
    <option value="lb">LB</option>
</select><br>

<select id="feet">
    <option value="">Feet</option>
    <option value="5">5</option>
    <option value="6">6</option>
</select>

<select id="inch">
    <option value="">Inch</option>
    <option value="0">0</option>
    <option value="1">1</option>
    <option value="2">2</option>
    <option value="3">3</option>
    <option value="4">4</option>
    <option value="5">5</option>
    <option value="6">6</option>
    <option value="7">7</option>
    <option value="8">8</option>
    <option value="9">9</option>
    <option value="10">10</option>
    <option value="11">11</option>
</select><br>

<button onclick="check()">Check</button>

<div id="result"></div>

<script>

// ===== DATA =====
const minW = {
"5-2":47,"5-3":49,"5-4":50,"5-5":52,"5-6":53,
"5-7":55,"5-8":57,"5-9":58,"5-10":60,"5-11":62,
"6-0":64,"6-1":65,"6-2":67
};

const maxW = {
u30:{"5-2":62,"5-3":64,"5-4":66,"5-5":68,"5-6":70,"5-7":72,"5-8":75,"5-9":77,"5-10":79,"5-11":81,"6-0":84,"6-1":86,"6-2":88},
a31:{"5-2":66,"5-3":68,"5-4":70,"5-5":72,"5-6":74,"5-7":77,"5-8":79,"5-9":81,"5-10":84,"5-11":86,"6-0":89,"6-1":91,"6-2":94},
a41:{"5-2":67,"5-3":69,"5-4":71,"5-5":74,"5-6":76,"5-7":78,"5-8":81,"5-9":83,"5-10":85,"5-11":88,"6-0":90,"6-1":93,"6-2":95},
a50:{"5-2":68,"5-3":70,"5-4":73,"5-5":75,"5-6":77,"5-7":80,"5-8":82,"5-9":84,"5-10":87,"5-11":89,"6-0":92,"6-1":95,"6-2":97}
};

// ===== AGE =====
function getAgeDetails(dob){
let birth = new Date(dob);
let today = new Date();

let y = today.getFullYear() - birth.getFullYear();
let m = today.getMonth() - birth.getMonth();
let d = today.getDate() - birth.getDate();

if(d < 0){ m--; d += 30; }
if(m < 0){ y--; m += 12; }

return {y,m,d};
}

// ===== MAIN =====
function check(){

let dob = document.getElementById("dob").value;
let w = parseFloat(document.getElementById("weight").value);
let unit = document.getElementById("unit").value;
let f = document.getElementById("feet").value;
let i = document.getElementById("inch").value;

let res = document.getElementById("result");

// validation
if(!dob || !w || f==="" || i===""){
res.innerHTML="সব তথ্য দিন



Note:
a. A maximum of 20 pounds weight waiver may be allowed for athletes such as wrestlers, boxers, throwers, or any other classified personnel (certified by the Commanding Officer or equivalent of the unit).
b. All measurements will be taken in uniform, and 7 pounds will be deducted to determine the actual body weight. Personnel below the minimum weight (underweight) will be subject to medical evaluation.
c. If an individual remains within the normal weight range but has a waist-hip ratio exceeding 1.0, the person will be considered obese and should undergo a special program.
d. In exceptional cases, a special medical board may be convened by the appropriate medical authority. The board will consider body frame size, waist-hip ratio, percentage of body fat, and overall physical performance before declaring the individual fit.


<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Smart Calculator</title>

<style>
body { 
  font-family: Arial, sans-serif; 
  background: #f4f4f4; 
  padding: 20px; 
}

.calculator { 
  max-width: 450px; 
  margin: auto; 
  background: #fff; 
  padding: 25px; 
  border-radius: 12px; 
  box-shadow: 0 6px 15px rgba(0,0,0,0.1); 
}

/* 🔥 Premium Title */
.title-box {
  text-align: center;
  font-size: 22px;
  font-weight: bold;
  color: #111;
  border: 2px solid gold;
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 20px;
  background: #C9A227;
  box-shadow: 0 0 10px rgba(255, 215, 0, 0.5);
}

label { 
  display: block; 
  margin-top: 12px; 
  font-weight: bold; 
}

input, select { 
  width: 100%; 
  padding: 10px; 
  margin-top: 5px; 
  border-radius: 5px; 
  border: 1px solid #ccc; 
  box-sizing: border-box; 
}

/* 💧 Glossy Button */
button { 
  width: 100%; 
  padding: 12px; 
  background: linear-gradient(to bottom, #4da6ff, #0066cc);
  color: #fff; 
  border: none; 
  border-radius: 8px; 
  cursor: pointer; 
  font-size: 16px; 
  margin-top: 20px; 
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
  transition: 0.3s;
}

button:hover { 
  background: linear-gradient(to bottom, #66b3ff, #0052a3);
}

.result { 
  margin-top: 20px; 
  padding: 15px; 
  border-radius: 8px; 
  text-align: center; 
  font-weight: bold; 
  line-height: 1.5; 
  color: #fff; 
}

/* 🌈 Developer Gradient Text */
.footer { 
  text-align: center; 
  margin-top: 30px; 
  font-size: 16px; 
  font-weight: bold; 
  background: linear-gradient(90deg, #000, #aaa, #000);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
</head>

<body>

<div class="calculator">
    
    <h2 class="title-box">BMI Smart Calculator</h2>
    
    <label>Date of Birth (DD/MM/YYYY)</label>
    <input type="text" id="dob" placeholder="e.g., 20/06/2015">

    <label>Gender</label>
    <select id="gender">
        <option value="male">Male</option>
        <option value="female">Female</option>
    </select>

    <label>Weight (kg)</label>
    <input type="number" id="weight" placeholder="e.g., 30">

    <label>Height</label>
    <div style="display:flex; gap:10px;">
        <input type="number" id="heightFeet" placeholder="Feet" style="flex:1;">
        <input type="number" id="heightInch" placeholder="Inches" style="flex:1;">
    </div>
    
    <button onclick="calculateBMI()">Calculate BMI</button>
    
    <div class="result" id="result"></div>
</div>

<div class="footer">
  Developed By Snk Technician Arman
</div>

<script>
function calculateBMI() {
    let dobInput = document.getElementById("dob").value.trim();
    let gender = document.getElementById("gender").value;
    let weight = parseFloat(document.getElementById("weight").value);
    let heightFeet = parseFloat(document.getElementById("heightFeet").value);
    let heightInch = parseFloat(document.getElementById("heightInch").value);

    if(!dobInput || !weight || !heightFeet || !heightInch){
        document.getElementById("result").innerHTML = "Please fill all fields.";
        document.getElementById("result").style.backgroundColor = "#555";
        return;
    }

    let birthDateParts = dobInput.split("/");
    if(birthDateParts.length !== 3){
        document.getElementById("result").innerHTML = "Invalid DOB format. Use DD/MM/YYYY";
        document.getElementById("result").style.backgroundColor = "#555";
        return;
    }

    let birthDate = new Date(birthDateParts[2], birthDateParts[1]-1, birthDateParts[0]);
    let today = new Date();
    let age = today.getFullYear() - birthDate.getFullYear();
    let m = today.getMonth() - birthDate.getMonth();
    if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) { age--; }

    let heightMeters = (heightFeet * 12 + heightInch) * 0.0254;

    let bmi = weight / (heightMeters * heightMeters);
    bmi = Math.round(bmi * 100) / 100;

    let category = "";
    let advice = "";
    let color = "";

    if(age >= 18){
        if(bmi < 18.5) { category="Underweight"; advice="Eat nutritious foods, gain weight gradually."; color="#2196F3"; }
        else if(bmi < 24.9) { category="Normal weight"; advice="Maintain a balanced diet and regular exercise."; color="#4CAF50"; }
        else if(bmi < 29.9) { category="Overweight"; advice="Exercise regularly and control diet."; color="#FF5722"; }
        else { category="Obese"; advice="Consult a doctor, follow diet and exercise plan."; color="#F44336"; }
    } else {
        if(gender === "male"){
            if(bmi < 14) { category="<5% (Underweight)"; advice="Ensure balanced diet, monitor growth."; color="#2196F3"; }
            else if(bmi < 18) { category="5-85% (Normal)"; advice="Encourage active play and healthy meals."; color="#4CAF50"; }
            else if(bmi < 20) { category="85-95% (Overweight)"; advice="Limit sugary foods, encourage physical activity."; color="#FF5722"; }
            else { category=">95% (Obese)"; advice="Consult pediatrician for guidance."; color="#F44336"; }
        } else {
            if(bmi < 13.5) { category="<5% (Underweight)"; advice="Ensure balanced diet, monitor growth."; color="#2196F3"; }
            else if(bmi < 17.5) { category="5-85% (Normal)"; advice="Encourage active play and healthy meals."; color="#4CAF50"; }
            else if(bmi < 19.5) { category="85-95% (Overweight)"; advice="Limit sugary foods, encourage physical activity."; color="#FF5722"; }
            else { category=">95% (Obese)"; advice="Consult pediatrician for guidance."; color="#F44336"; }
        }
    }

    document.getElementById("result").innerHTML = `Age: ${age} years<br>BMI: ${bmi} - ${category}<br>${advice}`;
    document.getElementById("result").style.backgroundColor = color;
}
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BMI Calculator</title>
<style>
    body { font-family: Arial, sans-serif; background: #f4f4f4; padding: 20px; }
    .calculator { max-width: 400px; margin: auto; background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
    h2 { text-align: center; color: #333; }
    input, select { width: 100%; padding: 10px; margin: 10px 0; border-radius: 5px; border: 1px solid #ccc; }
    button { width: 100%; padding: 10px; background: #0077cc; color: #fff; border: none; border-radius: 5px; cursor: pointer; font-size: 16px; }
    button:hover { background: #005fa3; }
    .result { margin-top: 20px; padding: 10px; background: #e3f2fd; border-radius: 5px; text-align: center; font-weight: bold; }
    .footer { text-align: center; margin-top: 30px; color: #555; font-size: 14px; font-style: italic; }
</style>
</head>
<body>

<div class="calculator">
    <h2>BMI Calculator</h2>
    
    <label>Weight (kg)</label>
    <input type="number" id="weight" placeholder="e.g., 30">
    
    <label>Height (meters)</label>
    <input type="number" step="0.01" id="height" placeholder="e.g., 1.2">
    
    <label>Age (years)</label>
    <input type="number" id="age" placeholder="e.g., 10">
    
    <label>Gender</label>
    <select id="gender">
        <option value="male">Male</option>
        <option value="female">Female</option>
    </select>
    
    <button onclick="calculateBMI()">Calculate BMI</button>
    
    <div class="result" id="result"></div>
</div>

<div class="footer">
    Developed by SNK Technician Arman (4SigBn)
</div>

<script>
function calculateBMI() {
    let weight = parseFloat(document.getElementById("weight").value);
    let height = parseFloat(document.getElementById("height").value);
    let age = parseInt(document.getElementById("age").value);
    let gender = document.getElementById("gender").value;
    
    if(!weight || !height || !age){
        document.getElementById("result").innerText = "Please fill all fields.";
        return;
    }
    
    let bmi = weight / (height * height);
    bmi = Math.round(bmi * 100) / 100;
    
    let category = "";

    if(age >= 18){
        // Adults BMI
        if(bmi < 18.5) category = "Underweight";
        else if(bmi < 24.9) category = "Normal weight";
        else if(bmi < 29.9) category = "Overweight";
        else category = "Obese";
        document.getElementById("result").innerText = `BMI: ${bmi} - ${category}`;
    } else {
        // Children simplified percentile approximation
        let percentile = 0;

        if(gender === "male"){
            if(bmi < 14) percentile = "<5% (Underweight)";
            else if(bmi < 18) percentile = "5-85% (Normal)";
            else if(bmi < 20) percentile = "85-95% (Overweight)";
            else percentile = ">95% (Obese)";
        } else {
            if(bmi < 13.5) percentile = "<5% (Underweight)";
            else if(bmi < 17.5) percentile = "5-85% (Normal)";
            else if(bmi < 19.5) percentile = "85-95% (Overweight)";
            else percentile = ">95% (Obese)";
        }

        document.getElementById("result").innerText = `BMI: ${bmi} - Children: ${percentile}`;
    }
}
</script>

</body>
</html>  const heightMeters = ((feet * 12) + inches) * 0.0254;

  const bmi = weight / (heightMeters * heightMeters);
  const bmiRounded = bmi.toFixed(1);

  let status = "";
  let advice = "";
  let color = "";

  if (bmi < 18.5) {
    status = "Underweight";
    advice = "Oh Shit! You should eat nutritious food to gain healthy weight.";
    color = "#3498db";
  } else if (bmi <= 25) {
    status = "Normal weight";
    advice = "Excellent! Maintain your current weight and healthy lifestyle.";
    color = "#2ecc71";
  } else if (bmi < 30) {
    status = "Overweight";
    advice = "You are overweight. Consider controlling your diet and exercising.";
    color = "#e67e22";
  } else {
    status = "Overweight";
    advice = "You are overweight. Seek medical advice and follow a healthy diet plan.";
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

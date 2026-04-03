<script>
function calculateBMI() {

let dob = document.getElementById("dob").value.trim();
let gender = document.getElementById("gender").value;
let weight = parseFloat(document.getElementById("weight").value);
let unit = document.getElementById("unit").value;
let feet = parseFloat(document.getElementById("heightFeet").value);
let inch = parseFloat(document.getElementById("heightInch").value);

if(!dob || !weight || !feet || !inch){
document.getElementById("result").innerHTML="Please fill all fields.";
document.getElementById("result").style.backgroundColor="#555";
return;
}

// convert pound → kg
let weightKg = (unit === "lb") ? weight * 0.453592 : weight;

// height meter
let height = (feet*12 + inch)*0.0254;

// BMI
let bmi = weightKg / (height*height);
bmi = Math.round(bmi * 100) / 100;

// ideal weight range
let minWeight = 18.5 * height * height;
let maxWeight = 24.9 * height * height;

let category = "";
let advice = "";
let color = "";
let diffText = "";

// Adult condition only (same as before)
if(bmi < 18.5){
category="Underweight";
advice="You should eat nutritious food to gain healthy weight.";
let need = (minWeight - weightKg);
diffText = `You need +${need.toFixed(1)} kg (${(need*2.205).toFixed(1)} lb)`;
color="#2196F3";
}
else if(bmi <= 24.9){
category="Normal weight";
advice="Maintain your current weight and healthy lifestyle.";
color="#4CAF50";
}
else if(bmi < 29.9){
category="Overweight";
advice="You are overweight. Consider controlling your diet and exercising.";
let extra = (weightKg - maxWeight);
diffText = `You have +${extra.toFixed(1)} kg (${(extra*2.205).toFixed(1)} lb) extra`;
color="#FF5722";
}
else{
category="Obese";
advice="You are obese. Seek medical advice and follow a healthy diet plan.";
let extra = (weightKg - maxWeight);
diffText = `You have +${extra.toFixed(1)} kg (${(extra*2.205).toFixed(1)} lb) extra`;
color="#F44336";
}

document.getElementById("result").innerHTML =
`BMI: ${bmi} (${category})<br>${diffText}<br>${advice}`;

document.getElementById("result").style.backgroundColor = color;

}
</script><div class="footer">
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

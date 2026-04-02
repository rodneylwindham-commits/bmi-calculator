<script>
function calculateBMI() {
  const weight = parseFloat(document.getElementById('weight').value);
  const feet = parseFloat(document.getElementById('feet').value);
  const inches = parseFloat(document.getElementById('inches').value);
  const birthdayInput = document.getElementById('birthday').value.trim();

  if(!weight || !feet || inches < 0 || !birthdayInput) {
    alert('Please enter valid height, weight, and birthday.');
    return;
  }

  // Parse DD/MM/YYYY
  const parts = birthdayInput.split('/');
  if(parts.length !== 3) {
    alert('Please enter birthday in DD/MM/YYYY format.');
    return;
  }

  const day = parseInt(parts[0], 10);
  const month = parseInt(parts[1], 10) - 1;
  const year = parseInt(parts[2], 10);

  const birthDate = new Date(year, month, day);

  if(isNaN(birthDate.getTime())) {
    alert('Invalid birth date.');
    return;
  }

  // Age calculate
  const today = new Date();
  let years = today.getFullYear() - year;
  let months = today.getMonth() - month;
  let days = today.getDate() - day;

  if(days < 0) {
    months -= 1;
    days += new Date(today.getFullYear(), today.getMonth(), 0).getDate();
  }

  if(months < 0) {
    years -= 1;
    months += 12;
  }

  const ageStr = `${years} years, ${months} months, ${days} days`;

  // Height to meters
  const heightMeters = ((feet * 12) + inches) * 0.0254;

  // BMI
  const bmi = weight / (heightMeters * heightMeters);
  const bmiRounded = bmi.toFixed(1);

  let status = "";
  let advice = "";
  let color = "";

  if (bmi < 18.5) {
    status = "Underweight";
    advice = "You should eat nutritious food.";
    color = "#3498db";
  } else if (bmi < 25) {
    status = "Normal";
    advice = "Maintain your current weight.";
    color = "#2ecc71";
  } else if (bmi < 30) {
    status = "Overweight";
    advice = "Consider exercise.";
    color = "#e67e22";
  } else {
    status = "Obese";
    advice = "Seek medical advice.";
    color = "#e74c3c";
  }

  const statusEl = document.getElementById('status');
  statusEl.innerText =
    `Age: ${ageStr}\nBMI: ${bmiRounded} (${status})\n${advice}`;
  statusEl.style.color = color;
}
</script>

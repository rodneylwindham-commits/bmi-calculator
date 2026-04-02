<!DOCTYPE html>
<html>
<head>
  <title>BMI Calculator</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      margin-top: 50px;
    }
    input {
      padding: 10px;
      margin: 5px;
    }
    button {
      padding: 10px 20px;
      background: green;
      color: white;
      border: none;
    }
  </style>
</head>

<body>

  <h1>BMI Calculator</h1>

  <input type="number" id="weight" placeholder="Weight (kg)">
  <br>
  <input type="number" id="feet" placeholder="Height (feet)">
  <input type="number" id="inch" placeholder="Inch">
  <br><br>

  <button onclick="calculateBMI()">Calculate</button>

  <h2 id="result"></h2>

  <script>
    function calculateBMI() {
      let weight = document.getElementById("weight").value;
      let feet = document.getElementById("feet").value;
      let inch = document.getElementById("inch").value;

      let height = (feet * 0.3048) + (inch * 0.0254);
      let bmi = weight / (height * height);

      document.getElementById("result").innerText = "Your BMI: " + bmi.toFixed(2);
    }
  </script>

</body>
</html>

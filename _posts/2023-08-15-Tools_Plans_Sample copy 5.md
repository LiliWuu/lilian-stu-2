---
toc: true
comments: false
layout: default
title: JS Calculator
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
type: hacks
courses: { compsci: {week: 4} }
---

<br><br><br><br>

<!--<!DOCTYPE html>-->
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>4 Function Calculator</title>


<h2>4 Function Calculator</h2>

<style>
  body{
    background-color: black; /* Set the background color to black */
    color: white; /* Set the text color to white for better readability */
  }

  h2{
    text-align: center;
    font-size: 22px;
    text-decoration: underline;
    font-family: monospace;
  }
  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px; /* Add some gap between the buttons for better visual separation */
    width: 400px; /* Set a fixed width for the calculator container */
    margin: 0 auto; /* Center the calculator horizontally on the page */
    margin-top: 50px; /* Adjust this value as needed */
    padding: 10px; /* Add some padding to the container */
    border: 2px solid green;
  }
  .calculator-output {
    /* Calculator output */
    grid-column: span 4;
    grid-row: span 1;
    border-radius: 10px;
    padding: 0.25em;
    font-size: 20px;
    border: 5px solid green;
    display: flex;
    align-items: center;
  }

  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
  }
  
  /* Add styles for calculator buttons */
  .calculator-button {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    border: 2px solid green;
    cursor: pointer;
  }
</style>
</head>
<body>
  <!-- Add a container for the animation -->
  <div id="animation">
    <div class="calculator-container">
      <!--result-->
      <div class="calculator-output" id="output">0</div>
      <!--row 1-->
<div class="calculator-button calculator-number">1</div>
<div class="calculator-button calculator-number">2</div>
<div class="calculator-button calculator-number">3</div>
<div class="calculator-button calculator-operation">+</div>
<!--row 2-->
<div class="calculator-button calculator-number">4</div>
<div class="calculator-button calculator-number">5</div>
<div class="calculator-button calculator-number">6</div>
<div class="calculator-button calculator-operation">-</div>
<!--row 3-->
<div class="calculator-button calculator-number">7</div>
<div class="calculator-button calculator-number">8</div>
<div class="calculator-button calculator-number">9</div>
<div class="calculator-button calculator-operation">*</div>
<!--row 4-->
<div class="calculator-button calculator-clear">A/C</div>
<div class="calculator-button calculator-number">0</div>
<div class="calculator-button calculator-number">.</div>
<div class="calculator-button calculator-operation">/</div>
<div class="calculator-button calculator-equals">=</div>
    </div>
  </div>

<!-- JavaScript (JS) implementation of the calculator. -->
<script>
// Keyboard event listener
document.addEventListener("keydown", function(event) {
  const key = event.key;

  // Check if the pressed key is a number key (0-9) or the decimal point key.
  if (!isNaN(key) || key === ".") {
    number(key);
  } else if (key === "+" || key === "-" || key === "*" || key === "/") {
    operation(key);
  } else if (key === "Enter") {
    equal();
  } else if (key === "Tab") {
    clearCalc(); // Call clearCalc when the "Tab" key is pressed.
  }
});
// initialize important variables to manage calculations
var firstNumber = null;
var operator = null;
var nextReady = true;
// build objects containing key elements
const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");

// Number buttons listener
numbers.forEach(button => {
  button.addEventListener("click", function() {
    number(button.textContent);
  });
});

// Number action
function number (value) { // function to input numbers into the calculator
    if (value != ".") {
        if (nextReady == true) { // nextReady is used to tell the computer when the user is going to input a completely new number
            output.innerHTML = value;
            if (value != "0") { // if statement to ensure that there are no multiple leading zeroes
                nextReady = false;
            }
        } else {
            output.innerHTML = output.innerHTML + value; // concatenation is used to add the numbers to the end of the input
        }
    } else { // special case for adding a decimal; can't have two decimals
        if (output.innerHTML.indexOf(".") == -1) {
            output.innerHTML = output.innerHTML + value;
            nextReady = false;
        }
    }
}

// Operation buttons listener
operations.forEach(button => {
  button.addEventListener("click", function() {
    operation(button.textContent);
  });
});

// Operator action
function operation (choice) { // function to input operations into the calculator
    if (firstNumber == null) { // once the operation is chosen, the displayed number is stored into the variable firstNumber
        firstNumber = parseInt(output.innerHTML);
        nextReady = true;
        operator = choice;
        return; // exits function
    }
    // occurs if there is already a number stored in the calculator
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML)); 
    operator = choice;
    output.innerHTML = firstNumber.toString();
    nextReady = true;
}

// Calculator
function calculate (first, second) { // function to calculate the result of the equation
    let result = 0;
    switch (operator) {
        case "+":
            result = first + second;
            break;
        case "-":
            result = first - second;
            break;
        case "*":
            result = first * second;
            break;
        case "/":
            result = first / second;
            break;
        default: 
            break;
    }
    return result;
}

// Equals button listener
equals.forEach(button => {
  button.addEventListener("click", function() {
    equal();
  });
});

// Equal action
function equal () { // function used when the equals button is clicked; calculates equation and displays it
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
    output.innerHTML = firstNumber.toString();
    nextReady = true;
}

// Clear button listener
clear.forEach(button => {
  button.addEventListener("click", function() {
    clearCalc();
  });
});

// A/C action
function clearCalc () { // clears calculator
    firstNumber = null;
    output.innerHTML = "0";
    nextReady = true;
}
</script>

<!-- 
Vanta animations just for fun, load JS onto the page
-->
<script src="/teacher/assets/js/three.r119.min.js"></script>
<script src="/teacher/assets/js/vanta.halo.min.js"></script>
<script src="/teacher/assets/js/vanta.birds.min.js"></script>
<script src="/teacher/assets/js/vanta.net.min.js"></script>
<script src="/teacher/assets/js/vanta.rings.min.js"></script>

<script>
// setup vanta scripts as functions
var vantaInstances = {
  halo: VANTA.HALO,
  birds: VANTA.BIRDS,
  net: VANTA.NET,
  rings: VANTA.RINGS
};

// obtain a random vanta function
var vantaInstance = vantaInstances[Object.keys(vantaInstances)[Math.floor(Math.random() * Object.keys(vantaInstances).length)]];

// run the animation
vantaInstance({
  el: "#animation",
  mouseControls: true,
  touchControls: true,
  gyroControls: false
});

</script>
<br>
<ul style="color: ;">
  <li>Press the buttons or keys that correspond to the correct symbols/numbers</li>
  <li>Enter to see the output</li>
  <li>Tab to reset the values</li>
</ul>
</body>
</html>
---
toc: true
comments: false
layout: post
title: Calculator MD
description: Grab of the Calculator from APCSA repo.
type: tangibles
courses: { compsci: {week: 2} }
---

<style>
 .calculator-output {
 /* calulator output 
 top bar shows the results of the calculator;
 result to take up the entirety of the first row;
 span defines 4 columns and 1 row
 */
 grid-column: span 4;
 grid-row: span 1;
 
 padding: 0.25em;
 font-size: 20px;
 border: 5px solid black;
 
 display: flex;
 align-items: center;
 }
</style>

<!-- Add a container for the animation -->
<div id="animation">
 <div class="calculator-container">
 <!--result-->
 <div class="calculator-output" id="output">0</div>
 <!--row 1-->
 <div class="calculator-number">1</div>
 <div class="calculator-number">2</div>
 <div class="calculator-number">3</div>
 <div class="calculator-operation">+</div>
 <!--row 2-->
 <div class="calculator-number">4</div>
 <div class="calculator-number">5</div>
 <div class="calculator-number">6</div>
 <div class="calculator-operation">-</div>
 <!--row 3-->
 <div class="calculator-number">7</div>
 <div class="calculator-number">8</div>
 <div class="calculator-number">9</div>
 <div class="calculator-operation">*</div>
 <!--row 4-->
 <div class="calculator-clear">A/C</div>
 <div class="calculator-number">0</div>
 <div class="calculator-number">.</div>
 <div class="calculator-operation">/</div> <!-- New divide button -->
 <div class="calculator-equals">=</div>
 </div>
</div>

<!-- JavaScript (JS) implementation of the calculator. -->
<script>
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
 function number(value) {
 if (value != ".") {
 if (nextReady == true) {
 output.innerHTML = value;
 if (value != "0") {
 nextReady = false;
 }
 } else {
 output.innerHTML = output.innerHTML + value;
 }
 } else {
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

 // Divide button listener
 const divide = document.querySelector(".calculator-operation:contains('/')"); // Assuming you are using jQuery
 divide.addEventListener("click", function() {
 operation(divide.textContent);
 });

 // Operator action
 function operation(choice) {
 if (firstNumber == null) {
 firstNumber = parseInt(output.innerHTML);
 nextReady = true;
 operator = choice;
 return;
 }

 firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
 operator = choice;
 output.innerHTML = firstNumber.toString();
 nextReady = true;
 }

 // Calculator
 function calculate(first, second) {
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
 function equal() {
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
 function clearCalc() {
 firstNumber = null;
 output.innerHTML = "0";
 nextReady = true;
 }
</script>

<!-- Add a new style script to set the background color to purple -->
<script>
 document.addEventListener('DOMContentLoaded', function () {
 document.body.style.backgroundColor = 'purple';
 });
</script>
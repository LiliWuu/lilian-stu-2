---
toc: true
comments: false
layout: post
title: JS Input
description: A calculator that allows the user to input their assignments, grades, and outputs the average grade.
type: hacks
courses: { compsci: {week: 4} }
---
<br><br><br>
<!--<!DOCTYPE html>-->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
</head>
<body>
    <div id="wrapper">
        <span style="color: maroon; text-decoration: underline wavy; font-family: 'copperplate', serif; font-size: 25px;">Grade Calculator</span>
        <br>
        <!-- Help Message -->
        <h3 style="font-size: 15px; color: purple; font-family: 'papyrus', sans-serif;"> (Input scores, press tab/enter to add each new number and get an output)</h3>
        <!-- Totals -->
        <table>
            <tr>
                <!-- New column for Assignment Names -->
                <th style="background-color: #FFC0CB;">Assignment Names (optional):</th>
                <!-- New column for Grades -->
                <th style="background-color: #87CEEB;">Grades :</th>
                <th style="background-color: #98FB98;">Average :</th>
            </tr>
            <tr>
                <td style="background-color: #FFC0CB;"><span id="assignments">N/A</span></td>
                <td style="background-color: #87CEEB;"><span id="grades">N/A</span></td>
                <td style="background-color: #98FB98;"><span id="average">0.0</span></td>
            </tr>
        </table>
        <!-- Rows added using scores ID -->
        <div id="scores">
            <!-- JavaScript-generated inputs for scores -->
        </div>
        <!-- Rows added using assignments ID -->
        <div id="assignments">
            <!-- JavaScript-generated inputs for assignment names -->
        </div>
        <!-- Reset button -->
        <button id="resetButton">Reset All</button>
        <!-- Load button -->
        <button id="loadButton">Load Data from Local Storage</button>
        <!-- Save button -->
        <button id="saveButton">Save Data to Local Storage</button>
    </div>

<script>
    // Function to save data to local storage
function saveDataToLocalStorage() {
    var data = {
        scores: [],
        assignmentNames: []
    };

    // Save scores
    var scoreElements = document.getElementsByName('score');
    scoreElements.forEach(function(scoreElement) {
        data.scores.push(scoreElement.value);
    });

    // Save assignment names
    var assignmentNameElements = document.getElementsByName('assignmentName');
    assignmentNameElements.forEach(function(assignmentNameElement) {
        data.assignmentNames.push(assignmentNameElement.value);
    });

    // Store the data as a JSON string in local storage
    localStorage.setItem('gradeData', JSON.stringify(data));
}

        // Function to load data from local storage
function loadDataFromLocalStorage() {
    var storedData = localStorage.getItem('gradeData');
    if (storedData) {
        var parsedData = JSON.parse(storedData);

        // Populate scores
        var scoreElements = document.getElementsByName('score');
        parsedData.scores.forEach(function (score, index) {
            if (scoreElements[index]) {
                scoreElements[index].value = score;
            } else {
                // Create a new input field if there are more scores in the loaded data
                newInputLine(index);
                scoreElements = document.getElementsByName('score'); // Update the array
                scoreElements[index].value = score;
            }
        });

        // Populate assignment names
        var assignmentNameElements = document.getElementsByName('assignmentName');
        parsedData.assignmentNames.forEach(function (assignmentName, index) {
            if (assignmentNameElements[index]) {
                assignmentNameElements[index].value = assignmentName;
            } else {
                // Create a new input field if there are more assignment names in the loaded data
                newAssignmentLine(index);
                assignmentNameElements = document.getElementsByName('assignmentName'); // Update the array
                assignmentNameElements[index].value = assignmentName;
            }
        });
    }
}

        // Call this function to load data from local storage when the page loads
        loadDataFromLocalStorage();

        // Button click event handler to load data from local storage
        document.getElementById("loadButton").addEventListener("click", function() {
            loadDataFromLocalStorage();
        });

        // Button click event handler to save data to local storage
        document.getElementById("saveButton").addEventListener("click", function() {
            saveDataToLocalStorage();
        });

    
// Executes on input event and calculates totals
function calculator(event) {
var key = event.key;
// Check if the pressed key is the "Tab" key (key code 9) or "Enter" key (key code 13)
if (key === "Tab" || key === "Enter") {
event.preventDefault(); // Prevent default behavior (tabbing to the next element)
var array = document.getElementsByName('score'); // setup array of scores
var total = 0; // running total
var count = 0; // count of input elements with valid values


for (var i = 0; i < array.length; i++) { // iterate through array
var value = array[i].value;
if (parseFloat(value)) {
var parsedValue = parseFloat(value);
total += parsedValue; // add to running total
count++;
}
}


if (count > 0) {
document.getElementById('average').innerHTML = (total / count).toFixed(2);
} else {
document.getElementById('average').innerHTML = "0.0";
}


// Calculate and update grades (you can customize this logic)
var grades = calculateGrades(total / count);
document.getElementById('grades').innerHTML = grades;
// adds newInputLine, only if all array values satisfy parseFloat
if (count === document.getElementsByName('score').length) {
newInputLine(count); // make a new input line for scores
}
}
}


// Function to calculate grades based on the average (customize this as needed)
function calculateGrades(average) {
if (average >= 90) {
return "A";
} else if (average >= 80) {
return "B";
} else if (average >= 70) {
return "C";
} else if (average >= 60) {
return "D";
} else {
return "F";
}
}


// Creates a new input box under the "Grades" column
function newInputLine(index) {


// Setup score element and attributes
var score = document.createElement("input"); // input element
score.id = index; // id of input element
score.onkeydown = calculator // Each key triggers event (using function as a value)
score.type = "number"; // Use text type to allow typing multiple characters
score.name = "score"; // name is used to group all "score" elements (array)
score.style.textAlign = "right";
score.style.width = "5em";
// Append the input box under the "Grades" column
var gradesColumn = document.getElementById("grades").parentNode;
gradesColumn.appendChild(score); // add to HTML


// Create and add a blank line after the input box
var br = document.createElement("br"); // line break element
gradesColumn.appendChild(br); // add to HTML


// Set focus on the new input line
score.focus();
}


// Initial creation of the first input line for scores
newInputLine(0);

// Reset button click event handler
document.getElementById("resetButton").addEventListener("click", function() {
    var array = document.getElementsByName('score');
    for (var i = 0; i < array.length; i++) {
        array[i].value = ""; // Clear each input field for scores
    }
    
    // Remove extra input fields for scores
    var gradesColumn = document.getElementById("grades").parentNode;
    while (gradesColumn.childNodes.length > 2) {
        gradesColumn.removeChild(gradesColumn.lastChild);
    }
    
    // Clear all input fields for assignment names except the first one
    var assignmentInputs = document.getElementsByName('assignmentName');
    for (var i = 0; i < assignmentInputs.length; i++) {
        assignmentInputs[i].value = "";
    }
    
    // Remove extra input fields for assignment names except the first one
    var assignmentsColumn = document.getElementById("assignments");
    while (assignmentsColumn.childNodes.length > 2) {
        assignmentsColumn.removeChild(assignmentsColumn.lastChild);
    }
    
    // Reset grade value and average value
    document.getElementById('grades').innerHTML = "N/A";
    document.getElementById('average').innerHTML = "0.0";
    
    calculator({ key: "Enter" }); // Trigger recalculation when reset button is clicked
});


// Creates a new input box under the "Assignment Names" column
function newAssignmentLine(index) {
    // Setup assignment name element and attributes
    var assignmentName = document.createElement("input"); // input element
    assignmentName.id = "assignmentName" + index; // id of input element
    assignmentName.onkeydown = function(event) {
        calculator(event); // Trigger calculator on Enter key press
        if (event.key === "Enter") {
            newAssignmentLine(index + 1); // Create a new input line for assignment names on Enter key press
        }
    };
    assignmentName.type = "text"; // Text input for assignment names
    assignmentName.name = "assignmentName"; // name is used to group all "assignmentName" elements (array)
    assignmentName.style.width = "15em";
    assignmentName.placeholder = "Enter Assignment Name";

    // Append the input box under the "Assignment Names" column
    var assignmentsColumn = document.getElementById("assignments");
    assignmentsColumn.appendChild(assignmentName); // add to HTML

    // Create and add a blank line after the input box
    var br = document.createElement("br"); // line break element
    assignmentsColumn.appendChild(br); // add to HTML

    // Set focus on the new input line for assignment names
    assignmentName.focus();
}

// Initial creation of the first input line for assignment names
newAssignmentLine(0);

</script>
</body>
</html>



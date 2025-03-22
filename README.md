<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            line-height: 1.6;
        }
        h1, h2, h3 {
            color: #2c3e50;
        }
        .container {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        .card {
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
        }
        button:hover {
            background-color: #2980b9;
        }
        .result {
            font-weight: bold;
            font-size: 18px;
            margin-top: 10px;
        }
        .grade-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        .grade-table th, .grade-table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        .grade-table th {
            background-color: #f2f2f2;
        }
        .slide-container {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .slider {
            flex: 1;
        }
        .value-display {
            width: 50px;
            text-align: center;
        }
        .assignments-list {
            margin-top: 10px;
        }
        .assignment {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            border-bottom: 1px solid #eee;
        }
        .delete-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            border-radius: 4px;
            padding: 2px 6px;
            cursor: pointer;
        }
        .delete-btn:hover {
            background-color: #c0392b;
        }
        footer {
            margin-top: 30px;
            text-align: center;
            color: #7f8c8d;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <h1>Grade Calculator</h1>
    <div class="container">
        <!-- Category Weights -->
        <div class="card">
            <h2>Category Weights</h2>
            <div class="grid">
                <div class="form-group">
                    <label for="tests-weight">Tests (%)</label>
                    <div class="slide-container">
                        <input type="range" id="tests-weight" class="slider" min="0" max="100" value="40">
                        <input type="number" id="tests-weight-value" class="value-display" min="0" max="100" value="40">
                    </div>
                </div>
                <div class="form-group">
                    <label for="quizzes-weight">Quizzes (%)</label>
                    <div class="slide-container">
                        <input type="range" id="quizzes-weight" class="slider" min="0" max="100" value="20">
                        <input type="number" id="quizzes-weight-value" class="value-display" min="0" max="100" value="20">
                    </div>
                </div>
                <div class="form-group">
                    <label for="classworks-weight">Classworks (%)</label>
                    <div class="slide-container">
                        <input type="range" id="classworks-weight" class="slider" min="0" max="100" value="20">
                        <input type="number" id="classworks-weight-value" class="value-display" min="0" max="100" value="20">
                    </div>
                </div>
                <div class="form-group">
                    <label for="homeworks-weight">Homeworks (%)</label>
                    <div class="slide-container">
                        <input type="range" id="homeworks-weight" class="slider" min="0" max="100" value="20">
                        <input type="number" id="homeworks-weight-value" class="value-display" min="0" max="100" value="20">
                    </div>
                </div>
            </div>
            <div id="weight-error" style="color: red; display: none;">Total weights must equal 100%</div>
            <button id="save-weights">Save Weights</button>
        </div>
        <!-- Current Grades -->
        <div class="card">
            <h2>Current Grades</h2>
            <div class="grid">
                <div class="form-group">
                    <label for="tests-category">Tests</label>
                    <div id="tests-assignments" class="assignments-list"></div>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <input type="number" id="tests-grade" placeholder="Grade (0-100)" min="0" max="100">
                        <button id="add-test">Add</button>
                    </div>
                </div>
                <div class="form-group">
                    <label for="quizzes-category">Quizzes</label>
                    <div id="quizzes-assignments" class="assignments-list"></div>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <input type="number" id="quizzes-grade" placeholder="Grade (0-100)" min="0" max="100">
                        <button id="add-quiz">Add</button>
                    </div>
                </div>
                <div class="form-group">
                    <label for="classworks-category">Classworks</label>
                    <div id="classworks-assignments" class="assignments-list"></div>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <input type="number" id="classworks-grade" placeholder="Grade (0-100)" min="0" max="100">
                        <button id="add-classwork">Add</button>
                    </div>
                </div>
                <div class="form-group">
                    <label for="homeworks-category">Homeworks</label>
                    <div id="homeworks-assignments" class="assignments-list"></div>
                    <div style="display: flex; gap: 10px; margin-top: 10px;">
                        <input type="number" id="homeworks-grade" placeholder="Grade (0-100)" min="0" max="100">
                        <button id="add-homework">Add</button>
                    </div>
                </div>
            </div>
            <div style="margin-top: 15px;">
                <button id="calculate-current">Calculate Current Grade</button>
                <div id="current-grade" class="result"></div>
            </div>
        </div>
        <!-- New Assignment -->
        <div class="card">
            <h2>Calculate Grade with New Assignment</h2>
            <div class="form-group">
                <label for="new-assignment-category">Category</label>
                <select id="new-assignment-category">
                    <option value="tests">Tests</option>
                    <option value="quizzes">Quizzes</option>
                    <option value="classworks">Classworks</option>
                    <option value="homeworks">Homeworks</option>
                </select>
            </div>
            <div class="form-group">
                <label for="new-assignment-grade">Expected Grade</label>
                <div class="slide-container">
                    <input type="range" id="new-assignment-grade" class="slider" min="0" max="100" value="80">
                    <input type="number" id="new-assignment-grade-value" class="value-display" min="0" max="100" value="80">
                </div>
            </div>
            <button id="calculate-new">Calculate New Grade</button>
            <div id="new-grade" class="result"></div>
        </div>
        <!-- Target Grade -->
        <div class="card">
            <h2>What Grade Do I Need?</h2>
            <div class="form-group">
                <label for="target-grade">Target Overall Grade</label>
                <div class="slide-container">
                    <input type="range" id="target-grade" class="slider" min="0" max="100" value="90">
                    <input type="number" id="target-grade-value" class="value-display" min="0" max="100" value="90">
                </div>
            </div>
            <button id="calculate-needed">Calculate Needed Grades</button>
            <div id="needed-grades" class="result"></div>
            <table id="needed-grades-table" class="grade-table" style="display: none;">
                <thead>
                    <tr>
                        <th>Category</th>
                        <th>Current Average</th>
                        <th>Needed Grade</th>
                    </tr>
                </thead>
                <tbody id="needed-grades-body">
                </tbody>
            </table>
        </div>
    </div>
    <footer>
        &copy; 2025 Grade Calculator | <a href="https://github.com/yourusername/grade-calculator" target="_blank">View on GitHub</a>
    </footer>
    <script>
        // State management
        const state = {
            weights: {
                tests: 40,
                quizzes: 20,
                classworks: 20,
                homeworks: 20
            },
            grades: {
                tests: [],
                quizzes: [],
                classworks: [],
                homeworks: []
            }
        };
        // Try to load data from localStorage
        try {
            const savedState = localStorage.getItem('gradeCalculatorState');
            if (savedState) {
                const parsedState = JSON.parse(savedState);
                state.weights = parsedState.weights;
                state.grades = parsedState.grades;
            }
        } catch (e) {
            console.log('Unable to access localStorage. Using default values.');
        }
        // Get DOM elements
        const weightInputs = {
            tests: document.getElementById('tests-weight'),
            quizzes: document.getElementById('quizzes-weight'),
            classworks: document.getElementById('classworks-weight'),
            homeworks: document.getElementById('homeworks-weight')
        };
        const weightValues = {
            tests: document.getElementById('tests-weight-value'),
            quizzes: document.getElementById('quizzes-weight-value'),
            classworks: document.getElementById('classworks-weight-value'),
            homeworks: document.getElementById('homeworks-weight-value')
        };
        const gradeInputs = {
            tests: document.getElementById('tests-grade'),
            quizzes: document.getElementById('quizzes-grade'),
            classworks: document.getElementById('classworks-grade'),
            homeworks: document.getElementById('homeworks-grade')
        };
        const assignmentLists = {
            tests: document.getElementById('tests-assignments'),
            quizzes: document.getElementById('quizzes-assignments'),
            classworks: document.getElementById('classworks-assignments'),
            homeworks: document.getElementById('homeworks-assignments')
        };
        const newAssignmentCategory = document.getElementById('new-assignment-category');
        const newAssignmentGrade = document.getElementById('new-assignment-grade');
        const newAssignmentGradeValue = document.getElementById('new-assignment-grade-value');
        const targetGrade = document.getElementById('target-grade');
        const targetGradeValue = document.getElementById('target-grade-value');
        // Initialize UI with current state
        function initializeUI() {
            // Set weight inputs
            for (const category in state.weights) {
                weightInputs[category].value = state.weights[category];
                weightValues[category].value = state.weights[category];
            }
            // Render assignments
            for (const category in state.grades) {
                renderAssignments(category);
            }
        }
      // Try to save state to localStorage
        function saveToStorage() {
            try {
                localStorage.setItem('gradeCalculatorState', JSON.stringify(state));
            } catch (e) {
                console.log('Unable to save to localStorage.');
            }
        }
        // Connect weight sliders and number inputs
        for (const category in weightInputs) {
            // Update number input when slider changes
            weightInputs[category].addEventListener('input', function() {
                weightValues[category].value = this.value;
                validateWeights();
            });
            // Update slider when number input changes
            weightValues[category].addEventListener('input', function() {
                weightInputs[category].value = this.value;
                validateWeights();
            });
        }
        // Validate that weights add up to 100%
        function validateWeights() {
            const total = Object.values(weightValues).reduce((sum, input) => sum + parseInt(input.value || 0), 0);
            const errorMsg = document.getElementById('weight-error');           
            if (total !== 100) {
                errorMsg.style.display = 'block';
                return false;
            } else {
                errorMsg.style.display = 'none';
                return true;
            }
        }
        // Save weights button
        document.getElementById('save-weights').addEventListener('click', function() {
            if (validateWeights()) {
                for (const category in weightInputs) {
                    state.weights[category] = parseInt(weightValues[category].value);
                }
                saveToStorage();
                alert('Weights saved successfully!');
            }
        });
        // Add grade for a category
        function addGrade(category) {
            const gradeValue = parseFloat(gradeInputs[category].value);      
            if (isNaN(gradeValue) || gradeValue < 0 || gradeValue > 100) {
                alert('Please enter a valid grade between 0 and 100.');
                return;
            }   
            state.grades[category].push(gradeValue);
            gradeInputs[category].value = '';
            renderAssignments(category);
            saveToStorage();
        }
        // Add event listeners for adding grades
        document.getElementById('add-test').addEventListener('click', function() {
            addGrade('tests');
        });
        document.getElementById('add-quiz').addEventListener('click', function() {
            addGrade('quizzes');
        });
        document.getElementById('add-classwork').addEventListener('click', function() {
            addGrade('classworks');
        });
        document.getElementById('add-homework').addEventListener('click', function() {
            addGrade('homeworks');
        });
        // Render assignments list for a category
        function renderAssignments(category) {
            const listElement = assignmentLists[category];
            listElement.innerHTML = '';
            state.grades[category].forEach((grade, index) => {
                const assignmentDiv = document.createElement('div');
                assignmentDiv.className = 'assignment';
                assignmentDiv.innerHTML = `
                    <span>Assignment ${index + 1}: ${grade.toFixed(1)}%</span>
                    <button class="delete-btn" data-category="${category}" data-index="${index}">×</button>
                `;
                listElement.appendChild(assignmentDiv);
            });
            // Add event listeners for delete buttons
            const deleteButtons = listElement.querySelectorAll('.delete-btn');
            deleteButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const category = this.getAttribute('data-category');
                    const index = parseInt(this.getAttribute('data-index'));
                    state.grades[category].splice(index, 1);
                    renderAssignments(category);
                    saveToStorage();
                });
            });
        }
        // Calculate current grade
        function calculateCurrentGrade() {
            let totalWeight = 0;
            let weightedSum = 0;
            for (const category in state.weights) {
                const grades = state.grades[category];
                if (grades.length > 0) {
                    const average = grades.reduce((sum, grade) => sum + grade, 0) / grades.length;
                    weightedSum += (average * state.weights[category]);
                    totalWeight += state.weights[category];
                }
            }
            if (totalWeight === 0) {
                return 'No grades entered yet';
            }
            // Normalize by the total weight of categories that have grades
            return (weightedSum / totalWeight).toFixed(2) + '%';
        }
        // Calculate current grade button
        document.getElementById('calculate-current').addEventListener('click', function() {
            const currentGrade = calculateCurrentGrade();
            document.getElementById('current-grade').textContent = `Current Grade: ${currentGrade}`;
        });
        // Connect new assignment grade slider and input
        newAssignmentGrade.addEventListener('input', function() {
            newAssignmentGradeValue.value = this.value;
        });
        newAssignmentGradeValue.addEventListener('input', function() {
            newAssignmentGrade.value = this.value;
        });
        // Calculate grade with new assignment
        document.getElementById('calculate-new').addEventListener('click', function() {
            const category = newAssignmentCategory.value;
            const grade = parseFloat(newAssignmentGradeValue.value);   
            if (isNaN(grade) || grade < 0 || grade > 100) {
                alert('Please enter a valid grade between 0 and 100.');
                return;
            }
            // Create a deep copy of the state
            const tempState = JSON.parse(JSON.stringify(state));
            // Add the new grade to the temporary state
            tempState.grades[category].push(grade);
            // Calculate with the temporary state
            let totalWeight = 0;
            let weightedSum = 0;
            for (const cat in tempState.weights) {
                const grades = tempState.grades[cat];
                if (grades.length > 0) {
                    const average = grades.reduce((sum, g) => sum + g, 0) / grades.length;
                    weightedSum += (average * tempState.weights[cat]);
                    totalWeight += tempState.weights[cat];
                }
            }
            let newGrade;
            if (totalWeight === 0) {
                newGrade = 'Cannot calculate grade';
            } else {
                newGrade = (weightedSum / totalWeight).toFixed(2) + '%';
            }
            document.getElementById('new-grade').textContent = `New Grade: ${newGrade}`;
        });
        // Connect target grade slider and input
        targetGrade.addEventListener('input', function() {
            targetGradeValue.value = this.value;
        });
        targetGradeValue.addEventListener('input', function() {
            targetGrade.value = this.value;
        });
        // Calculate needed grades
        document.getElementById('calculate-needed').addEventListener('click', function() {
            const target = parseFloat(targetGradeValue.value);
            if (isNaN(target) || target < 0 || target > 100) {
                alert('Please enter a valid target grade between 0 and 100.');
                return;
            }
            // Get current category averages and weights
            const categoryAverages = {};
            let totalWeightCovered = 0;
            for (const category in state.weights) {
                const grades = state.grades[category];
                if (grades.length > 0) {
                    categoryAverages[category] = grades.reduce((sum, grade) => sum + grade, 0) / grades.length;
                    totalWeightCovered += state.weights[category];
                } else {
                    categoryAverages[category] = null;
                }
            }
            // Calculate needed grades for each category
            const neededGrades = {};
            let canAchieveTarget = true;
            for (const category in state.weights) {
                if (categoryAverages[category] === null) {
                    // Calculate what grade is needed in this category
                    let currentWeightedSum = 0;
                    for (const cat in categoryAverages) {
                        if (categoryAverages[cat] !== null && cat !== category) {
                            currentWeightedSum += categoryAverages[cat] * state.weights[cat];
                        }
                    }
                    const remainingWeight = state.weights[category];
                    const needed = (target * 100 - currentWeightedSum) / remainingWeight;
                    if (needed < 0 || needed > 100) {
                        canAchieveTarget = false;
                    }
                    neededGrades[category] = Math.min(Math.max(needed, 0), 100).toFixed(2);
                } else {
                    neededGrades[category] = categoryAverages[category].toFixed(2);
                }
            }
            // Display the results
            const neededGradesElement = document.getElementById('needed-grades');
            const tableElement = document.getElementById('needed-grades-table');
            const tableBody = document.getElementById('needed-grades-body');
            if (!canAchieveTarget) {
                neededGradesElement.textContent = `To achieve ${target}%, you would need grades outside the possible range (0-100%).`;
                tableElement.style.display = 'none';
            } else {
                neededGradesElement.textContent = `To achieve ${target}%, you need:`;
                tableBody.innerHTML = '';
                for (const category in neededGrades) {
                    const row = document.createElement('tr');
                    const categoryCell = document.createElement('td');
                    categoryCell.textContent = category.charAt(0).toUpperCase() + category.slice(1);
                    const currentCell = document.createElement('td');
                    currentCell.textContent = categoryAverages[category] !== null ? categoryAverages[category].toFixed(2) + '%' : 'No grades';
                    const neededCell = document.createElement('td');
                    neededCell.textContent = neededGrades[category] + '%';
                    row.appendChild(categoryCell);
                    row.appendChild(currentCell);
                    row.appendChild(neededCell);
                    tableBody.appendChild(row);
                }
                tableElement.style.display = 'table';
            }
        });
        // Initialize the app
        initializeUI();
    </script>
</body>
</html>

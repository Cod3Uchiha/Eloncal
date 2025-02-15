## HTML file: index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Elon Calculator</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Elon Calculator</h1>
  <form>
    <input type="text" id="display" placeholder="0">
    <button type="button" class="operator" data-value="+">+</button>
    <button type="button" class="operator" data-value="-">-</button>
    <button type="button" class="operator" data-value="*">*</button>
    <button type="button" class="operator" data-value="/">/</button>
    <button type="button" class="number" data-value="7">7</button>
    <button type="button" class="number" data-value="8">8</button>
    <button type="button" class="number" data-value="9">9</button>
    <button type="button" class="number" data-value="4">4</button>
    <button type="button" class="number" data-value="5">5</button>
    <button type="button" class="number" data-value="6">6</button>
    <button type="button" class="number" data-value="1">1</button>
    <button type="button" class="number" data-value="2">2</button>
    <button type="button" class="number" data-value="3">3</button>
    <button type="button" class="decimal" data-value=".">.</button>
    <button type="button" class="clear" data-value="clear">C</button>
    <button type="button" class="equals" data-value="=">=</button>
  </form>
  <script src="script.js"></script>
</body>
</html>
```

## CSS file: style.css
```css
body {
  background-color: #f5f5f5;
  font-family: Arial, sans-serif;
}

h1 {
  margin-top: 0;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

#display {
  width: 250px;
  height: 50px;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  text-align: right;
  font-size: 24px;
}

.operator,
.number,
.decimal,
.clear,
.equals {
  width: 50px;
  height: 50px;
  margin: 5px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.operator {
  background-color: #f0f0f0;
}

.number,
.decimal {
  background-color: #ffffff;
}

.clear {
  background-color: #ff0000;
}

.equals {
  background-color: #008000;
}
```

## JavaScript file: script.js
```js
const display = document.getElementById('display');
const buttons = document.querySelectorAll('button');
let firstOperand = null;
let secondOperand = null;
let operator = null;

buttons.forEach((button) => {
  button.addEventListener('click', () => {
    const value = button.getAttribute('data-value');

    if (value === 'clear') {
      firstOperand = null;
      secondOperand = null;
      operator = null;
      display.value = '0';
    } else if (value === '.') {
      if (display.value.includes('.')) {
        return;
      }
      display.value += value;
    } else if (value === '+' || value === '-' || value === '*' || value === '/') {
      firstOperand = parseFloat(display.value);
      operator = value;
      display.value = '';
    } else if (value === '=') {
      secondOperand = parseFloat(display.value);
      let result = null;

      switch (operator) {
        case '+':
          result = firstOperand + secondOperand;
          break;
        case '-':
          result = firstOperand - secondOperand;
          break;
        case '*':
          result = firstOperand * secondOperand;
          break;
        case '/':
          if (secondOperand === 0) {
            alert('Cannot divide by zero');
            return;
          }
          result = firstOperand / secondOperand;
          break;
      }

      display.value = result;
      firstOperand = result;
      secondOperand = null;
      operator = null;
    } else {
      display.value += value;
    }
  });
});
```

## Documentation

### HTML file

The HTML file defines the structure of the calculator. It contains a form with a text input for the display, and a series of buttons for the operators and numbers.

### CSS file

The CSS file defines the style of the calculator. It sets the background color, font family, and layout of the elements.

### JavaScript file

The JavaScript file defines the behavior of the calculator. It handles the user input and updates the display accordingly.

### Implementation details

The calculator is implemented using event listeners on the buttons. When a button is clicked, the event listener retrieves the value of the button and performs the appropriate action.

The calculator keeps track of the first operand, second operand, and operator using three variables. When a number button is clicked, the value is appended to the display. When an operator button is clicked, the first operand is set to the current value of the display, the operator is set to the value of the button, and the display is cleared. When the equals button is clicked, the second operand is set to the current value of the display, the result is calculated, and the display is updated with the result.

The calculator also includes a clear button that resets all of the variables and clears the display.
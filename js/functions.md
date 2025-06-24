# Functions

A function in JavaScript is a block of code designed to perform a particular task. It executes when "something" invokes or calls it. Functions are reusable, can be passed data to operate on (i.e., parameters), and can optionally return data (output).

By the way: **A parameter is the variable listed inside the parentheses in the function definition.** **An argument is the actual value that is sent to the function when it is called**.

🌈The more you know🌈

### Function Declarations

This is one of the ways to define a function. You start with the `function` keyword, followed by the name of the function, parentheses that may include parameters, and a block of code enclosed in curly braces that defines the function body.

### Function Expressions

A function expression stores a function inside a variable. This can be an anonymous function (a function without a name) or a named function. Function expressions are not hoisted, meaning they cannot be called before they are defined in the code.

Choosing between function declarations vs function expressions, again, has to do with scope!

### ES5 vs ES6+ Functions

ECMAScript 6 (also known as ES6 and ECMAScript 2015) introduced several new features for writing cleaner and more concise functions:

- **ES5 Functions**: Traditional functions, either as declarations or expressions, without the enhancements found in ES6.
- **ES6+ Functions**:
    - **Arrow Functions**: They allow a short syntax. They are always anonymous.
    - **Default Parameters**: Parameters can now have default values if not provided.
    - **Rest Parameters**: Functions can accept a variable number of arguments without specifying them explicitly in the function definition.

[https://playground.wbscod.in/static/javascript-basics/7](https://playground.wbscod.in/static/javascript-basics/7)

```javascript
// Function declaration
function greet(name) {
  return 'Hello ' + name + '!';
}

greet('Sarah'); // Wait... nothing happened?

// No! It did. The thing is that our function is returning a value, we need to explicitly do something with it

console.log(greet('Sarah'));

/* 
In the previous line, greet('Sarah') is an expression that eventually evalutes to the string
Hello Sarah! which we just output
*/

const greetingResult = greet('Anoj');
console.info(greetingResult);
/* 
We can also simply store the result of a function (as long as it returns something) into a
variable for later use 
*/

// Function expression
const square = function (number) {
  return number * number;
};

const result = square(4);
console.log(result);

// Arrow function
const add = (a, b) => a + b;
console.log(add(50, 1000));

// Default parameters
function multiply(a, b = 2) {
  return a * b;
}

console.log(multiply(10)); // Should be 20 since b defaults to 2
console.log(multiply(10, 10)); // Should be 100 since b is provided

// Rest parameters or ...ain't nobody got time for that
function sum(...numbers) {
  return numbers.reduce((acc, number) => acc + parseInt(number), 0);
}

console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
```

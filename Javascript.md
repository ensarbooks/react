# Chapter 1: Introduction to JavaScript and Variables  
JavaScript is a versatile, high-level scripting language that executes in web browsers, enabling interactive web pages. It was created in 1995 and has since evolved into a powerful language used on both client and server sides of web development JavaScript’s integration with HTML and CSS makes it a core technology for the web. In this chapter, we’ll set up a development environment and write a simple “Hello, World” to ensure everything is working.

## Setting Up and “Hello, World”  
- **Environment**: All you need is a web browser and a text editor (or an IDE like VS Code). Create an HTML file and include a `<script>` tag, or use the browser console for quick experiments.  
- **Hello World Example**:  
  ```html  
  <!DOCTYPE html>  
  <html lang="en">  
  <head>  
    <meta charset="UTF-8" />  
    <title>Hello JS</title>  
  </head>  
  <body>  
    <h1 id="greet">Hello</h1>  
    <script>  
      document.getElementById('greet').textContent += ", World!";  
      console.log("Hello, World!"); // Logs greeting to console  
    </script>  
  </body>  
  </html>  
  ```  
  This script finds an element by ID and modifies its text content to display "Hello, World!" in the page, and also logs a message to the browser’s console.

## Variables in JavaScript  
JavaScript is **dynamically typed**, meaning you don’t declare types for variables – the type is determined at runtime based on the value You declare variables using `var`, `let`, or `const` keywords.  

- **`var`** – the old way to declare a variable. `var` is **function-scoped** (or global if declared outside a function). It can be re-assigned and even re-declared in the same scope (which can be confusing).  
- **`let`** – introduced in ES6 (2015) for block-scoped variables. `let` variables can be updated (re-assigned) but not re-declared in the same block.  
- **`const`** – also block-scoped, used for constants. A `const` must be initialized at declaration and cannot be re-assigned. (However, if the value is an object or array, its *contents* can still change.)  

**Example – Using var, let, and const:**  
```js  
function varVsLet() {  
  if (true) {  
    var x = 1;  
    let y = 2;  
    const z = 3;  
  }  
  console.log(x); // 1 (var is function-scoped, so accessible here)  
  console.log(typeof y); // "undefined" (y is block-scoped, not accessible here)  
  // console.log(z); // Uncaught ReferenceError: z is not defined (z is block-scoped)  
}  
varVsLet();  

// Re-declaration and re-assignment  
var a = 5;  
var a = 6;   // re-declaration allowed with var  
let b = 7;  
// let b = 8; // SyntaxError: Identifier 'b' has already been declared  
b = 8;       // re-assignment is fine  
const c = 9;  
// c = 10;    // TypeError: Assignment to constant variable.  
```  

**Key Takeaways:** Variables defined with `let` and `const` have block scope (they exist only within the nearest `{ ... }` block), which helps avoid bugs. `var` is hoisted to the top of its function scope, which can lead to unintended behavior. Advanced JavaScript code today generally prefers `let` and `const` over `var` for clearer scoping.

## Dynamic Typing and Types of Variables  
Because of dynamic typing, a variable can hold any type of value and that type can change at runtime. For example:  
```js  
let data = "Hello";      // data is a string  
data = 42;              // now data is a number  
data = true;           // now data is a boolean  
```  
This flexibility is powerful but means you must be careful with type conversions and comparisons. We will explore JavaScript data types in the next chapter.

# Chapter 2: Data Types and Their Methods – Part 1  
JavaScript has a set of **primitive data types** and **objects**. The seven primitive types are: **Number**, **String**, **Boolean**, **Null**, **Undefined**, **Symbol**, and **BigInt** Everything else (like arrays, functions, objects) is of type Object. Primitives are immutable (their value cannot be changed), whereas objects are mutable.  

## Number Type and Methods  
The **Number** type in JavaScript is used for all numeric values (integers and floating-point). JavaScript numbers follow the IEEE-754 standard (which means they are double-precision floating-point and can handle very large or very small values, but also means things like `0.1 + 0.2` may not equal exactly `0.3` due to binary floating-point precision).  

- **Basic operations**: addition `+`, subtraction `-`, multiplication `*`, division `/`, exponentiation `**`, and modulo `%`.  
- **Special numeric values**: `NaN` (Not-a-Number, e.g., result of invalid math operation like `parseInt("abc")`), `Infinity` and `-Infinity` (overflow values, e.g., `1/0`).  

**Example – Number usage:**  
```js  
let n = 42;  
n = n + 1;            // 43  
console.log(Math.pow(n, 2));  // 1849, using Math library for power  
console.log(0.1 + 0.2);      // 0.30000000000000004 (floating-point precision)  
console.log(isNaN("abc"/2)); // true, "abc"/2 results in NaN  
```  

**Number methods & properties:**  
- `Number.isNaN(x)` – checks if value is NaN.  
- `Number.isInteger(x)` – checks if x is an integer.  
- `toFixed(decimalPlaces)` – format a number with a fixed number of decimals as a string.  
- `Math` object – contains utilities like `Math.random()` (random 0-1), `Math.round()`, `Math.floor()`, `Math.ceil()`, trigonometric functions, etc.

**BigInt** is a newer primitive type for integers of arbitrary length (beyond the safe range of Number). You can create a BigInt by appending `n` to an integer literal or by using `BigInt()` function:  
```js  
const big = 12345678901234567890123456789n;  
console.log(big + 1n); // Works with BigInts  
// console.log(big + 1); // TypeError: cannot mix BigInt and other types  
```  
Use BigInt when you need to safely handle extremely large integers (like for cryptography or precise financial calculations).

## String Type and Methods  
Strings in JavaScript are sequences of characters. They are immutable – operations on strings always produce new strings and don’t modify the original. You can use single quotes `'...'`, double quotes `"..."`, or backticks `` `...` `` (for template literals) to define strings.

**Basic string operations:**  
- **Concatenation**: Using `+` or template literals.  
- **Length**: `str.length` property gives the number of characters.  
- **Access**: You can access characters by index `str[index]` (strings behave like arrays of characters, but they are read-only).

**Example – String basics:**  
```js  
let s1 = "Hello";  
let s2 = 'World';  
let message = s1 + ", " + s2 + "!";  
console.log(message);              // "Hello, World!"  
console.log(message.length);       // 13  
console.log(message[1]);           // "e"  
// Strings are immutable: methods return new strings  
console.log(s1.toUpperCase());     // "HELLO" (s1 remains "Hello")  
```  

**Useful string methods:**  
- `toUpperCase()` / `toLowerCase()` – return an uppercase/lowercase version.  
- `indexOf(substring)` – returns index of first occurrence of substring (or -1 if not found).  
- `includes(substring)` – returns true if substring is found.  
- `slice(start, end)` – extracts a substring from index `start` up to but not including `end`.  
- `substring(start, end)` – similar to slice, but cannot accept negative indices.  
- `trim()` – removes whitespace from both ends.  
- `replace(search, replacement)` – replaces occurrences of `search` (string or regex) with the replacement text.  

**Example – Using string methods:**  
```js  
let original = "  Hello JavaScript!  ";  
console.log(original.trim());            // "Hello JavaScript!"  
console.log(original.includes("Java"));  // true  
console.log(original.indexOf("Java"));   // 7 (position where "Java" starts)  
console.log(original.slice(2, 7));       // "Hello" (extracts characters at indices 2-6)  
console.log(original.replace("JavaScript", "JS")); // "  Hello JS!  "  
```  

**Template Literals:** Strings enclosed in backticks (`` ` ``) allow interpolation and multi-line strings. You can embed expressions with `${...}`.  
```js  
let name = "Alice";  
let greeting = `Hello, ${name}!`;  
console.log(greeting); // "Hello, Alice!"  
```  

Template literals also respect line breaks and spacing, making it easier to create multi-line text.

## Boolean Type  
The Boolean type has two values: `true` and `false`. It is commonly the result of comparisons or logical operations.  

- JavaScript has *truthy* and *falsy* values. Falsy values (which coerce to false in Boolean context) include: `false`, `0`, `""` (empty string), `null`, `undefined`, and `NaN`. Everything else is truthy (even `"0"` or `[]` or `{}` are truthy).  
- Booleans are often produced by comparison operators (==, ===, >, <, etc., which we will cover in Chapter 4) or logical operators.  

**Examples:**  
```js  
let isLoggedIn = false;  
console.log(Boolean(0));       // false (0 is falsy)  
console.log(Boolean("Hello")); // true (non-empty string is truthy)  
console.log(5 > 3);            // true (result of comparison is boolean)  
```  

Booleans have no special methods (they are primitives), but you can get a Boolean value using the `Boolean()` function or the `!!` double-not trick to convert a value to true/false.

## Null and Undefined  
These are two distinct primitive types that both represent an “empty” value:  

- **`undefined`**: automatically assigned to variables that have been declared but not initialized. It also is the default return value of functions that don’t explicitly return something.  
- **`null`**: a value that explicitly signifies “no value” or “empty”. Developers assign `null` to a variable to indicate it has no value.  

It’s a quirk of JavaScript that `typeof null` returns `"object"`– this is a historical bug in the language, but `null` is **not** actually an object; it’s a primitive that stands for “no object”. On the other hand, `typeof undefined` returns `"undefined"`. Despite both meaning “no value”, they are not the same:  
```js  
console.log(null == undefined);  // true (they are equal in value, loosely)  
console.log(null === undefined); // false (not equal in type)  
console.log(typeof null);        // "object" (JavaScript quirk/bug) 
```  
In summary, use `undefined` for unassigned things (often the system gives you undefined), and use `null` when you purposefully want to indicate “empty”. They are **equal in value** but **different in type** When checking for missing values, a common pattern is to check `value == null` which is true for *either* null or undefined. We will revisit nullish values with the “nullish coalescing” operator in a later chapter.

## Symbol Type  
A **Symbol** is a unique and immutable primitive introduced in ES6. It’s often used for unique property keys that won’t collide with other keys. Each time you call `Symbol()`, you get a new unique symbol:  
```js  
let sym1 = Symbol("id");  
let sym2 = Symbol("id");  
console.log(sym1 == sym2); // false, every Symbol is unique  
```  
Symbols are advanced and rarely needed for beginners, but in advanced code they enable special behaviors (for example, defining custom behavior for object serialization, or hidden object properties, by using well-known symbols like `Symbol.iterator`).

---

**Hands-On Exercise:** *Identify Data Types* – Try writing a function that takes any value and returns a message describing its type. It can use `typeof` for most cases, but also distinguish between `null` and objects properly. For example, it should return “null” for `null`, “array” for arrays (since `typeof []` is "object"), and so on. This will give you practice with primitives vs objects and using `typeof` operator quirks. (Hint: use `Array.isArray()` to detect arrays, and a special case for `null` since `typeof null` is the bug "object".)

# Chapter 3: Data Types and Their Methods – Part 2  
Continuing from the previous chapter, we’ll cover **objects** in general, **arrays**, and more on using data type methods. These are crucial for structuring and managing data in JavaScript.

## Objects  
Objects in JavaScript are collections of key-value pairs (properties). Almost everything that is not a primitive is an Object (including arrays and functions). You can think of an object as a simple dictionary of values, or as an entity with properties and methods.  

**Creating objects:**  
- **Object literal**:  
  ```js  
  let person = {  
    name: "Bob",  
    age: 30,  
    greet: function() {  
      console.log("Hello, I'm " + this.name);  
    }  
  };  
  ```  
  Here `person` has properties `name` and `age`, and a method `greet`. You can use the shorthand syntax for methods in ES6:  
  ```js  
  let person2 = {  
    name: "Alice",  
    age: 25,  
    greet() { console.log(`Hi, I'm ${this.name}`); }  // concise method syntax  
  };  
  ```  
- **Using `new Object()`** – not commonly used; object literal is preferred for simplicity.

**Accessing and modifying properties:**  
- Dot notation: `person.name`  
- Bracket notation: `person["name"]` (useful if property name is in a variable or not a valid identifier)  
```js  
console.log(person.name);         // "Bob"  
console.log(person["age"]);       // 30  
person.job = "Developer";         // add new property  
person["hobby"] = "painting";     // add another property  
delete person.age;                // remove a property  
```  

**Iterating over object properties:**  
- Use a `for...in` loop (we will discuss loops soon) or `Object.keys(person)` to get an array of keys.  

**Common operations:**  
- `Object.keys(obj)` – returns an array of property names.  
- `Object.values(obj)` – array of property values.  
- `Object.entries(obj)` – array of `[key, value]` pairs (useful for looping).  
- Objects are **reference types**, meaning if you assign `let obj2 = obj1`, both variables refer to the *same* object (they are not copied). We explore the implications of this in Chapter 11 on scope.  

**Methods in objects:** As seen, objects can contain functions (methods). Inside an object’s method, `this` refers to the object itself (when properly invoked as a method). For example, in `person.greet()`, inside greet, `this.name` refers to `person.name`.  

We will deep dive into `this` and object-oriented patterns later (Classes in Chapter 26-27). For now, remember that objects group related data and functionality. They are the backbone of structuring more complex data in JavaScript.

## Arrays  
Arrays are a special type of object in JavaScript used to store ordered collections of values. Arrays are dynamic (can grow/shrink) and can contain elements of different types (even different types in the same array, though that’s usually not advisable for clarity).

**Creating arrays:**  
- Array literal: `let arr = [1, 2, 3];`  
- Using constructor: `let arr2 = new Array(5); // creates an array of length 5 (all elements undefined)`

**Accessing elements:** Use zero-based indices. `arr[0]` is the first element.  
**Length:** `arr.length` gives the number of elements (it’s dynamic: add or remove elements and length updates).

**Common array methods:**  
- **Adding/removing at end**: `push(item)` adds to end, `pop()` removes last item.  
- **Adding/removing at start**: `unshift(item)` adds to front, `shift()` removes first item.  
- **Slice**: `arr.slice(start, end)` returns a new array copy of a subrange (does not modify original).  
- **Splice**: `arr.splice(start, deleteCount, ...items)` can insert/remove elements at arbitrary positions (modifies the array).  
- **indexOf(item)` / `includes(item)`**: find if an element exists.  
- **join(separator)`**: join elements into a string.  
- **concat(array2)`**: returns a new array by concatenating another array (does not modify original).  

**Example – Array methods:**  
```js  
let fruits = ["apple", "banana", "cherry"];  
fruits.push("date");             // ["apple", "banana", "cherry", "date"]  
let last = fruits.pop();         // removes "date", last = "date"  
fruits.unshift("avocado");       // ["avocado", "apple", "banana", "cherry"]  
let first = fruits.shift();      // removes "avocado", first = "avocado"  
console.log(fruits);             // ["apple", "banana", "cherry"]  
console.log(fruits.indexOf("banana")); // 1  
console.log(fruits.includes("grape")); // false  
```  

**Iterating arrays:** We typically use loops or array methods (next chapter covers loop options in detail). For example:  
```js  
for (let i = 0; i < fruits.length; i++) {  
  console.log(fruits[i]);  
}  
```  
Or using the array method `forEach`:  
```js  
fruits.forEach(fruit => console.log(fruit));  
```  

Arrays, being objects, are passed by reference. If you assign one array to another or pass it to a function, modifications will affect the original. To copy an array, use `slice()` or ES6 spread (`let copy = [...fruits];`). We will see more about spread syntax in Chapter 22.

## Type Conversion and Utility Methods  
JavaScript often converts between types implicitly (type coercion), but you can also explicitly convert:  
- `String(value)` – convert to string. (Or `value.toString()` if value is not null/undefined)  
- `Number(str)` – convert string to number (or `parseInt`, `parseFloat` for partial strings).  
- `Boolean(value)` – get the Boolean equivalent (true/false).  
- `JSON.stringify(obj)` – convert an object/array to a JSON string (useful for logging or storage).  
- `JSON.parse(jsonString)` – parse a JSON string back into an object/array.

**Example – Conversions:**  
```js  
let num = Number("123");        // 123 (number)  
let str = String(123);          // "123" (string)  
let bool = Boolean("hello");    // true  
console.log(JSON.stringify({x:10, y:20})); // "{"x":10,"y":20}"  
```  
Be mindful of coercion in comparisons (the `==` vs `===` difference discussed in next chapter). It’s usually best to use strict equality (`===`) to avoid unexpected type conversions.

**Challenge Exercise:** Create an object representing a simple product in an online store (with properties like name, price, quantity). Then write a function that takes such an object and returns the total value (price * quantity). Try adding a method to the object itself that calculates this. This exercise practices object property access and basic arithmetic with different types (numbers in object properties). Test it with different values.

# Chapter 4: Operators in JS  
JavaScript provides a variety of **operators** to act on data: arithmetic, assignment, comparison, logical, bitwise, and more. Understanding operators is fundamental for performing calculations and making decisions in code.

## Arithmetic and Assignment Operators  
- **Arithmetic**: `+`, `-`, `*`, `/`, `%` (remainder), `**` (exponentiation). They work as you’d expect from math.  
  - Note: `+` is also used for string concatenation. If either operand is a string, `+` will concatenate instead of add numbers. (E.g., `"5" + 2` results in `"52"` not `7`.)  
- **Unary operators**: `+` (unary plus, which tries to convert a value to number), `-` (unary negation), `++` (increment by 1), `--` (decrement by 1).  
  ```js  
  let x = 5;  
  x++; // x becomes 6 (post-increment returns old value)  
  ++x; // x becomes 7 (pre-increment increments then returns new value)  
  ```  
- **Assignment**: `=` assigns a value. There are compound assignments like `+=`, `-=`, `*=`, etc., which perform an operation and assign the result.  
  ```js  
  let a = 10;  
  a += 5; // equivalent to a = a + 5 (so a is 15)  
  a *= 2; // a = a * 2 (now a is 30)  
  ```  
- **Order of execution**: Multiplication/division happen before addition/subtraction by default. Use parentheses to ensure the desired order of operations.

## Comparison Operators  
Comparison operators evaluate two values and produce a Boolean result:  
- **Equal (`==`)** – compares values for equality with type coercion. E.g., `5 == "5"` is `true` (the string is coerced to number 5).  
- **Not Equal (`!=`)** – inequality with type coercion.  
- **Strict Equal (`===`)** – compares both value *and* type (no coercion). E.g., `5 === "5"` is `false` (types differ). This is generally recommended for clarity and avoiding surprises.  
- **Strict Not Equal (`!==`)** – opposite of `===`.  
- **Greater than (`>`)**, **Greater or Equal (`>=`)**, **Less than (`<`)**, **Less or Equal (`<=`)** – numeric comparisons (if operands are not numbers, they get converted, which can lead to complex rules – e.g., comparing strings lexicographically).  

**Example – Comparison:**  
```js  
console.log(5 == "5");    // true  (values are equal after type coercion)  
console.log(5 === "5");   // false (different types, no coercion with ===)  
console.log(0 == false);  // true  (0 is falsy, == treats false as 0)  
console.log(0 === false); // false (different types)  
console.log("apple" < "banana"); // true (string comparison lexicographically)  
```  
As a rule of thumb, use strict equality `===` and strict inequality `!==` to avoid unintended type conversions

## Logical Operators  
Logical operators work with Boolean values (they can also work with truthy/falsy values in JavaScript):  
- **AND (`&&`)** – returns true if both operands are true (truthy).  
- **OR (`||`)** – returns true if at least one operand is true (truthy).  
- **NOT (`!`)** – unary operator that negates a boolean value (`!true` is false).  

These operators also have short-circuit behavior:  
- `A && B` will evaluate `B` only if `A` is truthy (because if `A` is false, the whole expression is false without needing to check B).  
- `A || B` will evaluate `B` only if `A` is falsy (if `A` is true, the whole expression is true and B is ignored).  

Interestingly, in JavaScript, `&&` and `||` do not necessarily return a boolean – they return one of the operands. For example, `result = value1 || value2` will result in `value1` if it’s truthy, otherwise `value2`. This is often used for default values (before the nullish coalescing operator `??` existed). Similarly, `value1 && value2` returns `value2` if `value1` is truthy (and returns `value1` if it’s falsy).  

**Example – Logical ops:**  
```js  
let n = 5;  
if (n > 0 && n < 10) {  
  console.log("n is between 1 and 9");  
}  

console.log("" || "default");   // "default" ("" is falsy, so || returns second operand)  
console.log("hello" && 123);    // 123 (first is truthy, so && returns second)  
console.log(null || undefined || "ok"); // "ok" (both null and undefined are falsy, so returns "ok")  
```  

## Other Operators  
- **Ternary operator (conditional)**: `condition ? valueIfTrue : valueIfFalse`. This is a one-liner replacement for a simple if-else assignment.  
  ```js  
  let age = 20;  
  let status = age >= 18 ? "adult" : "minor";  
  console.log(status); // "adult"  
  ```  
- **Comma operator**: `,` – allows multiple expressions in places like a for loop initialization or a single line (rarely used). E.g., `let a = (1, 2);` will result in `a = 2` (the last expression’s value). Use sparingly or avoid for clarity.  
- **typeof**: an operator that returns a string indicating the type of a value. E.g., `typeof 123` is `"number"`, `typeof []` is `"object"`, `typeof undefined` is `"undefined"`. (Note: as mentioned, `typeof null` returns `"object"` by quirk.) 
- **instanceof**: checks if an object is an instance of a constructor or class. E.g., `arr instanceof Array` returns true if `arr` was created by the Array constructor (i.e., is an array).  
- **Spread (`...`) and Rest (`...`)**: While not “operators” in the traditional sense (they’re more syntax features), they use the `...` syntax to expand iterables or collect rest arguments. We will cover these in Chapter 22 (ES6 features).

## Bitwise Operators (Advanced)  
JavaScript supports bitwise operators (`&`, `|`, `^` for XOR, `~` for NOT, `<<` left shift, `>>` right shift, `>>>` unsigned right shift). These treat operands as 32-bit integers and operate on their binary representation. They are used rarely in everyday JS, mostly in specialized scenarios (like cryptography, graphics, low-level algorithms) because JS Number is not an integer type but can represent 32-bit ints for these operations. If you need to use bitwise operations, be mindful of the 32-bit conversion (for example, `~x` can be used as a quick hack for `-x-1`, or `x | 0` to truncate a number to 32-bit integer).

---

**Try it Out:** Use the console to experiment with some tricky cases:
- Predict the result of `'5' + 3` vs `'5' - 3`. Check what `typeof ('5' + 3)` is vs `typeof ('5' - 3)`. This will show how `+` concatenates when one operand is a string, but `-` forces numeric conversion.  
- Try some comparisons: e.g., `null == undefined` (true), `null < 1` (true, because null becomes 0 in comparison), `[] == 0` (true, array becomes empty string `""` then number 0), and `[] === 0` (false). These strange results reinforce why using strict equality is important to avoid confusion.  

# Chapter 5: Control Statements (if and switch)  
Control statements allow your code to make decisions and execute different paths based on conditions. The primary decision-making structures in JS are `if...else if...else` chains and the `switch` statement.

## if, else if, else  
The **if statement** executes a block of code if a condition is truthy. Optionally, you can add an **else** block to execute if the condition was falsy. You can also chain multiple conditions with **else if**. 

**Syntax:**  
```js  
if (condition1) {  
  // code if condition1 is truthy  
} else if (condition2) {  
  // code if condition1 was falsy and condition2 is truthy  
} else {  
  // code if all above conditions were falsy  
}  
```  

The conditions are expressions that evaluate to a boolean (or truthy/falsy value). Common conditions use comparison operators (like `===`, `<`, etc.). Make sure to use `===` for comparisons unless you specifically intend type coercion.

**Example – if/else:**  
```js  
let score = 85;  
if (score >= 90) {  
  console.log("Grade: A");  
} else if (score >= 80) {  
  console.log("Grade: B");  
} else if (score >= 70) {  
  console.log("Grade: C");  
} else {  
  console.log("Grade: F");  
}  
```  
In this example, only one of the blocks will execute depending on the score. Conditions are checked top-down; once one is true, the rest are skipped.

**Truthy/Falsy in conditions:** As mentioned, if statements consider a value truthy or falsy. For instance, `if ("") { ... }` will not execute because `""` is falsy, whereas `if ("hello") { ... }` will execute. Be cautious: values like 0, `null`, `undefined`, `NaN`, or `""` empty string will be treated as false in conditions. Sometimes you explicitly want to check for a condition (like `if (myArray.length === 0)` rather than just `if (myArray.length)` which would also handle the 0 as falsy).

## switch  
The **switch statement** is useful when you have a variable or expression that you want to compare against many possible values. It can be clearer than a long chain of else-if for certain scenarios (especially discrete values).

**Syntax:**  
```js  
switch (expression) {  
  case value1:  
    // code to execute if expression === value1  
    break;  
  case value2:  
    // code if expression === value2  
    break;  
  default:  
    // code if no case matched  
}  
```  
Important details:  
- The `break` statements are crucial. Without `break`, execution falls through to the next case, which is rarely what you want (though fall-through can be used intentionally in some cases).  
- The `default` case is optional, and it runs if none of the above cases match.  
- The comparisons use strict equality (`===`) under the hood. If the expression matches a case value (with `===`), that case executes.

**Example – switch:**  
```js  
let color = "blue";  
switch (color) {  
  case "red":  
    console.log("Stop");  
    break;  
  case "green":  
    console.log("Go");  
    break;  
  case "yellow":  
    console.log("Caution");  
    break;  
  default:  
    console.log("Unknown color");  
}  
// Output for color "blue" would be "Unknown color" (default case)  
```  

Another example where switch is handy is determining actions based on a number or enum-like value:  
```js  
let day = new Date().getDay(); // 0 = Sunday, 1 = Monday, ...  
switch (day) {  
  case 0:  
  case 6:  
    console.log("Weekend");  
    break;  
  default:  
    console.log("Weekday");  
}  
```  
In this example, case 0 and 6 (Sunday and Saturday) both execute the same code (“Weekend”) because we intentionally omitted a break between them, causing fall-through so that both 0 and 6 lead into the same code block.

## Conditional (Ternary) Operator Recap  
Though not a statement, recall the ternary operator `?:` from the previous chapter as a concise alternative for simple if-else:  
```js  
let max = (a > b) ? a : b;  
```  
This sets `max` to `a` if `a > b`, otherwise to `b`. Use it for simple decisions, but prefer `if` for more complex logic or multiple statements to keep code readable.

## Best Practices  
- Keep the conditions in if/else if mutually exclusive when possible. If multiple conditions can be true, ensure your ordering handles the priority or use separate ifs if they’re independent.  
- In a switch, remember to break; unintended fall-through is a common bug. If you *want* to fall through, add a comment like `// fallthrough` to make it clear.  
- For boolean flags, you can use them directly in conditions (e.g., `if (isReady) {...}`), but for non-boolean values, explicitly compare to avoid confusion (`if (count > 0)` rather than `if (count)` is often clearer to readers).  

---

**Exercise:** Write a function `getDayName(num)` that takes a number 0-6 and returns the weekday name ("Sunday" to "Saturday"). Use a switch statement inside. If the input is not 0-6, return "Invalid day". Test it with various inputs. This will help solidify your understanding of switch and case matching.

# Chapter 6: Loops (while, do-while, for)  
Loops allow you to execute a block of code repeatedly, either a set number of times or until a condition is met. JavaScript provides several looping constructs: `while`, `do...while`, and `for`. In this chapter, we'll explore these fundamental loops.

## while Loop  
The **while** loop runs as long as a condition remains true. It’s useful when you don’t know in advance how many times to iterate – the loop continues until some condition is false.  

**Syntax:**  
```js  
while (condition) {  
  // code block to execute repeatedly  
}  
```  
The condition is checked at the start of each loop iteration. If it’s true, the loop body executes, then it checks again, etc. If it’s false at the start, the loop body may not run at all.  

**Example – while:**  
```js  
let count = 5;  
while (count > 0) {  
  console.log(`Countdown: ${count}`);  
  count--;  
}  
console.log("Blast off!");  
```  
This will print countdown messages from 5 to 1, then "Blast off!". The variable `count` is decremented each time, eventually making the condition `count > 0` false and ending the loop. Always ensure your while loop will eventually make the condition false; otherwise, you get an infinite loop.

## do...while Loop  
The **do...while** loop is similar to `while`, but it guarantees the loop body runs at least once because the condition check happens *after* the first execution.  

**Syntax:**  
```js  
do {  
  // code block to execute  
} while (condition);  
```  
Note the semicolon at the end of a do...while loop.  

**Example – do...while:**  
```js  
let input;  
do {  
  input = prompt("Enter a number greater than 10:");  
} while (input <= 10);  
console.log("Thank you! You entered:", input);  
```  
In this pseudo-browser example, the prompt will show at least once, and then keep re-showing until the user enters a number > 10. This loop is useful when you want to run the body at least one time regardless of the condition.

## for Loop  
The **for** loop is a compact way to iterate a specific number of times, or over a range of values. It has three parts: initialization, condition, and final expression, all in one line.  

**Syntax:**  
```js  
for (initialization; condition; finalExpression) {  
  // loop body  
}  
```  
- **Initialization**: executed once at the beginning (e.g., `let i = 0`).  
- **Condition**: checked before each iteration; loop runs while true.  
- **Final Expression**: executed at the end of each iteration (e.g., `i++` to move to the next iteration).  

**Example – for loop:**  
```js  
for (let i = 1; i <= 5; i++) {  
  console.log("Iteration", i);  
}  
```  
This will print “Iteration 1” through “Iteration 5”. Here, `i` starts at 1, the loop runs while `i <= 5` is true, and `i++` increments `i` each time. When `i` becomes 6, the condition fails and the loop stops.

The for loop is commonly used for iterating over arrays by index:  
```js  
let arr = ["a", "b", "c"];  
for (let index = 0; index < arr.length; index++) {  
  console.log(index, arr[index]);  
}  
```  

## Breaking Out and Continuing  
- **break**: You can use `break` inside any loop to immediately exit the loop entirely. Execution continues after the loop.  
- **continue**: Use `continue` to skip the rest of the current loop iteration and jump to the next iteration (the condition check will happen immediately for while/do, or the finalExpression then condition for a for loop).  

**Example – break/continue:**  
```js  
for (let i = 1; i <= 10; i++) {  
  if (i === 5) {  
    console.log("Found 5, breaking out!");  
    break;            // exit loop completely when i is 5  
  }  
  if (i % 2 === 0) {  
    continue;         // skip even numbers  
  }  
  console.log(i);     // this will print only odd numbers until it breaks at 5  
}  
```  

In this snippet, when `i` reaches 5, the loop breaks, so you see output for 1,3 (and “Found 5...” at 5) and then it stops. If the break wasn’t there, it would print 1,3,5,7,9 (odd numbers only) due to the continue skipping evens.

## Infinite Loops and Cautions  
Be careful to avoid infinite loops. For example,  
```js  
// Warning: Infinite loop if uncommented  
// while (true) {  
//   // do something forever  
// }  
```  
Unless you have a `break` inside, this would run forever. When using while loops, ensure something inside the loop updates a condition so that the loop will terminate. With for loops, double-check your condition and increments. A common bug: using the wrong condition or forgetting to update the loop variable.

Also, when iterating arrays with a for loop, off-by-one errors are common. Remember that if an array has length N, the last index is N-1. Loop conditions often use `< arr.length` (not `<=`) to avoid going out of bounds.

---

**Practice:**  
1. Use a while loop to sum numbers from 1 to 100. Compare with doing the same using a for loop.  
2. Create a multiplication table using nested loops: an outer loop from 1 to 5, and an inner loop from 1 to 5. Print the product of the outer and inner loop counters (forming a 5x5 multiplication grid). This will practice looping within loops.  

Understanding these basic loops will build a foundation for more advanced looping patterns and iterations, which we will expand on with arrays and other structures.

# Chapter 7: Variations of for (for, for..in, for..of, forEach)  
JavaScript offers additional variations of the `for` loop to iterate over collections in more convenient ways. These include `for...in` for object property iteration, `for...of` for iterating over iterable values (like arrays), and higher-order methods like `forEach` on arrays. In this chapter, we explore these patterns and when to use each.

## The classic for loop (recap)  
We’ve already covered the classic `for` loop with an index. It’s very flexible – you can use it to iterate numbers, array indices, or even run indefinitely with a break. However, when dealing with collections like arrays or objects, there are specialized loops:

## for...in  
The **for...in** loop iterates over the *enumerable properties* of an object. It gives you each key (property name) on each iteration. It can also be used on arrays, where it will iterate over the array indices (which are property names "0", "1", ...).  

**Syntax:**  
```js  
for (let key in object) {  
  // use object[key] to get the value  
}  
```  

**Example – for...in with object:**  
```js  
let person = { name: "Charlie", age: 28, city: "London" };  
for (let prop in person) {  
  console.log(prop, "=", person[prop]);  
}  
// Output:  
// name = Charlie  
// age = 28  
// city = London  
```  
In each loop, `prop` is assigned to each property name of `person`. We then access the value with `person[prop]`. The iteration order is not strictly guaranteed (though in practice it often follows insertion order for normal objects in modern engines, but you shouldn’t rely on it).

**for...in with arrays:** It will iterate over indices that have values. But caution: `for...in` on arrays is generally not recommended because it iterates over *all enumerable properties*, not just numeric indices – if you or some library adds custom properties to the Array prototype, those might appear too. Also it iterates indices as strings. Typically, use traditional `for` or `for...of` or array methods for arrays, not `for...in`.  

## for...of  
The **for...of** loop (introduced in ES6) is designed for iterating over the values in an iterable (like arrays, strings, Maps, Sets, etc.). It gives you each element directly, without needing an index.  

**Syntax:**  
```js  
for (let value of iterable) {  
  // use value directly  
}  
```  

**Example – for...of with array:**  
```js  
let colors = ["red", "green", "blue"];  
for (let color of colors) {  
  console.log(color);  
}  
// Output: red, green, blue (each on new line)  
```  
Here, `color` takes on each element of the array in sequence. This is convenient and clean for simply reading values from an array.  

**Example – for...of with string:**  
```js  
for (let ch of "hello") {  
  console.log(ch);  
}  
// Output: h, e, l, l, o (each on new line)  
```  
For a string, it iterates over each character.

**Iterable protocol:** Under the hood, `for...of` uses an object's **iterator**. Most built-in collection types are iterable. Custom objects can be made iterable by defining a `[Symbol.iterator]` method, but that’s an advanced topic.

**Difference between for...in and for...of:**  
- `for...in` iterates over keys (property names). Use it for objects (plain object literals).  
- `for...of` iterates over values of an iterable. Use it for arrays, strings, maps, sets, etc., when you just need each value.  

For arrays, `for...of` is typically preferable to `for...in`. For objects, you cannot use `for...of` directly (objects aren’t iterable by default), so `for...in` or `Object.keys()` with a normal for is used.

## Array.prototype.forEach  
Array instances come with a built-in method `forEach` which allows you to iterate the array by providing a callback function. It’s a higher-order function (a function that takes another function as an argument).

**Syntax:**  
```js  
array.forEach(function(element, index, array) {  
  // use element (and index if needed)  
});  
```  
The callback will be called for each element in the array. It receives the element value, the index, and the whole array as arguments (usually you just need the first one or two).

**Example – forEach:**  
```js  
let numbers = [10, 20, 30];  
numbers.forEach((num, idx) => {  
  console.log(`Index ${idx}: ${num}`);  
});  
// Output:  
// Index 0: 10  
// Index 1: 20  
// Index 2: 30  
```  
This does the same as a simple for-of or for loop, but in a functional style. `forEach` is convenient and expressive. Note that you cannot `break` out of a `forEach` loop or use `continue` directly; once started, it will call the callback for every element (to prematurely stop, you’d have to throw an exception or use some external flag – which is not ideal). So use `forEach` when you want to process every element. If you need to break out early, stick to a regular loop.

## When to use which:  
- **Classic for (with index)**: When you need the index or need to iterate in a custom order or step. Also if you need to break/continue flexibly. Good for numeric loops or accessing arrays by index.  
- **for...of**: When you just need each value from an array (or iterable) and don’t need the index. It’s concise and avoids off-by-one errors. You can use `break` and `continue` with it.  
- **for...in**: When iterating over the properties of an object (not an array). Or in rare cases, iterating over array indices, but be cautious.  
- **forEach**: When you want to apply a function to each array element. It can lead to more functional code style and can be handy for in-place operations where you don't need to break early.

**Example – Using different loops for an array:**  
```js  
let letters = ['a', 'b', 'c'];  

// Classic for  
for (let i = 0; i < letters.length; i++) {  
  console.log(i, letters[i]);  
}  

// for...of  
for (let letter of letters) {  
  console.log(letter);  
}  

// forEach  
letters.forEach(letter => console.log(letter));  
```  
All three above will ultimately print the letters, but with slight differences in approach. Use what’s most readable and appropriate for the task.

**Note:** There are other array iteration methods like `map`, `filter`, `reduce` which we will discuss in the next chapter. They allow powerful patterns for processing arrays in a functional style.

---

**Try This:** Given an object with key-value pairs, use `for...in` to print its contents. Then, convert that object’s keys into an array (using `Object.keys`) and loop through it with `forEach`, printing both key and value. This will illustrate both approaches on object-like data.

# Chapter 8: forEach, map, filter, reduce  
JavaScript arrays have several powerful methods that come from functional programming concepts. These allow you to process arrays declaratively, often in a chainable way. The most commonly used ones are `forEach`, `map`, `filter`, and `reduce`. We saw `forEach` briefly; now let’s dive into it and the others with examples to illustrate their use and how they differ.

## Array.forEach (revisited)  
`forEach` executes a provided function once for each array element. It’s primarily for side effects (like logging, updating a variable outside, etc.) since it doesn’t return a new value (it always returns `undefined`). We covered usage in the last chapter. Remember: you can’t break out early from `forEach`.

**Use case**: Performing an action for each item (like summing into an external variable, or calling a function on each element).

Example:  
```js  
let sum = 0;  
[1, 2, 3].forEach(num => { sum += num });  
console.log(sum); // 6  
```  
Here we accumulate sum as a side effect.

## Array.map  
`map` is used to transform an array by applying a function to each element and producing a new array of the same length with transformed values It does **not** modify the original array (it returns a new one).

**Syntax:**  
```js  
let newArray = arr.map(callback(element, index, array) { ... });
```  
The callback returns the new value for each element.

**Example – map:**  
```js  
let numbers = [1, 2, 3];  
let doubled = numbers.map(n => n * 2);  
console.log(doubled);    // [2, 4, 6]  
console.log(numbers);    // [1, 2, 3] (original unchanged)  
```  
We took an array of numbers and mapped it to a new array of each number doubled. Common uses of map: converting data format (e.g., array of objects to array of strings by picking a property), or applying a calculation to each element.

Another example, transforming an array of strings:  
```js  
let names = ["alice", "Bob", "cHaRlie"];  
let normalized = names.map(name => name.charAt(0).toUpperCase() + name.slice(1).toLowerCase());  
console.log(normalized); // ["Alice", "Bob", "Charlie"]  
```  
Each name is transformed to capitalized form. Map makes it concise.

## Array.filter  
`filter` is used to select a subset of elements from an array that meet certain criteria It returns a new array with only the elements for which the callback returns true (or a truthy value). The original array is not changed.

**Syntax:**  
```js  
let newArray = arr.filter(callback(element, index, array) { ... });
```  
The callback should return a boolean – `true` to keep the element, `false` to exclude it.

**Example – filter:**  
```js  
let numbers = [5, 12, 8, 130, 44];  
let big = numbers.filter(n => n > 10);  
console.log(big);      // [12, 130, 44] (numbers greater than 10)  
console.log(numbers);  // [5, 12, 8, 130, 44] (original unchanged)  
```  
We filtered out numbers <= 10.

Another example: filtering objects:  
```js  
let users = [  
  { name: "Alan", active: true },  
  { name: "Becky", active: false },  
  { name: "Charlie", active: true }  
];  
let activeUsers = users.filter(user => user.active);  
// activeUsers will contain the objects for Alan and Charlie (active: true)  
```  
Filter is great for getting subsets (e.g., all active users, all tasks that are done, all array items that match a condition).

## Array.reduce  
`reduce` (also known as fold) is the most powerful but also the most conceptually challenging of these methods. It reduces the array to a single value (or a new structure) by accumulating results of a callback function. You provide an initial accumulator value, then for each element, the callback updates the accumulator, and finally returns it.

**Syntax:**  
```js  
let result = arr.reduce(function(accumulator, element, index, array) {  
    // compute newAccumulator from accumulator and element  
    return newAccumulator;  
}, initialValue);
```  
- `initialValue` is the starting value for the accumulator (if omitted, the first array element is used as the initial accumulator and iteration starts from second element – but it’s usually clearer to provide an initial value explicitly).  
- The callback takes the current `accumulator` and an element and returns the updated accumulator.

**Example – reduce (summing):**  
```js  
let arr = [1, 2, 3, 4];  
let sum = arr.reduce((acc, num) => acc + num, 0);  
console.log(sum); // 10  
```  
Here, `acc` starts at 0, then goes through: 0+1 -> 1, then 1+2 -> 3, then 3+3 -> 6, then 6+4 -> 10, which is returned.

**Example – reduce (product):**  
```js  
let product = arr.reduce((acc, num) => acc * num, 1);  
console.log(product); // 24 (1*2*3*4)  
```  

Reduce can do much more than summing: you can use it to transform arrays into objects, count things, group items, etc. For instance, turning an array of strings into a single string:  
```js  
let words = ["Hello", "World", "!"];  
let sentence = words.reduce((acc, w) => acc + " " + w);  
console.log(sentence); // "Hello World !"  
```  
(We didn’t provide initialValue here, so acc starts as "Hello", then goes through the rest.)

A more complex example: use reduce to count occurrences of letters in an array:  
```js  
let letters = ["a", "b", "a", "c", "b", "a"];  
let counts = letters.reduce((acc, letter) => {  
  acc[letter] = (acc[letter] || 0) + 1;  
  return acc;  
}, {});  
console.log(counts); // { a: 3, b: 2, c: 1 }  
```  
Here we built an object mapping each letter to how many times it appears by accumulating on an object.

## Combining map, filter, reduce  
These methods can be chained for powerful effect, often in a single line (though for readability, break it into multiple lines). For example:  

**Example – chain map and filter:**  
```js  
let nums = [1, 2, 3, 4, 5, 6];  
let result = nums  
  .filter(n => n % 2 === 0)    // take even numbers [2,4,6]  
  .map(n => n * n);            // square them -> [4,16,36]  
console.log(result);  
```  
We first filtered evens, then squared them. You could further reduce that to get a sum of squares of even numbers:  
```js  
let sumOfSquaresOfEvens = nums  
  .filter(n => n % 2 === 0)  
  .map(n => n * n)  
  .reduce((acc, n) => acc + n, 0);  
console.log(sumOfSquaresOfEvens); // 56 (4+16+36)  
```  

These array methods support a functional programming style. They often make code more concise and expressive, but they might be a bit slower than basic loops in some cases (usually negligible difference for most use cases). They also create new arrays for intermediate steps (`map` and `filter` do), so keep that in mind for very large data if performance is critical.

## When to use what:  
- Use **map** when you want to transform each element of an array into a corresponding element of a new array.  
- Use **filter** when you want to remove some elements and keep others based on a condition.  
- Use **reduce** when you want to compute a single summary value (or object) from a list of values.  
- Use **forEach** when you just need to execute some code for each element (and you aren’t trying to produce a new array or value from it).

With practice, these become natural. They can often replace loops that accumulate results with more succinct code.

---

**Exercise Ideas:**  
1. Given an array of numbers, use `filter` to get only the primes (you may need a helper function to test for prime).  
2. Given an array of strings, use `map` to create a new array of their lengths.  
3. Use `reduce` on an array of grades (numbers) to calculate the average grade.  
4. Combine `filter` and `reduce`: from an array of objects representing products (with a `price` property), filter those above a certain price, then use reduce to compute the total cost of the filtered products.  

Trying these will reinforce how these methods work and how they can simplify operations on arrays.

# Chapter 9: Functions (declaration, invocation, parameters, and arguments)  
Functions are the building blocks of structured and reusable code in JavaScript. This chapter covers how to declare functions, call them (invoke), and how parameters and arguments work.

## Function Declarations  
A **function declaration** defines a named function that can be called (invoked) in code.  

**Syntax:**  
```js  
function functionName(parameter1, parameter2, ...) {  
  // code block  
  // optionally return a value  
}  
```  
Function declarations are hoisted, meaning you can call them even before their definition in the code (the JS engine loads them during the compilation phase).

**Example – function declaration:**  
```js  
function greet(name) {  
  console.log("Hello, " + name + "!");  
}  

greet("Alice"); // outputs: Hello, Alice!  
```  

If a function should return a value, use the `return` statement. If no return is provided, the function returns `undefined` by default when called.

**Example – function with return:**  
```js  
function add(a, b) {  
  return a + b;  
}  

let sum = add(3, 4);  
console.log(sum); // 7  
```  

## Function Expressions  
You can also define a function as a **function expression**, where the function is part of an expression (often assigned to a variable). Function expressions can be named or anonymous.  

**Example – function expression:**  
```js  
const multiply = function(x, y) {  
  return x * y;  
};  

console.log(multiply(3, 4)); // 12  
```  
Here we assigned an anonymous function to the variable `multiply`. Unlike function declarations, function expressions are not hoisted (you can only call them after the assignment in code order).

## Arrow Functions (ES6)  
Arrow functions are a shorter syntax for function expressions, especially useful for simple callbacks or one-liners. We'll cover them in detail in Chapter 22 (ES6 Features), but here’s a quick example:  
```js  
const square = (n) => { return n * n; };  
// or shorter: const square = n => n * n;  (implicit return for single expression)  
console.log(square(5)); // 25  
```  
Arrow functions have special behavior with `this` (they don’t have their own `this`), which we’ll discuss later.

## Invoking (Calling) Functions  
To execute a function, you use parentheses `()` after its name or variable reference, passing arguments if needed: `functionName(arg1, arg2)`.  

When a function is called, the values passed are assigned to the function’s parameters. The number of arguments can differ from number of parameters – JavaScript doesn’t enforce matching arity:
- If too few arguments are passed, the missing parameters become `undefined`.  
- If extra arguments are passed, they are simply ignored unless you use special syntax to capture them (like rest parameters, or the `arguments` object discussed below).

**Example – invoking with different arguments:**  
```js  
function printTwo(a, b) {  
  console.log("A:", a, "B:", b);  
}  
printTwo(1, 2);        // A: 1 B: 2  
printTwo(5);           // A: 5 B: undefined (second param missing)  
printTwo(7, 8, 9);     // A: 7 B: 8 (third argument 9 is ignored)  
```  

## Parameters vs Arguments  
- **Parameters** are the variable names in the function definition. They act as placeholders for the values.  
- **Arguments** are the actual values you pass to the function when calling it  

For example, in `function greet(name) {...}`, `name` is a parameter. When you call `greet("Alice")`, the argument is `"Alice"`. The parameter `name` will refer to the argument value `"Alice"` inside the function

A function can have zero parameters (e.g., `function sayHi() { console.log("Hi"); }`), in which case it just doesn’t expect any arguments.

## Default Parameters (ES6)  
You can provide default values for parameters in case the caller doesn’t supply them:  
```js  
function multiply(a, b = 1) {  
  return a * b;  
}  
console.log(multiply(5));    // 5, because b defaults to 1  
console.log(multiply(5, 3)); // 15, b is 3  
```  
Here, if `b` is not provided or is `undefined`, it defaults to 1.

## Rest Parameters (Varargs)  
Sometimes you want a function to accept an arbitrary number of arguments. Rest parameters allow you to capture them into an array. Use `...` before the last parameter name:  
```js  
function sumAll(...numbers) {  
  return numbers.reduce((acc, n) => acc + n, 0);  
}  
console.log(sumAll(1, 2, 3, 4)); // 10  
```  
In `sumAll`, all arguments are gathered into the array `numbers` inside the function. Rest parameters must come at the end of the parameter list.

Prior to rest parameters, the `arguments` object (an array-like object available inside every function) was used to get all arguments. `arguments` still exists (except in arrow functions), but rest parameters are the modern, preferred way as they are true arrays and easier to work with.

## Scope of Variables in Functions  
Variables declared inside a function (with `let`, `const`, or `var`) are local to that function. You cannot access them outside the function. Parameters are also treated as local variables inside the function body. We will discuss scope in depth in Chapter 11, but in short: each function call creates a new scope (execution context) for its variables.

## Function as First-Class Citizens  
In JavaScript, functions are first-class objects:  
- They can be stored in variables (as seen with function expressions).  
- They can be passed as arguments to other functions, or returned from functions (this is key to callbacks and functional programming).  
- They have properties and methods (e.g., you can set `func.description = "This function does X"` though that’s not common).

Example of passing a function as an argument (callback):  
```js  
function repeatNTimes(action, n) {  
  for (let i = 0; i < n; i++) {  
    action();  // call the function passed in  
  }  
}  
function sayHello() { console.log("Hello"); }  
repeatNTimes(sayHello, 3);  
// Outputs "Hello" three times  
```  
Here `repeatNTimes` accepts an `action` function and calls it `n` times. We passed `sayHello` (note we pass the function *reference* without `()` so it’s not called immediately) as the callback.

This ability to treat functions as data opens the door to many programming patterns (callbacks, higher-order functions, etc., which we explore in later chapters like Chapter 10 on functional programming).

## Anonymous and IIFE Functions  
Functions don’t require a name; anonymous functions are common in expressions (as in `const foo = function() {}` or when passing a function inline to `forEach`). There’s also the concept of Immediately Invoked Function Expressions (IIFE), which are functions defined and invoked at the same time, often used to create a new scope or module pattern (less needed now with block scope and modules, but historically important). An IIFE looks like:  
```js  
(function() {  
  console.log("This runs immediately");  
})();  
```  
Notice the parentheses around the function and after it – that defines a function and calls it immediately.

---

**Practice:**  
- Write a function `isEven(n)` that returns true if n is even, false otherwise. Test it with various numbers.  
- Write a function `countChars(str, char)` that returns the number of times `char` appears in `str`. Use a loop or array methods inside.  
- Write an `adder(...nums)` function that uses rest parameters to accept any number of numeric arguments and returns their sum (essentially like `sumAll` above).  
- Try writing a function as a function expression assigned to a variable, and another as an arrow function, to get comfortable with the different syntaxes.  

Understanding how to define and use functions with parameters and return values will set the stage for more advanced topics like closures, callbacks, and object methods.

# Chapter 10: Functional Programming  
Functional programming (FP) is a programming paradigm where functions are treated as first-class entities and writing code without side effects is emphasized. JavaScript is multi-paradigm: you can write in an imperative style or a functional style, or a mix. In this chapter, we’ll discuss some core concepts of functional programming as they apply to JavaScript.

## First-Class Functions and Higher-Order Functions  
JavaScript functions are **first-class citizens** – you can pass them around just like data. A **higher-order function** is a function that takes one or more functions as arguments, or returns a function. We’ve already seen examples: `array.forEach` takes a function callback, `repeatNTimes` from last chapter takes a function. These are higher-order functions.

Functional programming often uses higher-order functions extensively for abstraction. For example, instead of writing a loop each time, you might have a generic function that can apply any operation on elements (like `map`, `filter` we discussed, which are higher-order functions).  

**Example – higher-order function:**  
```js  
function applyTwice(f, value) {  
  return f(f(value));  
}  
let double = x => x * 2;  
console.log(applyTwice(double, 5)); // 20 -> double(double(5))  
```  
Here `applyTwice` takes a function `f` and a value, and applies `f` two times. We passed the `double` function and the number 5.

## Pure Functions and Side Effects  
A key concept in FP is the idea of **pure functions**. A pure function is one that, given the same inputs, will always return the same output and has **no side effects** ([Pure function - Wikipedia](https://en.wikipedia.org/wiki/Pure_function#:~:text=following%20properties%3A,))  Side effects include modifying variables outside its scope, changing global state, doing I/O (like alert or console log), or mutating its inputs.

Pure functions are easier to test and reason about because they don’t depend on hidden state and don’t alter state outside of them. They just take input and produce output.

**Example – pure vs impure:**  
```js  
// Pure function: depends only on inputs, no side effects  
function pureAdd(a, b) {  
  return a + b;  
}  

// Impure function: uses external variable (side effect on external state)  
let total = 0;  
function impureAddToTotal(x) {  
  total += x;  // modifies outer state  
}  
```  
`pureAdd(2,3)` will always return 5. But `impureAddToTotal(5)` changes the external `total` variable; its effect depends on and alters outside state – not pure.

In practice, not all functions can be pure (especially if we need to interact with the world, like DOM manipulation or network calls). But understanding the distinction is important. Strive to keep functions pure when possible (especially in critical logic), and isolate side effects.

## Immutability  
Functional programming prefers **immutability**, meaning not changing data but instead producing new data structures. For instance, rather than modifying an array, a functional approach might create a new array with the changes (methods like `map`, `filter` naturally do this). This avoids unintended side effects on shared data.

Example: instead of sorting an array in place, one might use a spread to copy and then sort:  
```js  
const original = [3,1,4];  
const sorted = [...original].sort((a,b) => a-b);  
console.log(original); // [3,1,4] (unchanged)  
```  
We created a new sorted array, leaving the original intact.

## Functions as Values (Lambdas)  
We often use **anonymous functions** (also called lambda expressions in FP) directly as arguments to other functions. For example, `nums.map(x => x*x)` uses an arrow function inline without naming it. This is a common FP style: define the function at the point of use if it's simple or not reused.

## Recursion  
Functional programming languages often use recursion (a function calling itself) instead of loops for repetitive processes. JavaScript supports recursion, though it doesn’t have tail-call optimization in all implementations (which means deep recursion could hit a call stack limit).  

**Example – recursive sum:**  
```js  
function recursiveSum(n) {  
  if (n <= 1) return n;  
  return n + recursiveSum(n-1);  
}  
console.log(recursiveSum(5)); // 15 (i.e., 5+4+3+2+1)  
```  
This is more of an academic example; a loop would be simpler for this case in JS. But some problems are naturally recursive (like tree traversal).

## Avoiding Side Effects Example  
Suppose you have an array and you want to get a sorted version of it and then get the first element. An imperative approach might do:  
```js  
let arr = [3,1,4];  
arr.sort((a,b)=>a-b);             // sorts in place (side effect on arr)  
let smallest = arr[0];  
```  
This changed `arr`. A more functional approach:  
```js  
const arr2 = [3,1,4];  
const sortedArr = [...arr2].sort((a,b)=>a-b);  // non-destructive  
const [minValue] = sortedArr;                 // array destructuring to get first  
```  
Now `arr2` remains unsorted as originally, and we have `minValue` without side effects on the original data.

## Declarative vs Imperative  
Functional style tends to be more **declarative** – you describe what you want done, rather than how to do it step by step. Using array methods like `filter` and `map` is declarative (you say “filter this array for these conditions, then map to these new values”). A for-loop with pushes is more **imperative** (you explicitly instruct how to iterate and build the result). Declarative code can be more concise and easier to read at a glance.

## Example: Functional Composition  
Functional programming often involves **composing** small functions into more complex operations. For instance, if you have a series of transformations to apply, you might do:  
```js  
const result = transform3(transform2(transform1(input)));  
```  
This is function composition manually. Libraries or functional helpers can make this cleaner (like a `compose(f, g, h)` function that returns a new function equivalent to `f(g(h(x)))`). Without going too deep, just recognize that calling functions inside of functions is a form of composition.

## Real-world FP in JS  
JavaScript isn’t purely functional, but many libraries (like React for UI, or Redux for state management) encourage a functional approach: using pure functions for components or reducers, avoiding direct mutation of data, etc. Even if you’re not strictly following FP, using its principles (like pure functions and immutability) can lead to fewer bugs.

**Example – using map/filter (FP style) vs loop (imperative style):**  
```js  
// Imperative: find names of active users  
let activeUserNames = [];  
for (let user of users) {  
  if (user.active) {  
    activeUserNames.push(user.name);  
  }  
}  

// Functional: using filter and map  
let activeUserNames2 = users  
  .filter(u => u.active)  
  .map(u => u.name);  
```  
Both achieve the same result. The functional version is shorter and more expressive (“filter these users to active ones, then map to their names”), whereas the imperative version spells out the how (initializing an array, looping, pushing conditionally).

Neither is objectively “better” in all cases, but understanding both styles is valuable. Often you might mix them (some parts functional style, some parts imperative when needed for clarity or performance).

---

**Exercises:**  
- Write a pure function `capitalize(str)` that returns a new string with the first letter capitalized and the rest lowercased, without modifying the original string.  
- Take an array of numbers and use functional style (map/filter/reduce) to compute the average of the even numbers only.  
- Consider a list of objects representing bank transactions (with fields like `{amount: 100, type: "deposit"}`), and use reduce to compute the net balance (deposits add, withdrawals subtract). Ensure your reduce callback doesn’t modify any external variables – it should just accumulate and return the total.  

These will help reinforce avoiding side effects (don’t modify the original array or external state, produce new values instead) and using higher-order functions for clarity.

# Chapter 11: Scope, Closure, Callbacks  
This chapter dives into some of the trickier but powerful aspects of JavaScript: **scope** (the lifetime and visibility of variables), **closures** (functions remembering their outer variables), and **callbacks** (passing functions around to be executed later).

## Scope in JavaScript  
**Scope** determines where variables and functions are accessible in code. JavaScript uses **lexical (static) scope**, meaning scope is determined by the structure of the code (the nesting of blocks and functions), not by the call stack (who calls what).

There are a few kinds of scope:  
- **Global scope**: Variables declared outside any function or block. Accessible anywhere (unless shadowed by local variables).  
- **Function scope**: Each function creates a scope for its variables (and parameters). Variables declared with `var` are function-scoped.  
- **Block scope** (ES6): Variables declared with `let` or `const` inside a `{ ... }` block (like in if, for, while, or just standalone block) are only visible in that block.

**Example – scope and shadowing:**  
```js  
let x = 10;  
function foo() {  
  let y = 20;  
  console.log(x); // 10 (x is accessible, global)  
  if (y > 10) {  
    let z = 30;  
    console.log(x, y, z); // 10 20 30  
  }  
  // console.log(z); // Error: z is not defined (z is block-scoped inside if)  
}  
foo();  
// console.log(y); // Error: y is not defined (y is function-scoped inside foo)  
```  
Here, `x` is global, `y` exists only inside `foo`, and `z` exists only inside that if-block within `foo`.

If we had `var z = 30` in the if, that would actually hoist to function scope of `foo` (since `var` is not block-scoped), meaning it would be accessible anywhere in `foo`. This is one reason `let/const` is preferred now: block scoping avoids confusion.

**Hoisting:** Function declarations and `var` declarations are hoisted to the top of their scope. That’s why you can call a function declared later in the code, or use a `var` variable before its definition (though the variable will be `undefined` until the assignment is executed). `let` and `const` are hoisted too but in a different way – they are in a "temporal dead zone" until the line where they are defined, so you cannot use them before declaration (you’ll get an error).

## Closures  
A **closure** is created when a function is defined inside another function, and the inner function continues to have access to the outer function’s variables even after the outer function has returned ([JavaScript Function Closures - W3Schools](https://www.w3schools.com/js/js_function_closures.asp#:~:text=A%20closure%20is%20a%20function,used%20to%3A%20Create%20private))  In JavaScript, whenever you have a nested function, it forms a closure capturing the variables of the outer scope.

**Definition:** A closure is a function bundled with its lexical environment of outer variables ([JavaScript Function Closures - W3Schools](https://www.w3schools.com/js/js_function_closures.asp#:~:text=A%20closure%20is%20a%20function,used%20to%3A%20Create%20private))  

**Example – closure:**  
```js  
function makeCounter() {  
  let count = 0;  
  return function() {        // inner function forms a closure  
    count++;                 // access outer variable  
    return count;  
  };  
}  

const counter1 = makeCounter();  
console.log(counter1()); // 1  
console.log(counter1()); // 2  

const counter2 = makeCounter();  
console.log(counter2()); // 1 (counter2 has its own `count` separate from counter1)  
```  
In this example, `makeCounter` returns an inner function that increments `count`. When we call `makeCounter()`, it creates a new `count` and returns a function that can access `count`. That inner function *closes over* `count`. Even after `makeCounter` call finishes, the `counter1` function still has access to `count` via the closure. Each call to `makeCounter` creates a new closure with its own `count` – that’s why counter1 and counter2 don’t interfere.

Closures are a powerful concept. They enable **private variables** (as in the above example, `count` is like a private state accessible only through the returned function). They are used in many patterns and are fundamental to how JavaScript’s callbacks and functional patterns work.

**Key point:** The outer function’s variables live on as long as the inner function that uses them is still in use. They are not garbage-collected when the outer function returns if an inner function still references them.

## Callbacks  
A **callback** is simply a function passed into another function to be invoked at a later time or under certain conditions. This is a common way to handle asynchronous operations or to customize behavior.

For example, event handlers are callbacks:  
```js  
button.addEventListener('click', () => {  
  console.log('Button clicked!');  
});  
```  
Here we pass an arrow function as a callback to be called when the button is clicked (at some future time, not immediately).

Another example:  
```js  
function requestData(url, onSuccess, onError) {  
  // simulate an async request  
  setTimeout(() => {  
    if(url === "good") {  
      onSuccess({ data: "Some data" });  
    } else {  
      onError("Error: bad url");  
    }  
  }, 1000);  
}  

requestData("good",  
  response => { console.log("Got", response.data); },    // success callback  
  err => { console.error(err); }                        // error callback  
);  
```  
`requestData` takes two callbacks: one for success and one for error. It uses `setTimeout` to simulate an asynchronous operation (perhaps fetching data). After 1 second, it calls one of the callbacks. This demonstrates the inversion of control in asynchronous programming: we pass functions to be executed later by some library or event loop. 

Callbacks often form nested structures when you have to do a sequence of async operations (leading to the famous “callback hell” or pyramid of doom, which we’ll cover in Chapter 17). Modern JavaScript often uses Promises or `async/await` to avoid deep nesting, but understanding callbacks is fundamental as they underlie those abstractions.

Callbacks and closures often go hand-in-hand: the callback function forms a closure over the environment where it’s defined. For instance, if our success callback in the above example accessed some variable from the outer scope of `requestData` call, it would still have it when called later.

**Example – closure with callback:**  
```js  
function createDelayedIncrement(x) {  
  return function(delay) {  
    setTimeout(() => {  
      // this callback closes over x  
      console.log(x + 1);  
    }, delay);  
  };  
}  

let incrementLater = createDelayedIncrement(10);  
incrementLater(1000); // after 1s, logs 11  
```  
Here `createDelayedIncrement` returns a function that, when called with a delay, will log `x+1` after that delay. The arrow function given to `setTimeout` is a callback that closes over `x`.

## Scope and this (briefly)  
Though `this` is part of function execution context rather than lexical scope, it’s often discussed alongside scope. We’ll cover `this` more in Chapter 27 with classes and in context of call/apply, but in brief:
- In a regular function, `this` is determined by how the function is called (the object before the dot, or global if just called plainly, or undefined in strict mode if plain call).  
- In arrow functions, `this` is not its own – it inherits from the outer scope’s `this`.  

Closures capture variables, but not `this` in the sense that an inner function’s `this` can be different. If you need to use outer `this` in a callback, an arrow function is handy because it keeps `this` from outer scope.

**Example – traditional vs arrow with this:**  
```js  
function Person(name) {  
  this.name = name;  
  this.sayLater = function() {  
    setTimeout(function() {  
      console.log("Hi, I'm " + this.name);  // 'this' here is not Person's this, it's window/global or undefined in strict mode  
    }, 1000);  
  };  
  this.sayLaterArrow = function() {  
    setTimeout(() => {  
      console.log("Hi, I'm " + this.name);  // 'this' here is Person's this, arrow keeps context  
    }, 1000);  
  };  
}  

let p = new Person("Sam");  
p.sayLater();       // after 1s: "Hi, I'm undefined" (or error in strict mode)  
p.sayLaterArrow();  // after 1s: "Hi, I'm Sam"  
```  
In `sayLater`, the regular function callback had its `this` lost (or bound to global), whereas the arrow function in `sayLaterArrow` closed over the `this` of the Person instance.

## Takeaways  
- **Scope**: Controls variable visibility. Use `let`/`const` for block scope. Avoid global variables when possible to prevent conflicts.  
- **Closures**: When an inner function remembers and accesses variables from an outer function even after that outer function has finished executing ([JavaScript Function Closures - W3Schools](https://www.w3schools.com/js/js_function_closures.asp#:~:text=A%20closure%20is%20a%20function,used%20to%3A%20Create%20private))  Use closures to create private state or to maintain state between function calls in a functional way.  
- **Callbacks**: Functions passed to other functions to be executed later. They are used heavily for asynchronous code and event handling. Mastering callbacks (and managing them) is crucial, though newer patterns (Promises, async/await) improve syntax, callbacks are still under the hood.

---

**Exercises:**  
1. Write a function `makeAdder(x)` that returns a new function. The returned function should take a parameter `y` and return `x + y`. This uses closure to remember `x`. Test: `let add5 = makeAdder(5); console.log(add5(3)); // 8`.  
2. Implement a simple caching function using closure: Write `cacheFunction(f)` that takes a single-argument function `f` and returns a new function. This new function, when called, should check if it has seen the argument before. If yes, return the cached result; if not, call `f`, store the result, and return it. (This demonstrates closure for the cache object.)  
3. Write a function `callTwice(callback)` that accepts a function and invokes it twice. Test it by passing an anonymous function that logs something.  
4. (Stretch) Without using `bind`, create a function `bindContext(fn, ctx)` that returns a new function that calls `fn` with `this` set to `ctx`. (This would involve using `apply` or closure capturing `ctx` and calling `fn.apply` – a bit advanced, but consolidation of this understanding and how `this` can be set manually.)  

By practicing these, you’ll deepen your understanding of closures (makeAdder and cacheFunction particularly) and callback usage.

# Chapter 12: DOM Introduction, Selection, Modifying Content  
The Document Object Model (DOM) is a programming interface for HTML documents. It represents the page structure as a tree of objects (nodes). With JavaScript, we can manipulate this DOM to change what’s displayed, react to user input, and create dynamic pages. In this chapter, we’ll see how to select elements and modify their content and attributes.

## The DOM and `document` Object  
In a web browser, the `document` global object represents the loaded HTML page. The DOM is basically accessible through `document`. For example, `document.body` references the `<body>` element of the page.

Common ways to **select DOM elements**:  
- `document.getElementById("id")` – returns the element with the given ID.  
- `document.getElementsByClassName("class")` – returns an HTMLCollection of elements with the class (live collection).  
- `document.getElementsByTagName("div")` – returns all `<div>` elements, for example.  
- **Modern:** `document.querySelector(cssSelector)` – returns the first element matching a CSS selector.  
- `document.querySelectorAll(cssSelector)` – returns a NodeList of all elements matching the selector.  

`querySelector` and `querySelectorAll` are very flexible because you can use any CSS selector (like `"div.container > p.highlight"` or `"#main h2.title"` etc.). They are widely used for their power and simplicity.

**Example – selecting elements:**  
```html
<!DOCTYPE html>
<html>
<body>
  <h1 id="header">Welcome</h1>
  <p class="intro">Hello, <span>visitor</span>!</p>
  <p class="intro">Enjoy your stay.</p>
  <script>
    const header = document.getElementById('header');
    const firstIntro = document.querySelector('.intro');      // first element with class "intro"
    const allIntroParas = document.querySelectorAll('.intro'); // all elements with class "intro"
    console.log(header.textContent);        // outputs "Welcome"
    console.log(firstIntro.innerText);      // "Hello, visitor!"
    console.log(allIntroParas.length);      // 2
  </script>
</body>
</html>
```  
Here we grabbed elements by ID and class. `querySelectorAll('.intro')` returned a NodeList of two `<p>` elements.

## Reading and Changing Content  
Once you have a DOM element, there are several properties to get or set its content:  
- `element.innerText` – gets/sets the visible text content, not including hidden text or inner HTML markup.  
- `element.textContent` – gets/sets the text content including text in hidden elements, exactly as in the DOM. Good for reading/writing just text  
- `element.innerHTML` – gets/sets the HTML markup inside the element Setting `innerHTML` will parse the string as HTML and replace the element’s contents with the resulting DOM nodes.  
- `element.value` – for form inputs, the current value (e.g., text in a textbox).

**Example – modifying content:**  
```js  
header.textContent = "Hello World!";  
// The H1 now displays "Hello World!" instead of "Welcome"

firstIntro.innerHTML = 'Hi, <span style="color:red">friend</span>!';  
// The first paragraph now has its HTML changed. The span text "friend" will be red.
```  

Using `innerHTML` is convenient for injecting HTML, but be cautious if using untrusted input (to avoid XSS vulnerabilities). If inserting user-provided text, use `textContent` or other safe methods.

## Modifying Attributes and Properties  
DOM elements have attributes (like `src`, `href`, `id`, etc.) and many correspond to properties on the element objects.  
- `element.getAttribute('attrName')` – gets the attribute value as in HTML.  
- `element.setAttribute('attrName', 'value')` – sets an attribute.  
- Or often simpler: use the property. For example, `img.src = "photo.png";` is equivalent to setting the `src` attribute on an `<img>` element. Similarly, `link.href = "https://...";`, `input.value = "text";`, etc.  

For classes, there's a special `element.classList` property which is a DOMTokenList of the element’s classes and provides methods to add/remove/toggle classes easily.  
Example: `element.classList.add('active')`, `element.classList.remove('hidden')`, `element.classList.toggle('open')`.

**Example – attributes and classes:**  
```js  
const img = document.querySelector('img#logo');  
console.log(img.getAttribute('src'));  // logs current src  
img.setAttribute('alt', 'Site logo');  // sets alt attribute  
img.src = "newlogo.png";              // updates the src (property usage)  

const section = document.querySelector('section');  
section.classList.add('highlight');  
if(section.classList.contains('hidden')) {  
  section.classList.remove('hidden');  
}  
```  

## Style and CSS  
You can change element styles via the `element.style` property, which represents the inline style of the element. For example, `element.style.color = "blue";`, `element.style.fontSize = "20px";`. Only CSS properties that have been set via the `style` attribute or via this property will appear in `element.style`; it doesn’t give computed styles from CSS stylesheets. For computed style, one can use `getComputedStyle(element)`.

Often, instead of directly manipulating many styles, toggling CSS classes (and having those classes in a stylesheet) is a cleaner approach. e.g., adding a class `.hidden { display:none; }` rather than directly setting `element.style.display = "none"`.

**Example – styling:**  
```js  
header.style.color = "purple";  
header.style.backgroundColor = "#EEE";  // note: property names in JS use camelCase (background-color -> backgroundColor)  
```  

This will directly affect the element’s style attribute.

## Navigating the DOM  
From a given element, you can navigate to related nodes:  
- `element.parentElement` – the parent node (or `parentNode`, but parentElement skips text/comment nodes).  
- `element.children` – HTMLCollection of its child elements (no text nodes).  
- `element.firstElementChild`, `element.lastElementChild`.  
- `element.nextElementSibling`, `element.previousElementSibling`.  

There are also older or lower-level properties: `childNodes` (includes text nodes), `firstChild`, etc., and `nextSibling` (which includes text nodes, e.g., whitespace). Usually, the Element-only versions are easier unless you need to handle text.

**Example – traversing:**  
```js  
const list = document.querySelector('ul#menu');  
for(let item of list.children) {  
  console.log(item.tagName, item.textContent);  
}  
```  
This would log each `<li>` in a `<ul id="menu">` list.

## Putting it Together – Simple DOM Manipulation  
Let’s say we have a list of items and want to highlight one of them:  
```html
<ul id="menu">
  <li>Home</li>
  <li>About</li>
  <li>Contact</li>
</ul>
```  
JavaScript:  
```js  
const menuItems = document.querySelectorAll('#menu li');  
menuItems[1].textContent = "About Us";           // change text of second item  
menuItems[1].classList.add('active');            // add a class to second item  
menuItems[2].style.fontWeight = 'bold';          // make third item bold via style  
```  
This selects all `li` in the menu. Changes the second’s text and gives it a class `active`, and bolds the third. If corresponding CSS existed for `.active` (e.g., underline or different color), that would apply.

---

**Practice:**  
- Create an HTML file with some elements and try selecting them with different methods (`getElementById`, `querySelector`, etc.). Practice changing innerText vs innerHTML to see the difference.  
- Add a few `<img>` tags and use JavaScript to change their `src` or add an `alt`.  
- Create a simple paragraph and use JavaScript to wrap a word in a `<strong>` tag by using `innerHTML` (e.g., turn "hello world" into "hello <strong>world</strong>").  
- Try reading a value from a form input by doing `let val = inputElement.value;` after selecting the input.  

By manipulating the DOM, you make your static HTML interactive and dynamic. The next chapters will introduce events to respond to user actions and more ways to create or remove elements.

# Chapter 13: Handling Events (Event Handlers, Listeners)  
Interactivity on web pages is driven by events — user actions like clicks, key presses, mouse movements, or system-triggered events like page load. In this chapter, we’ll explore how to handle these events in JavaScript via event handlers and event listeners.

## What is an Event?  
An event is a signal that something has happened. Each event has a type (e.g., `"click"`, `"keydown"`, `"submit"`, `"load"`) and typically a target element (the element on which the event occurred). The browser provides an event object to handlers with details about the event (like mouse position, which key was pressed, etc.).

## Event Handler Properties (Old School)  
The simplest way to handle an event on an element is to assign a function to that element’s event property (like `onclick`, `onchange`, etc.).  

**Example – event handler property:**  
```html
<button id="myBtn">Click me</button>
<script>
  const btn = document.getElementById('myBtn');
  btn.onclick = function() {
    alert("Button was clicked!");
  };
</script>
```  
Here we set the `onclick` property of the button element to a function (which shows an alert). When the button is clicked, the browser calls that function.

Alternatively, in HTML you might see attributes like `<button onclick="alert('Hi')">`. That’s an inline HTML event handler. It works, but separating JS from HTML (using addEventListener or setting in script) is cleaner and recommended.

A downside of the property approach: an element can only have one `onclick` property at a time. Setting a new one overwrites the old. This is why **event listeners** (next section) are preferred for flexibility.

## addEventListener (Modern)  
`element.addEventListener(eventType, handlerFunction)` is the standard way to register multiple event listeners You can add many listeners for the same event on the same element, and remove them if needed via `removeEventListener`. 

**Syntax:**  
```js
element.addEventListener('eventType', callbackFunction);
```  
Optionally, a third argument for options like `capture` (for event capturing, default is false), or an object of options (like `{once: true}` to auto-remove after first call, or `{passive: true}` for scroll performance in some cases).

**Example – addEventListener:**  
```js  
btn.addEventListener('click', function(event) {  
  console.log("Clicked!", event);  
});  
```  
This attaches a click listener. When clicked, it logs "Clicked!" and the event object. The `event` object here (often named `e`) has properties like `event.target` (element that was clicked), `event.type` ("click"), etc.

You can add multiple:  
```js  
btn.addEventListener('click', () => console.log("First listener"));  
btn.addEventListener('click', () => console.log("Second listener"));  
```  
Clicking the button will log both messages.

To remove a listener: you need the exact same function reference. Example:  
```js  
function onClick() { console.log('clicked'); }  
btn.addEventListener('click', onClick);  
// later...
btn.removeEventListener('click', onClick);  
```  
If you used an anonymous function in addEventListener, you can’t remove it easily since you don’t have a reference to the exact function object.

## Common Event Types  
- Mouse events: `"click"`, `"dblclick"`, `"mousedown"`, `"mouseup"`, `"mouseenter"`, `"mouseleave"`, `"mousemove"` etc.  
- Keyboard events: `"keydown"`, `"keyup"`, `"keypress"`.  
- Form events: `"submit"` (form submission), `"change"` (input value changed), `"input"` (on text input changes), `"focus"`, `"blur` (when element gains/loses focus).  
- Document events: `"DOMContentLoaded"` (when initial HTML has loaded and parsed), `"load"` (when all resources like images also loaded), `"scroll"`, `"resize"` on window, etc.

**Example – key event:**  
```js  
document.addEventListener('keydown', e => {  
  if(e.key === 'Escape') {  
    console.log('Escape key pressed');  
  }  
});  
```  
Here we listen on the whole document for any keydown. If the key pressed was Escape (identified by `e.key` property), we log something. (Other useful properties: `e.code` for physical key code, `e.keyCode` is old and deprecated better use `e.key` which gives the actual character or key name.)

**Example – form submission:**  
```html
<form id="myForm">
  <input type="text" name="user" />
  <button type="submit">Submit</button>
</form>
<script>
  const myForm = document.getElementById('myForm');
  myForm.addEventListener('submit', function(e) {
    e.preventDefault(); // prevents the form from actually submitting/navigating
    console.log("Form submitted with user:", this.user.value);
  });
</script>
```  
Here on submit, we call `e.preventDefault()` to stop the default action (which would reload the page). Then `this` (or `e.target`) refers to the form, and we can access form fields (e.g., `this.user` because the input name is "user", or `document.querySelector('[name="user"]').value`). We log the input value instead of doing a real submission.

## Event Object and `this`  
Inside an event listener (with `function` syntax), `this` refers to the element the handler is attached to If using an arrow function, `this` retains the outer `this` because arrow functions don’t bind their own `this`. Typically, one can use `e.target` (the element that triggered the event) or `e.currentTarget` (the element the handler is attached to, which is the same as `this` in a non-arrow handler).

**Example:**  
```js  
btn.addEventListener('click', function(e) {  
  console.log(this === e.currentTarget); // true  
  console.log(e.target); // might be btn or a child element if clicked on, e.g., an <span> inside button  
});  
```  
If the user clicked on a child element inside the button, `e.target` would be that child, but `e.currentTarget` (and `this`) would still be the button (because the listener is on the button).

## Inline vs Script  
As mentioned, you can attach events directly in HTML (e.g., `<button onclick="doSomething()">Click</button>`), but this is discouraged for maintainability. It mixes logic with structure. Using script (either external .js or internal `<script>`) to attach events via `addEventListener` is the modern best practice.

## Example: Changing Content on Event  
Let's make an interactive example: say we have a button that when clicked, updates a counter on the page.

HTML:  
```html
<button id="countBtn">Clicked 0 times</button>
```  
JS:  
```js
let count = 0;
const btn = document.getElementById('countBtn');
btn.addEventListener('click', () => {
  count++;
  btn.textContent = `Clicked ${count} times`;
});
```  
Each click increments `count` and updates the button’s text.

## Removing Default Behavior vs Stopping Propagation  
- `event.preventDefault()` stops the browser’s default action for that event (like link navigation, form submit, etc.).  
- `event.stopPropagation()` stops the event from bubbling up to parent elements (useful if you have nested handlers and want to prevent the parent’s from firing in response).  
There’s also `event.stopImmediatePropagation()` which stops other listeners on the same element from firing (less used).

We’ll cover event propagation (bubbling/capturing) more in the next chapter.

---

**Exercises:**  
- Create a button that, when clicked, changes the background color of the page to a random color. (Hint: use `document.body.style.backgroundColor = ...`).  
- Make a simple image gallery: have a few small thumbnail images, and one large image display. When a thumbnail is clicked, set the src of the large image to match the clicked thumbnail. (Practices event target, using attributes).  
- Add an input field and a `<div>` or `<p>` below it. Listen for `"input"` events on the text field and update the `<div>`'s text to show what the user has typed so far in real-time.  
- Try adding two click listeners to the same element using addEventListener to ensure both run. Then use `removeEventListener` to remove one, and test that only the other runs on click.  

Understanding events is key to making web pages interactive. With these basics, you can respond to any user interaction or browser event as needed.

# Chapter 14: Events (Event Propagation and Delegation)  
When an event occurs in the DOM, it doesn’t just trigger on that single element; it goes through a process called **event propagation** that involves three phases: capturing, target, and bubbling Understanding this is important for advanced event handling, including a useful pattern called event delegation.

## Event Propagation Phases  
1. **Capturing phase (capture)**: The event starts at the root of the document and travels down through ancestors to the target element. Listeners can catch the event on the way down if they are registered in capture mode.  
2. **Target phase**: The event arrives at the target element (the element that was actually interacted with). Listeners on the target element fire.  
3. **Bubbling phase**: After the target, the event bubbles back up from the target’s parent to ancestors up to the root, invoking any listeners set to bubble (which is the default mode for addEventListener unless specified otherwise).

By default, `addEventListener('click', handler)` adds a bubbling listener (the third argument defaults to `{capture: false}`). If you want to catch event on capture, you pass `{capture: true}` (or just `true` as third arg, but using an object is clearer).

Most events bubble up, but some do not (for example, `focus` and `blur` do not bubble, but they have capturing equivalents like `focusin/focusout` that do bubble).

**Example – event propagation:**  
Consider HTML:  
```html
<div id="parent" style="padding:20px; background: #eee;">
  Parent
  <button id="child">Child Button</button>
</div>
```  
And JS:  
```js
const parent = document.getElementById('parent');
const childBtn = document.getElementById('child');

parent.addEventListener('click', () => {
  console.log('Parent clicked (bubble)');
});
parent.addEventListener('click', () => {
  console.log('Parent clicked (capture)');
}, true);

childBtn.addEventListener('click', () => {
  console.log('Button clicked');
});
```  
If you click the button:  
- Capture phase: event goes Document -> html -> body -> parent -> child. The parent’s capture listener logs "Parent clicked (capture)" on the way down (before the button’s listener).  
- Target phase: button’s listener logs "Button clicked".  
- Bubbling phase: event goes child -> parent -> body -> html -> Document. The parent’s bubble listener logs "Parent clicked (bubble)" after the button’s.

So the console order would be: capture parent, button, bubble parent.

Usually, you don’t use capture phase much unless needed for specific reasons (like intercepting events early or handling in a generic way).

## Event Bubbling and stopPropagation  
By default, because events bubble, a click on the child also causes a click event on its ancestors. Sometimes this is undesirable. If in the child’s event handler you call `event.stopPropagation()`, it will prevent the event from bubbling further up It stops at that point.

**Example:** If in the above code, inside `childBtn.addEventListener` we did `event.stopPropagation()`, then the parent’s bubble listener wouldn’t fire (though the parent’s capture listener would have already fired on the way down in capture phase).

Similarly, a parent could call `event.stopPropagation()` in a listener to stop it from going further up (maybe to stop a very general handler on `document` from running).

## Event Delegation  
**Event delegation** is a pattern where instead of adding individual event listeners to many child elements, you add one listener to a common ancestor and use the event’s bubbling to catch events from those children Then you determine which child triggered the event using `event.target` or similar.

This is useful for dynamic content (items added later still get handled) and for performance (one listener instead of potentially hundreds).

**Example – without delegation:** If you have 100 list items and want to handle clicks on each, you might attach 100 separate listeners. With delegation, you attach one listener on the `<ul>` and check what was clicked.

**Example – event delegation:**  
```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
  <!-- could be more or added later -->
</ul>
<script>
  const list = document.getElementById('list');
  list.addEventListener('click', function(e) {
    if(e.target.tagName === 'LI') {
      console.log('You clicked', e.target.textContent);
      e.target.style.backgroundColor = 'yellow';
    }
  });
</script>
```  
Here, we listen on the `<ul>`. When any `<li>` inside is clicked, the event bubbles up to `<ul>`. In the handler, `e.target` will be the actual clicked element. We check if it’s an `LI` (to ensure it’s not the UL itself or something else). If yes, we handle accordingly (e.g., highlight it, or do some action based on text or a data attribute).

This way, you can add or remove `<li>` items dynamically and the UL’s single listener still handles clicks for them without needing to attach new handlers.

One caveat: If the `<li>` contains inner elements (like a link or a button), `e.target` might be that inner element. Sometimes you might use `e.currentTarget` or other logic to find the closest desired ancestor. A useful method is `e.target.closest('li')` which returns the nearest `<li>` up the chain (including itself if it’s an li). That helps ensure you have the list item element.

**Example with closest:**  
```js
list.addEventListener('click', function(e) {
  const li = e.target.closest('li');
  if(li && list.contains(li)) {
    // li is the <li> that was clicked (or whose child was clicked)
    console.log('Clicked LI:', li.textContent);
  }
});
```  
We also ensure `list.contains(li)` to confirm the found li is actually within the list (so that clicking somewhere else in the list not on an li doesn’t give a false positive).

## Stopping Propagation vs PreventDefault  
Just to re-iterate:  
- `e.stopPropagation()` stops event from bubbling further. Useful in delegation when an inner element’s event is being handled and you don’t want parent’s handler to also fire for it (if parent’s logic would conflict).  
- `e.preventDefault()` stops the default browser action (like navigating on a link, submitting a form, etc.).  

They are different. Often you might call both in some cases (like stopping a link from navigating and also not letting its click bubble if needed).

## summary of propagation  
To summarize propagation: an event on a child goes up to ancestors. If multiple listeners, capture ones fire first (top-down), then target, then bubble ones (bottom-up). Without calling stopPropagation, it will bubble all the way to top (window or document). This is often fine, but it also means if you have multiple nested listeners for the same event type, they will all run unless you intervene.

## Real example: Modal dialog with delegation  
Imagine a common scenario: you have a modal dialog overlay with a backdrop. Clicking the backdrop should close the modal, but clicking inside the modal content area should not.

HTML:  
```html
<div id="modal" class="modal">
  <div class="modal-content">
    <p>Modal stuff</p>
    <button id="closeBtn">Close</button>
  </div>
</div>
```  
CSS: `.modal { /* covers page */ } .modal-content { /* inner dialog */ }`.

JS:  
```js
const modal = document.getElementById('modal');
const closeBtn = document.getElementById('closeBtn');

closeBtn.addEventListener('click', hideModal);
modal.addEventListener('click', function(e) {
  if(e.target === modal) { // click directly on backdrop
    hideModal();
  }
});
function hideModal() {
  modal.style.display = 'none';
}
```  
This uses delegation-like behavior: The modal covers entire screen; we attach a click to it that if the backdrop itself (modal div) was clicked (and not the content inside), we close it. We check `if(e.target === modal)` – meaning the click target was the modal itself, not a child. If you clicked the inner content, that event bubbles to modal, but then e.target would be the inner element, not equal to modal, so we do nothing (allowing the close button to be handled separately or to do nothing if just clicking content).

Alternatively, we could attach an event to the backdrop layer separate from content. But in cases where elements are generated or numerous, delegation is cleaner.

## Summary  
- Bubbling allows one handler on a parent to handle events from many children (delegation).  
- Bubbling can cause multiple handlers to fire if not managed (sometimes that’s intended, sometimes not).  
- You can stop bubbling when needed.  
- Event delegation is a powerful pattern to simplify event management especially in lists, tables, or any container with multiple similar items.

---

**Exercises:**  
- Use event delegation on a UL to implement a to-do list: clicking an LI toggles a 'done' class on it (e.g., cross it out). New LIs added via an input should also respond without adding new listeners.  
- Create nested elements (like a button inside a div inside another div). Attach click listeners to each level that log something. Click the innermost and observe order (to ensure understanding of capture vs bubble). Then try adding `{capture:true}` to one of them to see how order changes.  
- For practice with preventDefault vs stopPropagation: Place a link inside a div. Add a click listener on the div that alerts "div clicked", and one on the link that does `e.preventDefault()` and alerts "link clicked". See what happens on clicking the link (the div handler still runs because we prevented default but didn't stop propagation). Then modify the link handler to also `e.stopPropagation()` and see the difference (div no longer alerts).  

Mastering propagation and delegation will let you design more efficient event handling and avoid common pitfalls when you have complex nested elements.

# Chapter 15: Creating and Deleting Elements  
Beyond modifying existing DOM elements, often we need to create new elements or remove elements dynamically (e.g., adding new items to a list, or removing a notification message). This chapter covers how to create, insert, and remove DOM nodes using JavaScript.

## Creating New Elements  
To create a new element, use `document.createElement(tagName)` This creates a DOM element in memory (not yet in the document). You can then set its properties (like textContent, class, etc.), and finally append it to the desired parent in the DOM tree.

**Example – create and append:**  
```js  
const newPara = document.createElement('p');  
newPara.textContent = "This is a new paragraph.";  
newPara.classList.add('message');  
document.body.appendChild(newPara);  
```  
This makes a `<p class="message">This is a new paragraph.</p>` and appends it to the end of the `<body>`.

If you want to add text or other nodes, you can also create text nodes explicitly with `document.createTextNode("text")`, but usually setting textContent is easier. However, `createTextNode` is useful if you need to insert text into a certain position among other HTML without using innerHTML (for security or structure reasons).

**Example – create with createTextNode:**  
```js  
const textNode = document.createTextNode('Hello World');  
const h1 = document.createElement('h1');  
h1.appendChild(textNode);  
document.body.appendChild(h1);  
```  
That does the same as setting textContent on h1 in effect.

## Appending vs Prepending vs Inserting  
- `parent.appendChild(newElement)` adds as the last child inside `parent`  
- `parent.prepend(newElement)` (a newer method) adds as the first child.  
- `parent.insertBefore(newElement, referenceElement)` inserts `newElement` before `referenceElement` (which should be an existing child of parent) Use `null` as second argument to mimic appendChild (since before `null` means end).  
- `parent.insertAdjacentHTML(position, htmlString)` is a quick way to insert HTML relative to parent. `position` can be `"beforebegin"`, `"afterbegin"`, `"beforeend"`, `"afterend"` – these refer to positions relative to the element: outside before it, inside at start, inside at end, outside after it. (This can be easier than createElement if inserting known HTML snippet directly, but careful with content trust).  
- `element.after(newNode)` and `element.before(newNode)` can insert siblings relative to an element (newer DOM methods).  
- `element.replaceWith(newNode)` can replace an element with another.

**Example – insertBefore:**  
```js  
const list = document.getElementById('todoList');  
const newItem = document.createElement('li');  
newItem.textContent = 'New Task';  
const firstItem = list.firstElementChild;  
list.insertBefore(newItem, firstItem);  // newItem becomes the new first child  
```  

**Example – insertAdjacentHTML:**  
```js  
const container = document.getElementById('container');  
container.insertAdjacentHTML('beforeend', '<div class="notice">Hello</div>');  
```  
This will append the given HTML string as HTML inside the container at the end.

## Removing Elements  
To remove an element, you typically call `parent.removeChild(element)`or use the newer `element.remove()` method.

**Example – removeChild:**  
```js  
const item = document.getElementById('oldItem');  
item.parentNode.removeChild(item);  
```  
This finds an element with id "oldItem" and removes it from its parent node.

**Example – element.remove():**  
```js  
document.getElementById('oldItem').remove();  
```  
This is succinct (supported in modern browsers, IE9+ with a polyfill required for older IE).

Keep in mind removing an element also removes its children from the DOM (they will be freed for garbage collection if no JS references).

If you want to empty an element’s contents, you can remove its children in a loop or set `element.innerHTML = ''` to clear it out.

## Cloning Elements  
Sometimes you may want to duplicate a node: `element.cloneNode()` creates a copy. If you pass `true` to `cloneNode(true)`, it performs a deep clone (including all descendants). Without arguments or false, it clones only the element itself (shallow clone, no children). This can be useful for templates.

Example:  
```js  
let original = document.getElementById('templateItem');  
let copy = original.cloneNode(true);  
copy.id = ''; // adjust id or remove it since ID should be unique  
document.body.appendChild(copy);  
```  

## Building DOM Fragment Example  
Suppose you want to add a list of items dynamically (like from an array of data). Doing `appendChild` in a loop can be fine, but if the list is big, sometimes using a **DocumentFragment** can be a little more efficient (a DocumentFragment is like a lightweight container of DOM nodes that isn’t part of the main DOM tree, so appending multiple elements to it doesn’t cause multiple reflows or repaints; you then append the fragment once to the DOM).

**Example – using DocumentFragment:**  
```js  
const items = ["One", "Two", "Three"];  
const list = document.createElement('ul');  
const frag = document.createDocumentFragment();  
items.forEach(text => {  
  let li = document.createElement('li');  
  li.textContent = text;  
  frag.appendChild(li);  
});  
list.appendChild(frag); // appends all li's at once from the fragment  
document.body.appendChild(list);  
```  
Using fragment is optional; modern browsers are quite fast with DOM, but it’s good to know.

## Putting it Together  
Let’s say we have a form where user enters a new task name, and we want to add it to a list on submit.

HTML:  
```html
<input type="text" id="taskInput" />
<button id="addTaskBtn">Add Task</button>
<ul id="tasks"></ul>
```  
JS:  
```js
const input = document.getElementById('taskInput');
const btn = document.getElementById('addTaskBtn');
const taskList = document.getElementById('tasks');

btn.addEventListener('click', () => {
  const text = input.value.trim();
  if(text !== "") {
    const li = document.createElement('li');
    li.textContent = text;
    // could also add a delete button here within li if wanted
    taskList.appendChild(li);
    input.value = ""; // clear input
  }
});
```  
Now each time the button is clicked (or if we wanted to handle enter key in input by capturing 'keydown'), it creates a new `li` with the input text and appends to the UL.

To remove tasks, maybe we could attach an event listener on the list (event delegation from previous chapter) to handle clicking on an LI to remove it:

```js
taskList.addEventListener('click', e => {
  if(e.target.tagName === 'LI') {
    e.target.remove();
  }
});
```  

---

**Exercises:**  
- Write a script to add 5 new list items to an existing UL with id "myList". Each item text could be "Item X". Use a loop and createElement/appendChild.  
- Create a simple image gallery: have an array of image URLs, create an `<img>` element for each and append to a container div. Ensure you set some attributes like `alt` and maybe a common class for styling.  
- Implement a "Remove" button: dynamically create a button element that, when clicked, removes itself from the DOM. (This can be done by adding a click listener to the button that calls `button.remove()`.)  
- Use `insertBefore` to insert a new item at the top of a list instead of bottom, as an exercise.  
- Try cloning an element: perhaps clone a form input or a card and append the clone to test that cloneNode is working as you expect (and see that events are not copied by cloneNode by default — event listeners have to be reattached if needed).  

Understanding how to create and remove elements gives you control to build DOM structures on the fly and update the page dynamically in response to program logic or user interactions.

# Chapter 16: Forms in JS  
Handling forms is a common task: reading user input, validating it, and possibly providing feedback or sending it to a server. JavaScript can intercept form submissions, validate fields, and manipulate form controls. In this chapter, we'll cover form elements and how to work with them through the DOM.

## Accessing Form Elements  
Form elements (inputs, selects, textareas, etc.) can be accessed like any other element via DOM selectors. Additionally, the form element has a property that references its elements by name: e.g., `document.forms.myFormName.elements.fieldName`. But using `getElementById` or `querySelector` is straightforward and often clearer.

Common form elements:  
- `<input>` (types: text, checkbox, radio, etc.)  
- `<textarea>`  
- `<select>` (and its `<option>` children)  
- `<button>` or `<input type="submit">`  

Key properties:  
- `input.value` – the string value of text, number, password, etc., input. For checkboxes/radios, `value` is the value attribute (not the checked state), and `checked` property is a boolean for whether it's selected.  
- `textarea.value` – the text inside.  
- `select.value` – value of the selected option (or use `select.options` collection or `select.selectedIndex` to dive deeper).  
- `input.checked` – boolean if checkbox/radio is checked.  
- `input.files` – for file inputs, the selected FileList.  
- `form.elements` – a collection of form controls inside a form (also accessible by name or index).  

**Example – reading values:**  
```html
<form id="loginForm">
  <input type="text" name="username" id="username" />
  <input type="password" name="password" id="password" />
  <button type="submit">Login</button>
</form>
<script>
  const form = document.getElementById('loginForm');
  form.addEventListener('submit', function(e) {
    e.preventDefault();
    const usernameVal = document.getElementById('username').value;
    const passwordVal = document.getElementById('password').value;
    console.log("Username:", usernameVal, "Password:", passwordVal);
    // here you might validate or send data via AJAX
  });
</script>
```  
We prevented the default so the form doesn't actually submit to a server, and then we read values and possibly handle them with JS.

## Form Events  
- `submit` event on a form triggers when the form is about to submit (either by clicking a submit button or pressing Enter in a text field). We often intercept it to do validation.  
- `input` event on text fields triggers on every change (every keypress that changes the value).  
- `change` event triggers when an input loses focus after its value was changed, or for select when a new option selected, or for checkboxes when toggled.  
- `focus` and `blur` events when an element gains or loses focus (these do not bubble, but `focusin` and `focusout` do bubble).  

Example:  
```js
const emailField = document.querySelector('input[type=email]');
emailField.addEventListener('input', () => {
  // maybe show/hide a "invalid email" message as they type
});
emailField.addEventListener('blur', () => {
  // validate when they leave the field
});
```

## Form Validation  
You can manually check values and display messages. E.g., check if a field is empty, if an email contains "@" etc., if a password meets criteria. If invalid, you might: 
- Show an error message (possibly in a span near the field). 
- Prevent form submission (by `event.preventDefault()` in submit handler). 
- You can also use the HTML5 constraint validation API or attributes like `required`, `pattern`, `minlength`, etc. The browser can show built-in messages or you can use `input.setCustomValidity("message")` to set a validation message. Calling `form.reportValidity()` can trigger the browser’s validation UI.

Basic manual validation example:  
```js
form.addEventListener('submit', function(e) {
  const email = emailField.value.trim();
  if(email === "" || !email.includes('@')) {
    e.preventDefault();
    alert("Please enter a valid email.");
  }
});
```  

## Submitting Form Data (AJAX)  
Although not directly about forms DOM, typically after validating, you might want to send the data via fetch (AJAX) rather than a full page reload. You can gather data from form elements and use `fetch` or other means to send to server in background.

Example snippet using fetch (assuming there's an endpoint to handle the data):  
```js
form.addEventListener('submit', function(e) {
  e.preventDefault();
  const formData = new FormData(form); // collects form fields
  fetch('/login', {
    method: 'POST',
    body: formData
  }).then(response => {
    // handle response
  });
});
```  
Here FormData is a convenient API that grabs all form fields by name and formats for submission (like multipart/form-data or application/x-www-form-urlencoded depending on usage). If using JSON, you might do:  
```js
const data = { 
  user: usernameVal, 
  pass: passwordVal 
};
fetch('/login', {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify(data)
});
```  
(This goes more into AJAX, which is coming in Chapter 34, but it's good to see context.)

## Interacting with Form Controls  
You can dynamically change forms: add options to a select, check a box, etc. For example, to check a checkbox via JS: `checkboxElement.checked = true;`. To select an option: `selectElement.value = "someValue";` or find the option and set its `selected` property true.

If you have radio inputs with same name, setting one’s checked = true will mark it and typically uncheck the others (the browser enforces only one radio of same name is checked).

**Example – dynamically adding an option:**  
```js
const countrySelect = document.getElementById('country');
let opt = document.createElement('option');
opt.value = "new";
opt.textContent = "New Country";
countrySelect.appendChild(opt);
```  

## Preventing Enter key default  
One nuance: pressing Enter in a single text input form might trigger submit. If you want to prevent that (maybe you have an explicit button), you can capture keydown on that input and if `e.key === "Enter"` do `e.preventDefault()` to stop form from submitting.

**Example:**  
```js
document.getElementById('myField').addEventListener('keydown', e => {
  if(e.key === 'Enter') {
    e.preventDefault();
    // maybe trigger something else or just prevent submission
  }
});
```  

## Example: Signup Form Validation  
Consider a simple signup form: username, email, password, confirm password. We want to validate: all filled, email looks like email, password and confirm match, maybe password length >= 6.

Pseudo-code:  
```js
form.addEventListener('submit', e => {
  let valid = true;
  if(username.value.trim() === "") {
    showError(username, "Username required");
    valid = false;
  }
  if(!email.value.includes('@')) {
    showError(email, "Email invalid");
    valid = false;
  }
  if(password.value.length < 6) {
    showError(password, "Password too short");
    valid = false;
  }
  if(password.value !== confirmPass.value) {
    showError(confirmPass, "Passwords do not match");
    valid = false;
  }
  if(!valid) {
    e.preventDefault(); // stop submission
  }
});
```  
We assume showError is a function that maybe adds a small error text or highlights the field. If everything is valid, the form can proceed (or you can send via AJAX).

## Resetting Form  
`form.reset()` will reset all fields to their initial values (clears them if they had none). Useful for after a successful submission to clear inputs.

---

**Exercises:**  
- Create a form with a text input for a phone number. When the user leaves the field (blur event), check if it’s 10 digits; if not, display a message below the field (you can create a small span or div for the message).  
- Make a form with a group of checkboxes (like interests or options) and a "Select All" checkbox. Use an event such that clicking "Select All" sets all the other checkboxes to checked or unchecked accordingly.  
- Implement a character counter: a textarea that shows "X characters remaining" (for a max length) as the user types (use input event). If over some limit (you can enforce with `maxlength` attribute or just visual warning), display in red or something.  
- Experiment with the constraint validation API: Try adding `required` attribute to an input and see how `form.reportValidity()` works (it will show the default tooltip). Then try using `input.setCustomValidity("Your custom message")` on some condition and `form.reportValidity()`.  

Working with forms ties together many of the earlier topics: DOM selection/manipulation, events, and user input handling. With these tools, you can create interactive forms that validate and respond in real-time, improving user experience.

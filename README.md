<!-- [Javascript](#javascript "Goto Javascript") -->
<!-- [Node.js](#Node.js "Goto Node.js") -->

# Javascript

### Q : What is js?
A : JavaScript is a programming language commonly used in web development. It was originally developed by Netscape as a means to add dynamic and interactive elements to websites.

JavaScript is a synchronous, blocking, single-threaded language.
JavaScript is a dynamically typed language. In a dynamically typed language, the type of a variable is checked during run-time in contrast to statically typed language, where the type of a variable is checked during compile-time.

# 1. **"JavaScript is a synchronous, blocking, single-threaded language."**
   - **Correct but requires clarification:**
     - JavaScript is **single-threaded**, meaning it has a single call stack, and only one piece of code is executed at a time.
     - By default, JavaScript executes code **synchronously** (one line after another).
     - However, JavaScript is **non-blocking** in practice due to its event loop and asynchronous features, such as `setTimeout`, Promises, and `async/await`. These allow JavaScript to handle tasks asynchronously without blocking the main thread.

## 2. **"JavaScript is a dynamically typed language."**
   - **Correct:**
     - In JavaScript, variables do not have a fixed type. The type of a variable is determined at runtime, and you can reassign variables to values of different types.

     ```javascript
     let x = 5; // x is a number
     x = "hello"; // x is now a string
     ```

## 3. **"In a dynamically typed language, the type of a variable is checked during run-time in contrast to statically typed language, where the type of a variable is checked during compile-time."**
   - **Correct:**
     - This is an accurate description of the difference between dynamically typed and statically typed languages.
     - Example of dynamically typed behavior in JavaScript:
       ```javascript
       let num = 10;
       num = "ten"; // No error, type changes at runtime
       ```

     - Example of statically typed behavior in TypeScript (a superset of JavaScript):
       ```typescript
       let num: number = 10;
       num = "ten"; // Error: Type 'string' is not assignable to type 'number'
       ```

### Final Assessment:
The statements are **mostly correct** but could be better worded for clarity:
1. JavaScript is **single-threaded** and executes code synchronously by default, but it is **non-blocking** due to its asynchronous features like the event loop.
2. JavaScript is a **dynamically typed language**, where variable types are determined at runtime.
3. The distinction between dynamically and statically typed languages is accurately described.

### Q : Why JS behaves async while api call and ajax?
A : JavaScript is single-threaded, meaning it can only execute one piece of code at a time. However, JavaScript also supports asynchronous programming through mechanisms like callbacks, promises, and async/await.

When you make an AJAX (Asynchronous JavaScript and XML) call in JavaScript, it typically doesn't block the execution of the rest of your code. Instead, it initiates a network request and continues executing the subsequent lines of code without waiting for the response from the server.

Here's how it typically works:

1. You initiate an AJAX request using functions like `XMLHttpRequest` or the more modern `fetch` API.
2. The AJAX request is sent to the server.
3. While waiting for the server's response, your JavaScript code continues executing.
4. When the response is received from the server, a callback function (or a `.then()` handler in the case of promises) is triggered to handle the response data.
5. Your code inside the callback function (or `.then()` handler) is then executed, allowing you to process the response data or perform other tasks.

This asynchronous behavior is essential for web applications because it allows them to perform tasks like fetching data from servers without blocking the user interface (UI) or making the application unresponsive.

It's important to handle asynchronous operations properly in JavaScript to avoid issues like race conditions, callback hell, and ensuring that dependent operations are executed in the correct order. This is where constructs like promises, async/await, and callback functions come into play to manage asynchronous code in a more organized and readable way.

### Q : What are the different data types present in javascript?
A : There are two types of data types in JavaScript.
~~~
 1. Primitive data type // It holds single value
 2. Non-primitive (reference) data type

 JavaScript primitive data types : 
    String, Number, Boolean, Undefined, Null

 JavaScript non-primitive data types : 
    Object, Array, RegExp
~~~
The difference between primitives and non-primitives is that primitives are immutable and non-primitives are mutable.

Non primitive values can also be referred to as reference types because they are being compared by reference instead of value. Two objects are only strictly equal if they refer to the same underlying object.

### Q : What is mutable and immutable data types in javascript?
A : Image result for what is mutable and immutable data types in javascript Mutable objects are objects whose value can change once created, while immutable objects are those whose value cannot change once created. 

Primitives are known as being immutable data types because there is no way to change a primitive value once it gets created.
~~~
var myString = "Helllooo"

console.log('myString[2]', myString[2]);

myString[2] = 'c'

console.log(myString);

==> result : myString[2] l
             Helllooo

As u can see value of string does not changed to Hecllooo cause string is immutable
~~~
On the other hand Non-primitives are known as being mutable data types like Arrays and Objects.
~~~
var x = {
    foo: 'bar'
};
var  y = x;
x.foo = 'Something else';
console.log(y.foo); // Something else
console.log(x === y) // true

As you can see, x is a mutable object, and any change in the property of x gets reflected in the value of y.
They all share the same reference. So, when you update the value of a property of x, you’re modifying 
the value for all the references to that object.
~~~

### Q : Difference between "==" and "===" 
A : == compares value and === compares vlue and type
== convert type of right side to type of left and then compare

=== is faster than ==

### Q : Difference between null and undefined
A : both of them is an empty value but difference is that when you define a variable and not assign any value it automatically so you don't have to assign value undefine js do it for you. In case of null you have to assugn value null to variable. Typeof undefined will be undefined while typeof null will be object.

### Q : What is scope in javascript
A : Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.

### Q : What is a strict mode in javascript
A : Strict Mode is a new feature in ECMAScript 5 that allows you to place a program, or a function, in a “strict” operating context. This way it prevents certain actions from being taken and throws more exceptions. The literal expression "use strict"; instructs the browser to use the javascript code in the Strict mode.

### Q : What are the possible ways to create objects in JavaScript
A : 
1. Object constructor:
```var object = new Object();```

2. Object's create method:
```var object = Object.create(null);```

3. Object literal syntax:
```
var object = {
     name: "Sudheer"
     age: 34
};
```

4. Function constructor:
```
function Person(name) {
  this.name = name;
  this.age = 21;
}
var object = new Person("Sudheer");
```

5. Function constructor with prototype:
```
function Person() {}
Person.prototype.name = "Sudheer";
var object = new Person();
```

6. ES6 Class syntax
```
class Person {
  constructor(name) {
    this.name = name;
  }
}

var object = new Person("Sudheer");
``` 

### Q : what is the diff between deep cloning and shallow cloning
A : 
* In Shallow copy, a copy of the original object is stored and only the reference address is finally copied. In Deep copy, the copy of the original object and the repetitive copies both are stored.
* A deep copying means that value of the new variable is disconnected from the original variable while a shallow copy means that some values are still connected to the original variable.

For Shallow cloning

```
let originalObject = { a: 1, b: { c: 2 } };
let shallowClone = Object.assign({}, originalObject);

and

//Spread Operator
let originalObject = { a: 1, b: { c: 2 } };
let shallowClone = { ...originalObject };
```

For Deep clone use lodash lobrary
```const _ = require('lodash');

let originalObject = { a: 1, b: { c: 2 } };
let deepClone = _.cloneDeep(originalObject);
```
* Deep cloning creates a new object and recursively copies all nested objects, ensuring that the new object is completely independent of the original object. There are several ways to perform deep cloning, but one common approach is to use a library like lodash or implement a custom deep cloning function.
* This method works for simple JSON-serializable objects but has limitations with handling certain types like functions and circular references.Keep in mind that the JSON method may not be suitable for all cases, especially if the object contains functions, non-JSON-safe values, or circular references.
```
const a = { x: 20, date: new Date() };
const b = structuredClone(a); 
```

### Q : call, apply and bind in JavaScript
A : 
```
var obj = {
 num: 2
}

var add = function(a,b,c){
 return this.num + a + b + c
}

add.call(obj, 1,2,3)
add.apply(obj, [1,2,3])
var bound = add.bind(obj)
bound(1,2,3)
```

* call method invokes the function with 1st argument as context object and further comma separated arguments which the function can directly consume.
* apply is exactly same as call method, the only difference is it takes the 2nd argument as array list of the parameters.
* bind method is similar to the call method but it does not invokes the function, rather gives you the copy of exactly same function, which can be invoked later.

where it's used

 apply() when you want to invoke the function immediately, and modify the context. Call/apply call the function immediately, whereas bind returns a function that, when later executed, will have the correct context set for calling the original function.

The call, bind and apply methods can be used to set the this keyword independent of how a function is called. The bind method creates a copy of the function and sets the this keyword, while the call and apply methods sets the this keyword and calls the function immediately.


### Q : Difference between "var", "let" and "const"
A : 
* var declarations are globally scoped or function/locally scoped or function scoped while let and const are block scoped.
* var variables can be updated and re-declared within its scope; let variables can be updated but not re-declared; const variables can neither be updated nor re-declared.
* They are all hoisted to the top of their scope. But while var variables are initialized with undefined, let and const variables are not initialized.
* While var and let can be declared without being initialized, const must be initialized during declaration.
* var can be accessed without initialization as its default value is “undefined”.	let cannot be accessed without initialization, as it returns an error. const cannot be accessed without initialization, as it cannot be declared without initialization.

var variables can be re-declared and updated : 
 ```javascript
      var a = 1;
      var a = 2; 
        OR
      var a = 1;
      a = 2;
--------------------
  function newFunction() {
  if(true){
          var a = "hello";
      }
  console.log(a);
  }
result will be => hello
--------------------
console.log(a);
      var a = 1;
 this code will interpreted as 
    var a;
    console.log(a); // a is undefined
    a = 1;
```

let has a block scope
```javascript
  function newFunction() {
  if(true){
          let a = "hello";
      }
  console.log(a);
  }
result will be => VM250:5 Uncaught ReferenceError: a is not defined
```

### Q : To prevent changing the value of a.b, you can use Object.freeze().
A : In this example, attempting to change the value of a.b to 3 will have no effect because the object a has been frozen. As a result, a.b remains 1 and cannot be modified. However, please note that Object.freeze() only provides shallow immutability, meaning it only freezes the top-level properties of an object. If a had nested objects, those nested objects would still be mutable unless they are also frozen.

```
const a = Object.freeze({ b: 1 });

// Attempt to change a.b
a.b = 3;

console.log(a.b); // Output: 1 (unchanged)
```

### Q : JS array method and interview questions
A : 
* The pop() method removes the last element from an array. The pop() method returns the value that was "popped out". The push() method adds a new element to an array (at the end).The push() method returns the new array length.

```
let dailyActivities = ['work', 'eat', 'sleep', 'exercise'];
dailyActivities.pop();
console.log(dailyActivities); // ['work', 'eat', 'sleep']
```

* The shift() method removes the first array element and "shifts" all other elements to a lower index.The shift() method returns the value that was "shifted out".
```
let dailyActivities = ['work', 'eat', 'sleep'];
dailyActivities.shift();
console.log(dailyActivities); // ['eat', 'sleep']
```

* The unshift() method adds a new element to an array (at the beginning), and "unshifts" older elements.The unshift() method returns the new array length.
```
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.unshift("Lemon", "Pineapple"); // [Lemon,Pineapple,Banana,Orange,Apple,Mango]
```

* The concat() method creates a new array by merging (concatenating) existing arrays, The concat() method does not change the existing arrays. It always returns a new array.The concat() method can take any number of array arguments.

* Splicing and Slicing Arrays : The splice() method can be used to add new items to an array

```
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
```

* check if it is array
```
const fruits = ["Banana", "Orange", "Apple", "Mango"];
let result =  Array.isArray(fruits); //true
``` 

* Interview question 
```
const arr = ['A', 'N', 'U'];
arr[10] = 10;
console.log(arr.length); //outout 11

let array = [1, 2, 3, 4, 5];
array.length = 0;
console.log(array) //[]

const getUniqueValues = (arr) => [...new Set(arr)]; //get all unique element array

let arr1 = [10, 12, 3.1];
let arr2 = [10, 12, 3.1];
console.log(arr1 == arr2); //false
```

### Q : Map, Filter and Reduce
A : 
* Map
The map() method is used for creating a new array from an existing one, applying a function to each one of the elements of the first array.

```
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(item => item * 2);
console.log(doubled); // [2, 4, 6, 8]
```

* Filter
The filter() method takes each element in an array and it applies a conditional statement against it. If this conditional returns true, the element gets pushed to the output array. If the condition returns false, the element does not get pushed to the output array.

```
const numbers = [1, 2, 3, 4];
const evens = numbers.filter(item => item % 2 === 0);
console.log(evens); // [2, 4]
```

* Reduce
The reduce() method reduces an array of values down to just one value. To get the output value, it runs a reducer function on each element of the array.

```
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((result, item) => {
  return result + item;
}, 0);
console.log(sum); // 10
```

### Q : Different Types of Loops in JavaScript
A : 
* while — loops through a block of code as long as the condition specified evaluates to true.
```
while (i < 10) {
  text += "The number is " + i;
  i++;
}
```

* do…while — loops through a block of code once; then the condition is evaluated. If the condition is true, the statement is repeated as long as the specified condition is true.
```
do {
  text += "The number is " + i;
  i++;
}
while (i < 10);
```

* for — loops through a block of code until the counter reaches a specified number.
```
for (let i = 0; i < cars.length; i++) {
  text += cars[i] + "<br>";
}
```

* for…in — loops through the properties of an object.
```
for (key in object) {
  // code block to be executed
}
```

* for…of — loops over iterable objects such as arrays, strings, etc.
```
let text = "";
for (let x of cars) {
  text += x;
}
```

### Q : What is event bubbling and capturing?
A : Event flow is the order in which event is received on the web page. When you click an element that is nested in various other elements, before your click actually reaches its destination, or target element, it must trigger the click event for each of its parent elements first, starting at the top with the global window object. There are two ways of event flow

Top to Bottom(Event Capturing)
Bottom to Top (Event Bubbling)

* Event bubbling is a type of event propagation where the event first triggers on the innermost target element, and then successively triggers on the ancestors (parents) of the target element in the same nesting hierarchy till it reaches the outermost DOM element.

* Event capturing is a type of event propagation where the event is first captured by the outermost element, and then successively triggers on the descendants (children) of the target element in the same nesting hierarchy till it reaches the innermost DOM element.

### Q : What is ECMA Script and How are JavaScript and ECMA Script related?
ECMA Script are like rules and guideline while Javascript is a scripting language used for web development.

### Q : What are some of the features of ES6?
A : 
* Support for constants (also known as “immutable variables”)
* Block-Scope support for both variables, constants, functions
* Arrow functions
* Extended Parameter Handling
* Template Literals and Extended Literals
* Spread operator
* Destructuring Assignment

### Q : What is use of arrow 
A : arrow functions were introduced in ES6.
* An arrow function is a shorter syntax for a function expression and does not have its own this, arguments, super, or new.target. These functions are best suited for non-method functions, and they cannot be used as constructors.
* Arrow functions do not bind their own this value. Instead, they inherit the this value from the enclosing scope. This behavior can be advantageous in certain situations, especially when dealing with callbacks or functions inside other functions.
* Unlike regular functions, arrow functions do not have their own this. The value of this inside an arrow function remains the same throughout the lifecycle of the function and is always bound to the value of this in the closest non-arrow parent function.
* In short, with arrow functions there are no binding of this.
* In regular functions the this keyword represented the object that called the function, which could be the window, the document, a button or whatever.
```javascript
let add = (x, y) => x + y;
--------------------------
let me = { 
 value: 1, 
 thisInArrow:() => { 
 console.log(this.value); // no 'this' binding here 
 }, 
 thisInRegular(){ 
 console.log(this.value); // 'this' binding works here 
 } 
};
me.thisInArrow(); 
me.thisInRegular();
==> result : undefined
             1
```

### Q : What is the rest parameter and spread operator?
A : Both rest parameter and spread operator were introduced in the ES6 version of javascript.

* Rest parameter ( … )

The rest parameter allows a function to accept an indefinite number of arguments as an array.

In the sum function, the ...numbers syntax allows it to accept any number of arguments, which are then treated as an array called numbers. This array can be processed using array methods like reduce in this example.
```
// Rest parameter in function declaration
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

// Using the function with different numbers of arguments
console.log(sum(1, 2, 3));         // Output: 6
console.log(sum(4, 5, 6, 7));      // Output: 22
console.log(sum(10));              // Output: 10
```

* Spread operator (…)

The spread operator spreads the elements of an array (or characters of a string) or the properties of an object into another array, object, or function call.

The spread operator (…) allows us to expand an iterable like array into its individual elements.

```
// Spread operator in array
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5, 6];

console.log(arr2);  // Output: [1, 2, 3, 4, 5, 6]

// Spread operator in function call
const numbers = [10, 20, 30];
console.log(Math.max(...numbers));  // Output: 30
```

### Q : What is Object Destructuring?

A : Object destructuring is a new way to extract elements from an object or an array.

```
const classDetails = {
  strength: 78,
  benches: 39,
  blackBoard:1
}

const {strength:classStrength, benches:classBenches,blackBoard:classBlackBoard} = classDetails;

console.log(classStrength); // Outputs 78
console.log(classBenches); // Outputs 39
console.log(classBlackBoard); // Outputs 1
```

### Q : Explain “this” keyword
A : The “this” keyword refers to the object that the function is a property of.
The value of “this” keyword will always depend on the object that is invoking the function.

```
var obj = {
    name:  "vivek",
    getName: function(){
    console.log(this.name);
  }
}
        
obj.getName();
```

### Q : What would be the result of 3+2+"7"?
A : Since 3 and 2 are integers, they will be added numerically. And since 7 is a string, its concatenation will be done. So the result would be 57.

### Q : What is type of null and function?
A : type of null is "object" and type of function is "function".

### Q : What is closure and counter dillema?
A : We can create nested functions in JavaScript. Inner function can access variables and parameters of an outer function (however, cannot access arguments object of outer function).
A JavaScript closure is when an inner function has access to its outer enclosing function's variables and properties. like bwlow example.

A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains

* Own scope where variables defined between its curly brackets
* Outer function’s variables
* Global variables

Closures help in maintaining the state between function calls without using a global variable.

Closures are frequently used in JavaScript for object data privacy, in event handlers and callback functions, and in partial applications, currying, and other functional programming patterns
```
javascript
function OuterFunction() {

    var outerVariable = 1;

    function InnerFunction() {
        console.log(outerVariable);
    }

    InnerFunction();
    //or
    // return InnerFunction
}
OuterFunction()
//or
//OuterFunction()();
```
### Q : What is currying in JavaScript?
A : Currying is an advanced technique to transform a function of arguments n, to n functions of one or less arguments.
```javascript
function add (a) {
  return function(b){
    return a + b;
  }
}

add(3)(4) ==> 7
```
### Q : What are object prototypes?
A : All javascript objects inherit properties from a prototype.

For example,
Date objects inherit properties from the Date prototype

Math objects inherit properties from the Math prototype

Array objects inherit properties from the Array prototype.

On top of the 
is Object.prototype. Every prototype inherits properties and methods from the Object.prototype.

A prototype is a blueprint of an object. Prototype allows us to use properties and methods on an object even if the properties and methods do not exist on the current object.

### Q : What is a prototype chain?
A : Prototype chaining is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language.

The prototype on object instance is available through Object.getPrototypeOf(object) or proto property whereas prototype on constructors function is available through Object.prototype.


### Q : What is prototypal inheritance?
A : When we read a property from object , and it's missing, JavaScript automatically takes it from the prototype. In programming, such thing is called “prototypal inheritance”.
```javascript
let car = function(model) {
 this.model = model;
};

car.prototype.getModel = function() {
 return this.model;
}

let a = new car('Toyota');
console.log(a.getModel());
}
==> result: Toyota
```
### Q : Function Declarations vs. Function Expressions
A : 
```javascript
//Function Declarations
function a() {
 console.log('Hello');
}

//Function Expressons
var a = function() {
 console.log('Hello');
}
```

### Q : What do you understand by Callback and Callback hell in JavaScript?
A : A callback function is a function which is passed as an argument to second function, which is invoked inside the second function at some point to execute some action. But, sometimes callback gets difficult to write in the code. So to make it simple, let’s first start with knowing the syntax of arrow function and its similarities with regular function.

A Callback is a function that is to be executed after another function has finished executing — hence the name ‘call back’.

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action. The above example is a synchronous callback, as it is executed immediately.

It is used to handle the execution of function after the completion of the execution of another function. A callback would be helpful in working with events. In the callback, a function can be passed as an argument to another function. It is a great way when we are dealing with basic cases such as minimal asynchronous operations.
```javascript
// function
function greet(name, callback) {
    console.log('Hi' + ' ' + name);
    callback();
}

// callback function
function callMe() {
    console.log('I am callback function');
}

// passing function as an argument
greet('Peter', callMe);
```
Callback hell: When we develop a web application that includes a lot of code, then working with callback is messy. This excessive Callback nesting is often referred to as Callback hell.

### Q : What is promises?
A : Promises are used to handle asynchronous operations in JavaScript. 
it has 4 state: 
* fulfilled: Action related to the promise succeeded
* rejected: Action related to the promise failed
* pending: Promise is still pending i.e not fulfilled or rejected yet
* settled: Promise has fulfilled or rejected
```
var promise = new Promise(function(resolve, reject) { 
  const x = "geeksforgeeks"; 
  const y = "geeksforgeeks"
  if(x === y) { 
    resolve(); 
  } else { 
    reject(); 
  } 
}); 
  
promise. 
    then(function () { 
        console.log('Success, You are a GEEK'); 
    }). 
    catch(function () { 
        console.log('Some error has occured'); 
    }); 
```

* Promise.all()
- Promise.all() takes an iterable (such as Array) and returns a single promise that resolves when all of the promises have resolved.

- Keeping that in mind we can see how this method can be helpful, for example, if we need to fetch data from different points and they’re not dependent on each other (that means that we’re not interested in the sequence of execution) we can use Promise.all() to do that. But, there are some things that we need to keep in mind when using this method.

- Promise.all() has a fail-fast behavior. It means that if one of the promises is rejected then the promise returned from Promise.all() is rejected as well.

* Promise.allSettled()
- Promise.allSettled() is really similar to Promise.all() . It also takes an iterable and returns a promise that resolves after all of the given promises either have resolved or rejected, with an array of objects which describe the outcome of each promise.

- In simple words, it’s Promise.all() without fail-fast behavior and also a bit different return value. But why the different return value? Well, for us to understand whether the provided promise was rejected or resolved a simple value is usually not enough. 

* Promise.race()
- Promise.race() is a bit different although very similar to previous methods that we’ve discussed. It also takes in an iterable as an argument and returns a promise that either resolves or rejects as soon as one of the promises are either resolved or rejected. 

### Q : What are the pros and cons of promises over callbacks? 
A : Below are the list of pros and cons of promises over callbacks,

Pros:

It avoids callback hell which is unreadable
Easy to write sequential asynchronous code with .then()
Easy to write parallel asynchronous code with Promise.all()
Solves some of the common problems of callbacks(call the callback too late, too early, many times and swallow errors/exceptions)
Cons:

It makes little complex code
You need to load a polyfill if ES6 is not supported

### Q : What is async await?
* An async function is a function that always returns a promise. This allows you to use the await keyword within the function to handle asynchronous operations in a more synchronous-looking manner. The primary benefit of async functions is that they make it easier to write and reason about asynchronous code by avoiding callback hell and providing a more linear flow of control.
* The await keyword is used inside an async function to wait for a promise to settle (either resolve or reject). It allows you to pause the execution of the async function until the promise is resolved, and then retrieve the result.
```
async function fetchData() {
  // Simulating an asynchronous operation, e.g., fetching data from an API
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Data successfully fetched!");
    }, 1000);
  });
}

async function exampleAsyncFunction() {
  console.log("Start");

  // Using await to wait for a promise to resolve
  const result = await fetchData();

  console.log(result);
  console.log("End");
}

exampleAsyncFunction();
```

### Q : What is an Immediately Invoked Function in JavaScript?
A : An Immediately Invoked Function ( known as IIFE and pronounced as IIFY) is a function that runs as soon as it is defined.
```javascript
(function(){ 
  // Do something;
})();
```

### Q :  Explain Implicit Type Coercion in javascript.
A : Implicit type coercion in javascript is automatic conversion of value from one data type to another. It takes place when the operands of an expression are of different data types.
* String coercion
String coercion takes place while using the ‘ + ‘ operator. When a number is added to a string, the number type is always converted to the string type.
```javascript
var x = 3;
var y = "3";
x + y // Returns "33" 
```

### Q : Explain Hoisting in javascript.
A : Hoisting is a default behaviour of javascript where all the variable and function declarations are moved on top. This means that irrespective of where the variables and functions are declared, they are moved on top of the scope. The scope can be both local and global.

Hoisting is a JavaScript mechanism where variables, function declarations and classes are moved to the top of their scope before code execution. Remember that JavaScript only hoists declarations, not initialisation. Let's take a simple example of variable hoisting,

```javascript
hoistedVariable = 3;
console.log(hoistedVariable); // outputs 3 even when the variable is declared after it is initialized	
var hoistedVariable;

console.log(message); //output : undefined
var message = "The variable Has been hoisted";

```
To avoid hoisting, you can run javascript in strict mode by using “use strict” on top of the code.

### Q : console.log(6<7<8) ?
A : true
it counts from left to right and  6<7 is true and true means 1 so after 1st comparision it become 1<7 which is true so answer will be true.


### Q : What is memoization?
A : Memoization is an optimization technique that speeds up applications by storing the results of expensive function calls and returning the cached result when the same inputs are supplied again.
Memoization is used for expensive function calls but in the following example, we are considering a simple function for understanding the concept of memoization better.
```
javascript
function memoizedAddTo256(){
  var cache = {};

  return function(num){
    if(num in cache){
      console.log("cached value");
      return cache[num]
    }else{
      cache[num] = num + 256;
      return cache[num];
    }
  }
}

var memoizedFunc = memoizedAddTo256();

memoizedFunc(20); // Normal return
memoizedFunc(20); // Cached return
```
Although using memoization saves time, it results in larger consumption of memory since we are storing all the computed results.

### Q : What is a Temporal Dead Zone?
A : Temporal Dead Zone is a behaviour that occurs with variables declared using let and const keywords.
It is a behaviour where we try to access a variable before it is initialized.
```
javascript
x = 23; // Gives reference error
let x;

function anotherRandomFunc(){
  message = "Hello"; // Throws a reference error
  let message;
}
anotherRandomFunc();
```

### Q : What is a first order function
A : First-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value.
```const firstOrder = () => console.log ('I am a first order function!');```

### Q : What is Higher-Order Functions?
A : In Javascript, functions are values ( first-class citizens ). This means that they can be assigned to a variable and/or passed as a value. 
A function that accepts and/or returns another function is called a higher-order function. The map function is one of the many higher-order functions built into the language. sort, reduce, filter, forEach are other examples of higher-order functions built into the language.
For example, the map function on arrays is a higher order function. The map function takes a function as an argument.
```
javascript
const double = n => n * 2
[1, 2, 3, 4].map(double) // [ 2, 4, 6, 8 ]
--- OR ---
[1, 2, 3, 4].map(function(n){
    return n * 2
}) // [ 2, 4, 6, 8 ]

```
### Q : What is DOM?
A : DOM stands for Document Object Model.

DOM is a programming interface for HTML and XML documents.
When the browser tries to render a HTML document, it creates an object based on the HTML document called DOM. Using this DOM, we can manipulate or change various elements inside the HTML document.

### Q : What are the falsy values in JavaScript?
A : '', 0, null
undefined
false
NaN

### Q : How to check if a value is falsy?
A : Use the !! operator or Boolean function to check if they’re falsy.
If a value is falsy, then both will return false.

!!0
false

### https://stackoverflow.com/questions/17502948/nexttick-vs-setimmediate-visual-explanatio
### Q : Diff betweem setImediate and process.nexttick?
A : In simple terms:
process.nextTick: Executes a callback in the current event loop cycle, before continuing to the next phase, with higher priority.

setImmediate: Executes a callback in the next event loop cycle, after I/O events, with slightly lower priority.

Both are used for scheduling callbacks in Node.js, but their timing and priority within the event loop differ.

### Q : Debouncing and Throttling in JavaScript
A : DEBOUNCING
* Debounce function limits the execution of a function call and waits for a certain amount of time before running it again.
* Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page. 
* The debounced function will ignore all calls to it until the calls have stopped for a specified time period. Only then will it call the original function.
* Debouncing forces a function to wait a certain amount of time before running again. In other words, it limits the rate at which a function gets invoked.

```
const debounce = function(func, delay){
      let timer;
      return function () {     //anonymous function
        const context = this; 
	const args = arguments;
	clearTimeout(timer); 
	timer = setTimeout(()=> {
	    func.apply(context, args)
	},delay);
	}
}
```

Throttling

* Throttling limits the rate at which a function can be called.
* It ensures that the function is not called more than once in a specified time interval.
* Unlike debouncing, throttling guarantees that the function will be called at regular intervals, preventing it from being invoked too frequently.

Implementing Throttle:
Throttle can be a little taxing as its desired behavior has different interpretations. Let’s start by limiting the rate at which we execute a function.
Gaming — In action games, the user often performs a key action by pushing a button (example: shooting, punching). But, as any gamer knows, users often press the buttons much more than is necessary, probably due to the excitement and intensity of the action. So the user might hit “Punch” 10 times in 5 seconds, but the game character can only throw one punch in one second. In such a situation, it makes sense to throttle the action. In this case, throttling the “Punch” action to one second would ignore the second button press each second.

* It’s not recommended to use throttling logic in search bar and we we cannot use debouncing in shooting game scenario or browser resizing or onScroll events.
* Throttling or sometimes is also called throttle function is a practice used in websites. Throttling is used to call a function after every millisecond or a particular interval of time only the first click is executed immediately.
* Debouncing is a technique where we can monitor the time delay of user action and once that delay reaches our predetermined threshold we can can make the function call. Throttling is a technique where we make the function call in a predetermined time interval irrespective of continuous user actions.

### Q : What are the differences between cookie, local storage and session storage
A : 
| Feature     			          | Cookie 			   | Local storage      | Session storage  |
| ----------- 				  | -----------                    | ----------- 	| ----------- 	   |
| Accessed on client or server side       | Both server-side & client-side | client-side only   | client-side only |
| size				          | 4KB	        		   | 5 MB	   	| 5 MB        	   |

LocalStorage is the same as SessionStorage but it persists the data even when the browser is closed and reopened(i.e it has no expiration time) whereas in sessionStorage data gets cleared when the page session ends.

* Session storage is designed to be session-specific, tied to a single tab or window. If you close one tab, the session storage for that tab will be cleared. However, the session storage in the other tab will remain unaffected.

* Local storage persists across sessions and tabs, but each tab has its own separate local storage. Closing one tab will not affect the local storage of the other tab.

* In summary, closing one tab does not automatically clear the session storage or local storage of another tab. Each tab maintains its own storage state. If you want to share data between tabs, you would need to use other mechanisms such as window.postMessage or a shared backend storage solution.

### Q : What is the use of setTimeout?
A : setTimeout is used to execute a function or evaluate an expression after a specified delay (in milliseconds). It schedules a one-time execution.
```
setTimeout(function () {
  console.log("Good morning");
}, 2000);
```

### Q : What is the use of setInterval?
A : setInterval is used to repeatedly execute a function or evaluate an expression at fixed intervals. It continues to execute the specified function at the specified interval until it is cleared with clearInterval.
```
let counter = 0;
const intervalId = setInterval(function() {
  console.log("Interval count:", counter++);
}, 1000);
```

### Q : what is setImmediate(Node.js)?
A : setImmediate is a Node.js-specific function used to execute a callback function after the current event loop cycle. It provides a way to execute code immediately after the current I/O events and before the next event loop cycle.Note that setImmediate is not a standard part of the ECMAScript specification and is specific to Node.js.
```
setImmediate(function () {
  console.log("Good morning");
});
```
--------------------------------------------------------------------------------------------------------------------------------------------------

# Node.js and REST APIs

### Q : How does Node.js works?
A : 
Node.js is completely event-driven. Basically the server consists of one thread processing one event after another.

A new request coming in is one kind of event. The server starts processing it and when there is a blocking IO operation, it does not wait until it completes and instead registers a callback function. The server then immediately starts to process another event ( maybe another request ). When the IO operation is finished, that is another kind of event, and the server will process it ( i.e. continue working on the request ) by executing the callback as soon as it has time.

Node.js Platform does not follow Request/Response Multi-Threaded Stateless Model. It follows Single Threaded with Event Loop Model. Node.js Processing model mainly based on Javascript Event based model with Javascript callback mechanism.

![ALT TEXT]([here you have to insert the image url](https://raw.githubusercontent.com/Mohamed-Hashem/nodejs-interview-questions/master/assets/event-loop.png)

Single Threaded Event Loop Model Processing Steps:

Clients Send request to Web Server.
Node.js Web Server internally maintains a Limited Thread pool to provide services to the Client Requests.
Node.js Web Server receives those requests and places them into a Queue. It is known as Event Queue.
Node.js Web Server internally has a Component, known as Event Loop. Why it got this name is that it uses indefinite loop to receive requests and process them.
Event Loop uses Single Thread only. It is main heart of Node.js Platform Processing Model.
Event Loop checks any Client Request is placed in Event Queue. If no, then wait for incoming requests for indefinitely.
If yes, then pick up one Client Request from Event Queue
Starts process that Client Request
If that Client Request Does Not requires any Blocking IO Operations, then process everything, prepare response and send it back to client.
If that Client Request requires some Blocking IO Operations like interacting with Database, File System, External Services then it will follow different approach
Checks Threads availability from Internal Thread Pool
Picks up one Thread and assign this Client Request to that thread.
That Thread is responsible for taking that request, process it, perform Blocking IO operations, prepare response and send it back to the Event Loop
Event Loop in turn, sends that Response to the respective Client.


### Q : REPL Function
A : 
Read − Reads user's input, parses the input into JavaScript data-structure, and stores in memory.

* Eval − Takes and evaluates the data structure.
* Print − Prints the result.
* Loop − Loops the above command until the user presses ctrl-c twice.
* The REPL feature of Node is very useful in experimenting with Node.js codes and to debug JavaScript codes.

### Q : Node advantage and disadvantage
A : 
#### ADVANTAGE
Asynchronous and Event Driven − All APIs of Node.js library are asynchronous, that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.

Very Fast − Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.

Single Threaded but Highly Scalable − Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server.

No Buffering − Node.js applications never buffer any data. These applications simply output the data in chunks.

#### Disadvantage
Reduces performance when handling Heavy Computing Tasks.

Node.js invites a lot of code changes due to Unstable API.

Node.js Asynchronous Programming Model makes it difficult to maintain code.

Choose Wisely – Lack of Library Support can Endanger your Code.

Node. js doesn't support multi-threaded programming yet. It is able to serve way more complicated applications than Ruby, but it's not suitable for performing long-running calculations. Heavy computations block the incoming requests, which can lead to decrease of performance .


### Q : where it's used?
A : 
* Real-time conversations
* Complex SPAs for the Internet of Things (Single-Page Applications)
* Tools for real-time collaboration
* Applications for streaming
* Architecture of microservices
* JSON APIs based Applications

### Q : cors
A : CORS, or Cross-Origin Resource Sharing, is a security feature implemented by web browsers that restricts web pages from making requests to a different domain than the one that served the original web page. This security measure is in place to prevent potential security vulnerabilities, such as cross-site request forgery.

When a web page makes a request to a different domain, the browser checks if the server on that domain allows such cross-origin requests. If the server doesn't explicitly permit the request, the browser blocks it for security reasons. This is where CORS comes into play.

CORS is implemented using HTTP headers. The server must include specific headers in its response to indicate which origins are allowed to access its resources. The main headers involved in CORS are:

1.) Access-Control-Allow-Origin: Specifies which origins are permitted to access the resource. It can be a specific origin or a comma-separated list of origins.

2.) Access-Control-Allow-Methods: Specifies the HTTP methods (e.g., GET, POST) that are allowed when accessing the resource.

3.) Access-Control-Allow-Headers: Specifies which headers can be used during the actual request.

4.) Access-Control-Allow-Credentials: Indicates whether the browser should include credentials (like cookies or HTTP authentication) when making the actual request.

5.) Access-Control-Expose-Headers: Specifies which headers should be exposed to the response.

### Q : How node.js prevents blocking code?
A : Blocking vs Non-blocking

Blocking is when the execution of additional JavaScript in the Node.js process must wait until a non-JavaScript operation completes. This happens because the event loop is unable to continue running JavaScript while a blocking operation is occurring.

Synchronous methods in the Node.js standard library that use libuv are the most commonly used blocking operations. Native modules may also have blocking methods. Blocking methods execute synchronously and non-blocking methods execute asynchronously.

```
// Blocking
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
console.log(data);
moreWork(); // will run after console.log

// Non-blocking
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
  console.log(data);
});
moreWork(); // will run before console.log
```

### Q : Name the types of API functions in Node.js?
A : There are two types of API functions in Node.js:

Asynchronous, Non-blocking functions
Synchronous, Blocking functions

### Q : Streams
A : 
* Readable − Stream which is used for read operation.

* Writable − Stream which is used for write operation.

* Duplex − Stream which can be used for both read and write operation.

* Transform − A type of duplex stream where the output is computed based on input.

### Q : Chaining the Streams
A : Chaining is a mechanism to connect the output of one stream to another stream and create a chain of multiple stream operations. It is normally used with piping operations. Now we'll use piping and chaining to first compress a file and then decompress the same.

The readable.pipe() method in a Readable Stream is used to attach a Writable stream to the readable stream so that it consequently switches into flowing mode and then pushes all the data that it has to the attached Writable

```
// Accessing fs module
var fs = require("fs");
 
// Create a readable stream
var readable = fs.createReadStream('input.txt');
 
// Create a writable stream
var writable = fs.createWriteStream('output.txt');
 
// Calling pipe method
readable.pipe(writable);
 
console.log("Program Ended");
```

Create a js file named main.js with the following code −

```
var fs = require("fs");
var zlib = require('zlib');

// Compress the file input.txt to input.txt.gz
fs.createReadStream('input.txt')
   .pipe(zlib.createGzip())
   .pipe(fs.createWriteStream('input.txt.gz'));
  
console.log("File Compressed.");
```

### Q : Node.js - Global Objects
A : Node. js Global Objects are the objects that are available in all modules. Global Objects are built-in objects that are part of the JavaScript and can be used directly in the application without importing any particular module.

* __filename
* __dirname
* console
* process
* exports
* module
* require()

### Q : Node.js DNS Module
A : DNS is a node module used to do name resolution facility which is provided by the operating system as well as used to do an actual DNS lookup.

Advantage
No need for memorising IP addresses – DNS servers provide a nifty solution of converting domain or subdomain names to IP addresses.
```
var dns = require('dns');
var w3 = dns.lookup('w3schools.com', function (err, addresses, family) {
  console.log(addresses);
});
```
it gives IP of the host

getServers() :	Returns an array containing all IP addresses belonging to the current server
lookup() : Looks up a hostname. A callback function contains information about the hostname, including it's IP address
lookupService() : Looks up a address and port. A callback function contains information about the address, such as the hostname
resolve() : Returns an array of record types belonging to the specified hostname

### Q : What is the preferred method of resolving unhandled exceptions in Node.js?
A : Unhandled exceptions in Node.js can be caught at the Process level by attaching a handler for uncaughtException event.

```
process.on('uncaughtException', function(err) {
    console.log('Caught exception: ' + err);
});
```

Process is a global object that provides information about the current Node.js process. Process is a listener function that is always listening to events.

Few events are :

* Exit
* disconnect
* unhandledException
* rejectionHandled

### Q : Event loop and Work Flow
A : 
* Node.js is a single-threaded event-driven platform that is capable of running non-blocking, asynchronously programming. These functionalities of Node.js make it memory efficient. The event loop allows Node.js to perform non-blocking I/O operations despite the fact that JavaScript is single-threaded. It is done by assigning operations to the operating system whenever and wherever possible.

* Node.js is an event loop single-threaded language. It can handle concurrent requests with a single thread without blocking it for one request.

## Features of Event Loop:

* Event loop is an endless loop, which waits for tasks, executes them and then sleeps until it receives more tasks.
* The event loop executes tasks from the event queue only when the call stack is empty i.e. there is no ongoing task.
* The event loop allows us to use callbacks and promises.
* The event loop executes the tasks starting from the oldest first.

Libuv implements two extremely important features of node.js  

Event Queue
Event loop
Thread pool

Parts of the Node.js architecture
* Node.js server: The Node.js server receives user requests, processes them, and sends feedback to the users. It is the server-side of the platform.

* Event queue: The event queue helps in request handling. It arranges incoming requests and sends them for processing one after the other.

* Requests: These are the tasks users try to perform on web applications. They are sent to the web application's server.

* Thread pool: These are the number of available threads used to carry out every incoming request by the user.

* Event loop: The event loop receives requests from clients, processes them, and sends them back to the client.

* External resources: These are resources that help perform client requests. The request could be computational or requires data storage.

A request is sent to the server by the client. The request could be to delete data, query data, update data, and so on.
The request is received by the event queue and kept for processing.
The events are sent in the order they were received through the event loop. A check is also performed to know if any event requires external resources.
The event loop processes the request (input/output) output polling and sends the feedback to the client.

## Advantages of using Node.js
Fewer resources are required in the operations carried out in the Node.js server.
Node.js can handle multiple concurrent requests with ease. This is made possible through the event queue and the thread pool.
Node.js does not need multiple threads because the event loop helps handle the events one after the other.

### Q : Why to use Express.js?
Features of Express.js:
* Fast Server-Side Development: The features of node js help express saving a lot of time.
* Middleware: Middleware is a request handler that has access to the application's request-response cycle.
* Routing: It refers to how an application's endpoint's URLs respond to client requests.
* Templating: It provides templating engines to build dynamic content on the web pages by creating HTML templates on the server.
* Debugging: Express makes it easier as it identifies the exact part where bugs are.

### Q : Node.js Worker Threads
A : Worker Threads in Node.js is useful for performing heavy JavaScript tasks. With the help of threads, Worker makes it easy to run javascript codes in parallel making it much faster and efficient. We can do heavy tasks without even disturbing the main thread.

### Q : Child process
A : Node.js runs in a single-thread mode, but it uses an event-driven paradigm to handle concurrency. It also facilitates creation of child processes to leverage parallel processing on multi-core CPU based systems.

Definition: A child process in Node.js is a spawned operating system process created by the main (parent) Node.js process. It allows Node.js to run other programs or scripts as separate processes.
Use Cases: Commonly used for parallelizing tasks, running external commands, or offloading CPU-intensive operations to separate processes.
Module: The child_process module in Node.js provides functionalities to spawn child processes, communicate with them, and handle their input/output.

Child processes always have three streams child.stdin, child.stdout, and child.stderr which may be shared with the stdio streams of the parent process.

Node provides child_process module which has the following three major ways to create a child process.
* exec − child_process.exec method runs a command in a shell/console and buffers the output.
* spawn − child_process.spawn launches a new process with a given command.
* fork − The child_process.fork method is a special case of the spawn() to create child processes.
```
const { spawn } = require('child_process');
const ls = spawn('ls', ['-l', '/']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});
```
## In summary, Node.js primarily relies on a single thread for execution and uses the event loop to handle concurrency. Child processes are used to spawn separate operating system processes for parallel execution, but Node.js does not create child threads within the same process for concurrency.

### Q : Diff between import and require
A : The differences between import and require are primarily related to the modules system used in JavaScript and its versions (ES5, CommonJS, and ES6+).

* require (CommonJS): Traditionally used in Node.js and CommonJS modules. It is a synchronous statement and is used to load modules in a blocking manner.Typically used in Node.js environments or with bundlers like Webpack that understand CommonJS.

* import (ES6+): Introduced in ECMAScript 2015 (ES6) and is the standard syntax for modules in modern JavaScript. It is asynchronous and allows for more advanced features like named exports and default exports.Standardized by ECMAScript, it is used in modern browsers that support ES6 modules. Additionally, it's commonly used with bundlers and transpilers like Babel.

* In summary, while both require and import are used to include external modules in JavaScript, require is associated with CommonJS (Node.js) and is synchronous, while import is the standard syntax for ES6 modules and is asynchronous. The choice between them depends on the JavaScript environment and the module system being used.

### Q : what is module wrapper function?
A : 
* The module wrapper function is a wrapper around each Node.js module's code, providing context-specific variables and encapsulation. It includes parameters like exports, require, module, __filename, and __dirname. It helps in modularizing code and preventing variable conflicts.

* This wrapper is automatically applied by Node.js to every module, ensuring a level of encapsulation and providing access to module-specific features.

Here's a short representation of the module wrapper function:
```
//if you run code like below
console.log('1')
//it will print : 1 coz it will be aexecuted like below

(function (exports, require, module, __filename, __dirname) {
	console.log('1')
});
```

### Q : Clustering in node.js
A : In the context of Node.js, a cluster refers to a mechanism for parallelizing and distributing the load of a Node.js application across multiple processes, taking advantage of multi-core systems. The cluster module in Node.js provides an easy way to create child processes (workers) that share the same server port. Each worker runs on a separate core, allowing the application to handle more concurrent connections and distribute the processing load.

Having multiple processes to handle incoming requests means that several requests can be processed simultaneously and if there is a long-running/blocking operation on one worker, the other workers can continue handling other incoming requests — your app won't have come to a standstill until the blocking operation completes.

In the context of Node.js, a cluster refers to a mechanism for parallelizing and distributing the load of a Node.js application across multiple processes, taking advantage of multi-core systems. The cluster module in Node.js provides an easy way to create child processes (workers) that share the same server port. Each worker runs on a separate core, allowing the application to handle more concurrent connections and distribute the processing load.

Key components and concepts related to Node.js clusters:

* Master Process:

The main Node.js process is known as the master process. It manages the creation and termination of worker processes and handles communication between them.
The master process typically listens for incoming connections and then distributes those connections among the worker processes.

* Worker Processes:

Worker processes are spawned by the master process using the cluster.fork() method.
Each worker runs its own instance of the Node.js event loop, effectively utilizing multiple CPU cores.
Workers can handle incoming requests independently, improving the application's concurrency and overall performance.

* Communication:

The master and worker processes can communicate with each other using inter-process communication (IPC) channels.
Communication is often used to share common resources, distribute tasks, or notify the master process about worker status.

* Load Balancing:

The built-in cluster module provides a basic form of load balancing by distributing incoming connections among the available worker processes.
Load balancing ensures that each worker is handling a roughly equal number of requests, optimizing the utilization of system resources.

```
var cluster = require('cluster');
var http = require('http');
var numCPUs = 4;

if (cluster.isMaster) {
 for (var i = 0; i < numCPUs; i++) {
  cluster.fork();
 }
} else {
 http.createServer(function(req, res) {
  res.writeHead(200);
  res.end('process ' + process.pid + ' says hello!');
 }).listen(8000);
}
```

### Q : Dependency and Devdependencies in package.json
A :
- "dependencies" : Packages required by your application in production.
```
npm install <package-name> --save
or
npm install <package-name> --save-prod
```

- "devDependencies" : Packages that are only needed for local development and testing.
```
npm install <package-name> --save-dev
```

### Q : Node.js Memory Leak Detectors
A : Fixing a memory leak is not as straightforward as it may seem. You’ll need to check your codebase to find any issues with your global scope, closures, heap memory, or any other pain points I outlined above.

A quick way to fix Node.js memory leaks in the short term is to restart the app. Make sure to do this first and then dedicate the time to seek out the root cause of the memory leak.

* Memwatch
* Heapdump
these tools can work

* Centroid-based Clustering.
* Density-based Clustering.
* Distribution-based Clustering.
* Hierarchical Clustering.

### Q : How to optimaze a nodeJS api project
A : 
* Use the Latest Node.js Version: Always use the latest stable version of Node.js. New releases often come with performance improvements and optimizations.

* Code Profiling and Performance Monitoring: Utilize tools like clinic.js or profiler to identify performance bottlenecks in your code. Monitoring tools like New Relic or AppDynamics can provide insights into your application's performance in a production environment.

* Caching: Implement caching mechanisms for frequently accessed data. This can include in-memory caching (using libraries like node-cache or memory-cache) or external caching solutions like Redis.

* Database Optimization: Optimize database queries, use proper indexing, and consider database connection pooling. Use tools like Sequelize or TypeORM to manage database interactions efficiently.

* Compression: Compress responses to reduce data transfer size. Middleware like compression can be added to your Express application.

* Load Balancing: Deploy your application behind a load balancer to distribute incoming traffic across multiple instances. This helps improve scalability and availability.

* Async/Await: Utilize async/await syntax for asynchronous operations, making your code more readable and maintainable. This can also help in avoiding callback hell.

* Connection Pooling: If your API connects to databases or external services, use connection pooling to reuse connections and avoid the overhead of creating new ones for each request.

* Concurrency: Adjust the concurrency settings of your server based on your application's needs. Tools like pm2 allow you to manage and scale Node.js processes effectively.

* Optimized Libraries: Choose libraries that are optimized for performance. For example, use Fastify instead of Express for lightweight and faster APIs.

* Minimize Dependencies: Regularly review and minimize unnecessary dependencies in your project. Each dependency adds some overhead, and a leaner project is generally easier to manage and deploy.

* Error Handling: Implement robust error handling to catch and log errors effectively. Use tools like winston for advanced logging.

### Q : How to do errror handling in nodejs
A : 
* You can use traditional try...catch blocks to handle synchronous errors. Keep in mind that try...catch only works for synchronous code. Asynchronous errors won't be caught using this method.
* Using Promises: When working with asynchronous code, you can use Promises and handle errors using the .catch() method.
* Using async/await: With the introduction of async/await in ES2017, handling asynchronous code has become more readable.
* Express.js Error Handling: If you are using Express.js for web development, you can define error-handling middleware.
```
app.use((err, req, res, next) => {
  // Handle error
  console.error(err);
  res.status(500).send('Internal Server Error');
});
Ensure that this middleware is defined after your route handlers.
```
* Logging: Always log your errors for debugging purposes. You can use libraries like Winston or Bunyan for structured logging.

### Q : how to optimise a api which is getting timeout
A : 
* Identify the Cause: Before making any optimizations, you need to identify the root cause of the timeouts. This could be due to various reasons such as slow database queries, external service delays, or inefficient code. Use logging and monitoring tools to track the execution flow and pinpoint where the delays occur.

* Optimize Database Queries: If your API relies on database queries, inefficient queries can lead to timeouts. Optimize database queries, ensure proper indexing, and use tools like database profilers to identify slow queries.

* Connection Pooling: If your API makes frequent database or external service connections, use connection pooling to reuse existing connections. This reduces the overhead of creating new connections for each request.

* Asynchronous Processing: Consider offloading time-consuming tasks to background processes or worker queues to avoid blocking the main thread. This allows the API to respond quickly to incoming requests while background tasks are processed separately.

* Load Balancing: If your API is under heavy load, consider deploying it behind a load balancer. Load balancing distributes incoming traffic across multiple server instances, improving both performance and availability.

* Increase Timeout Values: If the timeouts are occurring due to network latency or other temporary issues, consider increasing the timeout values for your API. However, be cautious about setting excessively high timeouts, as this may mask underlying issues.

* Optimize Code Execution: Review and optimize the performance of your code. Identify any loops, computations, or operations that can be optimized. Profiling tools can help identify performance bottlenecks in your code.

* Caching: Implement caching mechanisms for frequently requested data. Caching reduces the need to compute or fetch data on every request, improving response times.

* Implement Retries: For external service calls, consider implementing retry mechanisms with exponential backoff. This can help handle temporary failures and reduce the impact of intermittent issues.

* Distributed Tracing: Use distributed tracing tools to analyze the flow of requests across different components of your system. This can help identify where delays are occurring and how different services contribute to the overall response time.

* Review Infrastructure: Check the infrastructure hosting your API. Ensure that your server resources (CPU, memory, disk I/O) are not saturated. Consider scaling up your infrastructure if necessary.

* Optimize Network Calls: Minimize the number of external API calls and optimize the ones that are necessary. Batch requests where possible and use efficient protocols for data transfer.

* Implement Circuit Breakers: Use circuit breakers to handle failures gracefully. If a particular service consistently fails to respond, a circuit breaker can temporarily stop making requests to that service, preventing the API from waiting indefinitely.

* Monitor and Analyze: Continuously monitor your API's performance using tools like New Relic, Datadog, or custom logging. Set up alerts for specific thresholds to be notified when response times exceed acceptable limits.

### Q : How to make nodeJS apis more secure
A : 
* Use the latest Node.js version: Always keep your Node.js runtime and dependencies up to date to benefit from security patches and improvements.
* Dependency Management:Regularly update your project dependencies and use tools like npm audit to identify and fix any known vulnerabilities in your project's dependencies.
```
npm audit
npm audit fix
```
* Input Validation and Sanitization: Validate and sanitize user inputs to prevent injection attacks and other security vulnerabilities. Use libraries like validator to help with input validation.
```
npm install validator
```
* Middleware for Security Headers:Implement security headers using middleware like helmet to enhance the security of your application. This includes headers like Content Security Policy (CSP), Strict-Transport-Security (HSTS), etc.
```
const express = require('express');
const helmet = require('helmet');

const app = express();
app.use(helmet());
```
* Authentication and Authorization:Use strong authentication mechanisms like JWT (JSON Web Tokens) for user authentication. Implement proper authorization checks to ensure that users have the necessary permissions to access specific resources.
```
npm install jsonwebtoken
```
* Secure sensitive data: Avoid hardcoding sensitive information like API keys and database credentials directly in your code. Use environment variables and a configuration management approach to handle such sensitive data securely.
* HTTPS: Always use HTTPS to encrypt data in transit. Obtain and use SSL/TLS certificates to enable secure communication between clients and your API.
* Logging and Monitoring: Implement robust logging to track and monitor activities. Use tools like Winston or Morgan for logging. Additionally, set up monitoring and alerting systems to be notified of any suspicious activities.
* Rate Limiting: Implement rate limiting to prevent abuse or denial-of-service attacks. Libraries like express-rate-limit can be helpful.
* Content Validation: Ensure that the data sent to your API is in the expected format and meets specific criteria. Use validation libraries such as joi for schema validation.
* Cross-Site Scripting (XSS) Protection: Sanitize user inputs and implement proper encoding to prevent cross-site scripting attacks.
```
const xss = require('xss');
```
* Security Audits: Regularly perform security audits and penetration testing to identify and fix potential vulnerabilities. Services like OWASP ZAP and Snyk can help in this regard.
* Avoid using deprecated packages: Remove or update deprecated packages to mitigate potential security risks.

### Q : Explain what is process.nexttick?
A : process.nextTick is a Node.js function that allows a callback function to be executed in the next iteration of the event loop. It provides a way to defer the execution of a function until the current stack has cleared, but before the event loop continues.

In Node.js, the event loop is the mechanism that handles asynchronous operations. When you execute a piece of asynchronous code (like reading from a file or making an HTTP request), Node.js doesn't block the entire program. Instead, it continues to execute the remaining synchronous code and then processes the asynchronous task when it's ready.

process.nextTick is often used to break down long-running tasks into smaller, asynchronous steps, allowing the event loop to handle other tasks in between. It's important to note that process.nextTick callbacks have priority over other asynchronous events in the event loop.

Here's a simple example to illustrate its usage:
```
console.log('Start');

process.nextTick(() => {
  console.log('Next Tick Callback');
});

console.log('End');
//result
Start
End
Next Tick Callback
```

### Q : Implement JWT with node.js 
A: Implementing JWT (JSON Web Tokens) in a Node.js application typically involves using a library like jsonwebtoken. Here's a simple example of how you can implement JWT in a Node.js application:
```
const express = require('express');
const jwt = require('jsonwebtoken');

const app = express();
const secretKey = 'your-secret-key'; // Replace with a secure secret key

// Sample user data (replace with your authentication logic)
const users = [
  { id: 1, username: 'john_doe', password: 'password123' },
  { id: 2, username: 'jane_smith', password: 'securepass' },
];

// Middleware to verify the JWT token
function authenticateToken(req, res, next) {
  const token = req.header('Authorization');
  if (!token) return res.sendStatus(401);

  jwt.verify(token, secretKey, (err, user) => {
    if (err) return res.sendStatus(403);

    req.user = user;
    next();
  });
}

app.use(express.json());

// Endpoint to generate a JWT token
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  // Replace this with your authentication logic (e.g., querying a database)
  const user = users.find(u => u.username === username && u.password === password);

  if (!user) {
    return res.status(401).json({ message: 'Invalid username or password' });
  }

  const token = jwt.sign({ id: user.id, username: user.username }, secretKey, { expiresIn: '1h' });

  res.json({ token });
});

// Protected endpoint - requires a valid JWT token
app.get('/protected', authenticateToken, (req, res) => {
  res.json({ message: 'Access granted to protected resource', user: req.user });
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```
In this example:

The /login endpoint receives a username and password, performs authentication (replace with your own authentication logic), and generates a JWT token using the jsonwebtoken library.
The /protected endpoint is a sample protected resource that requires a valid JWT token for access. The authenticateToken middleware verifies the token.
Remember to replace 'your-secret-key' with a secure secret key in your production application. Additionally, the example uses an in-memory user array for simplicity; in a real-world scenario, you would likely have a database and a more robust authentication mechanism.

### Q : What is diff between authentication and authorisation?
A :
* Authentication:

What it checks: Verifies "Who you are."
Goal: Confirms the identity of a user or system.
Example: Logging in with a username and password.

* Authorization:

What it checks: Determines "What you are allowed to do."
Goal: Controls access and actions based on permissions.
Example: Deciding if a logged-in user can view, edit, or delete certain data.
In essence, authentication confirms identity, while authorization decides what actions or resources are permitted for the identified entity.

## FOR DOCUMENTATION FOR REST API USED SWAGGER AND TESTING USED POSTMAN 

### REST api
A : REST represents REpresentational State Transfer; it is a relatively new aspect of writing web API.
REST is stateless, therefore the SERVER has no state (or session data)
With a well-applied REST API, the server could be restarted between two calls as every data is passed to the server
Web service mostly uses POST method to make operations, whereas REST uses GET to access resources

* POST - Create

* PUT - Update/Replace

* Patch - Update/Modify

* Delete - Delete

* Get - Read

Here is a simple description of all: POST is always for creating a resource ( does not matter if it was duplicated ) PUT is for checking if resource exists then update, else create new resource. PATCH is always for updating a resource.

### Q : What is the difference between PUT and POST?
A : Answer: PUT is used to update a resource or create it if it doesn't exist, typically updating the entire resource. POST is used to create a new resource or submit data for processing.

### Q : Explain the term "Idempotent" in the context of HTTP methods.
A : Answer: An HTTP method is considered idempotent if making the same request multiple times has the same result as making it once. GET, PUT, and DELETE are idempotent, while POST is not.

### Q : What is the difference between stateful and stateless communication?
A : Stateless communication means each request from a client to a server is independent and contains all the information needed. In stateful communication, the server retains the client's state across requests.

### Q : Explain the purpose of the OPTIONS HTTP method.
A : The OPTIONS method is used to describe the communication options for the target resource. It can be used to retrieve the allowed methods, headers, or other meta-information about a resource.

### Q : Explain the concept of content negotiation.
Content negotiation is the process of selecting the best representation for a resource based on the client's preferences. It involves the Accept and Content-Type headers in the HTTP request and response.

### Q: status code
* 200 OK= success
* 201 Created = A new resource has been created
* 400 Bad Request: The request could not be understood or was missing required parameters.
* 401 Unauthorized: Authentication is required, and the provided credentials are invalid.
* 403 Forbidden: The server understood the request but refuses to authorize it.
* 404 Not Found: The requested resource could not be found on the server.
* 405 Method Not Allowed: The request method (GET, POST, etc.) is not supported for the specified resource.
* 500 Internal Server Error: A generic error message indicating that something went wrong on the server.
* 502 Bad Gateway: The server, while acting as a gateway, received an invalid response from an upstream server.
* 503 Service Unavailable: The server is currently unable to handle the request due to temporary overloading or maintenance.

### Q : What is GraphQL?
A: GraphQL is a query language and runtime for APIs developed by Facebook. It allows clients to request only the data they need and receive a structured response.

### Q : How does GraphQL differ from REST?
A: GraphQL allows clients to specify the shape and structure of the response, enabling more efficient and flexible data retrieval compared to the fixed structure of REST.

### Q : How does GraphQL handle versioning?
A: GraphQL itself does not enforce versioning. Instead, it allows clients to request only the specific fields they need, reducing the impact of changes. Some APIs use versioning in the URL or headers if needed.

### Q : Explain the concept of a subscription in GraphQL.
A: Subscriptions in GraphQL enable real-time data updates. Clients can subscribe to specific events, and the server pushes updates to the subscribed clients when those events occur.

## GRAPHQL vs REST
Comparing GraphQL and REST in a tabular format:

| Criteria                | GraphQL                                        | REST                                         |
|-------------------------|------------------------------------------------|----------------------------------------------|
| Data Fetching           | Clients can request precise data with GraphQL queries, reducing over-fetching and under-fetching issues. | REST endpoints expose fixed data structures, which may lead to over-fetching or under-fetching of data. |
| Flexibility             | Provides flexibility for clients to request only the data they need, enhancing efficiency in data fetching. | Fixed endpoints may limit flexibility in data retrieval, requiring multiple endpoints for different data needs. |
| Learning Curve          | Might have a steeper learning curve due to its unique syntax and concepts like schemas and resolvers. | Familiar and well-established, with simpler concepts such as HTTP methods (GET, POST, PUT, DELETE) for CRUD operations. |
| Tooling and Ecosystem   | Offers a rich ecosystem with tools for introspection, schema validation, and client libraries for various platforms. | Well-established tooling with extensive support for testing, documentation, and libraries in various programming languages. |
| Performance Optimization| Provides efficient data fetching, reducing network overhead by fetching only required data. | Requires careful design to optimize endpoints for performance, potentially leading to multiple requests or data redundancy. |
| Existing Infrastructure| Might require adjustments or a shift in infrastructure to support GraphQL's single endpoint approach. | Can seamlessly integrate with existing RESTful architectures and infrastructure. |
| Scalability             | Enables efficient scaling as clients can request tailored data, reducing unnecessary data transfer. | Scalability might depend on the careful design of endpoints and caching strategies. |
| Developer Adoption      | Gaining popularity but may have less widespread adoption compared to REST. | Widely adopted and understood by developers due to its long-standing presence. |
| Use Cases               | Ideal for applications with complex data requirements, real-time updates, and diverse client needs. | Suited for simpler applications or those with well-defined data structures and operations. |
| Standardization         | Offers a unified approach to data fetching and manipulation, enhancing consistency in API design. | Adheres to HTTP standards, promoting interoperability and compatibility with various client and server implementations. |

Ultimately, the choice between GraphQL and REST depends on factors such as the nature of the application, data requirements, development team expertise, and long-term scalability goals. Each has its own strengths and weaknesses, and the decision should be based on the specific needs and constraints of the project.

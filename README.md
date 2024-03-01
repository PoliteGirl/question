<!-- [Javascript](#javascript "Goto Javascript") -->
<!-- [Node.js](#Node.js "Goto Node.js") -->

# Javascript

javascript is the best

### Q : What is js?
A : JavaScript is a programming language commonly used in web development. It was originally developed by Netscape as a means to add dynamic and interactive elements to websites.
JavaScript is a synchronous, blocking, single-threaded language.
JavaScript is a dynamically typed language. In a dynamically typed language, the type of a variable is checked during run-time in contrast to statically typed language, where the type of a variable is checked during compile-time.

JavaScript is a dynamically typed language. In a dynamically typed language, the type of a variable is checked during run-time in contrast to statically typed language, where the type of a variable is checked during compile-time

### Q : What are the different data types present in javascript?
A : There are two types of data types in JavaScript.
~~~
 1. Primitive data type
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
A : In Shallow copy, a copy of the original object is stored and only the reference address is finally copied. In Deep copy, the copy of the original object and the repetitive copies both are stored.

A deep copying means that value of the new variable is disconnected from the original variable while a shallow copy means that some values are still connected to the original variable.

For Deep clone use lodash lobrary
```_.cloneDeep(object)```

or use ... operator
```var a = { ...obj }```

or var student2 = Object.assign( {}, obj);

or can use var cloned = JSON.parse(JSON.stringify(obj));  but it looses all undefined and function and converts it to null value. Because JSON.parse(JSON.stringify(obj)) has some limitations like you have mentioned, which are, they do not serialize the circular object or things like Map, Set, Date, RegEx etc.

or structuredClone

const a = { x: 20, date: new Date() };
const b = structuredClone(a); 

shallow cloning is just like assign value to var like let a = obj;


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


### Q : JS array method
A : 
The pop() method removes the last element from an array. The pop() method returns the value that was "popped out".
```
let dailyActivities = ['work', 'eat', 'sleep', 'exercise'];

dailyActivities.pop();
console.log(dailyActivities); // ['work', 'eat', 'sleep']

// remove the last element from ['work', 'eat', 'sleep']
const removedElement = dailyActivities.pop();

//get removed element
console.log(removedElement); // 'sleep'
console.log(dailyActivities);  // ['work', 'eat']
```

The push() method adds a new element to an array (at the end).The push() method returns the new array length.

The shift() method removes the first array element and "shifts" all other elements to a lower index.The shift() method returns the value that was "shifted out".
```
let dailyActivities = ['work', 'eat', 'sleep'];

// remove the first element
dailyActivities.shift();

console.log(dailyActivities); // ['eat', 'sleep']
```

The unshift() method adds a new element to an array (at the beginning), and "unshifts" older elements.The unshift() method returns the new array length.

The concat() method creates a new array by merging (concatenating) existing arrays, The concat() method does not change the existing arrays. It always returns a new array.The concat() method can take any number of array arguments.

Splicing and Slicing Arrays :
The splice() method can be used to add new items to an array

```
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 0, "Lemon", "Kiwi");
```

The first parameter (2) defines the position where new elements should be added (spliced in).

The second parameter (0) defines how many elements should be removed.

The rest of the parameters ("Lemon" , "Kiwi") define the new elements to be added.

The splice() method returns an array with the deleted items:

The slice() method slices out a piece of an array into a new array.
```
let dailyActivities = ['sleep', 'work', 'exercise']
let newRoutine = ['eat'];

const newDailyActivities = dailyActivities.slice(1);
console.log(newDailyActivities); // [ 'sleep', 'work']
```

This example slices out a part of an array starting from array element 1 ("Orange"):The slice() method creates a new array.The slice() method does not remove any elements from the source array.

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
const sum = numbers.reduce(function (result, item) {
  return result + item;
}, 0);
console.log(sum); // 10
```

### Q : What is scope in javascript
A : Scope is the accessibility of variables, functions, and objects in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.

### Q : What is a strict mode in javascript
A : Strict Mode is a new feature in ECMAScript 5 that allows you to place a program, or a function, in a “strict” operating context. This way it prevents certain actions from being taken and throws more exceptions. The literal expression "use strict"; instructs the browser to use the javascript code in the Strict mode.

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
* Unlike regular functions, arrow functions do not have their own this. The value of this inside an arrow function remains the same throughout the lifecycle of the function and is always bound to the value of this in the closest non-arrow parent function.
* The handling of this is also different in arrow functions compared to regular functions.
* In short, with arrow functions there are no binding of this.
* In regular functions the this keyword represented the object that called the function, which could be the window, the document, a button or whatever.
* With arrow functions the this keyword always represents the object that defined the arrow function.
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

Rest parameter ( … )

It provides an improved way of handling parameters of a function.

Using the rest parameter syntax, we can create functions that can take a variable number of arguments.

Any number of arguments will be converted into an array using the rest parameter.

The rest operator (…) allows us to call a function with any number of arguments and then access those excess arguments as an array. The rest operator also allows us in destructuring array or objects.

The main difference between rest and spread is that the rest operator puts the rest of some specific user-supplied values into a JavaScript array.
```
function extractingArgs(...args){
  return args[1];
}

// extractingArgs(8,9,1); // Returns 9

function addAllArgs(...args){
  let sumOfArgs = 0;
  let i = 0;
  while(i < args.length){
    sumOfArgs += args[i];
    i++;
  }
  return sumOfArgs;
}

addAllArgs(6, 5, 7, 99); // Returns 117
addAllArgs(1, 3, 4); // Returns 8
```
- Rest parameter should always be used at the last parameter of a function:

Spread operator (…)

Although the syntax of spread operator is exactly the same as the rest parameter, spread operator is used to spread an array, and object literals. We also use spread operators where one or more arguments are expected in a function call. 

The spread operator (…) allows us to expand an iterable like array into its individual elements.

```

const myName = ["Sofela", "is", "my"];
const aboutMe = ["Oluwatobi", ...myName, "name."];

console.log(aboutMe);

// The invocation above will return:
[ "Oluwatobi", "Sofela", "is", "my", "name." ]

----------------------------------------------------------------------------------

const myName = "Oluwatobi Sofela";

console.log([...myName]);

// The invocation above will return:
[ "O", "l", "u", "w", "a", "t", "o", "b", "i", " ", "S", "o", "f", "e", "l", "a" ]

----------------------------------------------------------------------------------

const numbers = [1, 3, 5, 7];

function addNumbers(a, b, c, d) {
  return a + b + c + d;
}

console.log(addNumbers(...numbers));

// The invocation above will return:
16

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

Callback: Callback is an asynchronous equivalent for a function. A callback function is called at the completion of a given task.  callback is a function that will be executed after another function gets executed.

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
The callbacks are needed because javascript is an event driven language. That means instead of waiting for a response javascript will keep executing while listening for other events. Let's take an example with the first function invoking an API call(simulated by setTimeout) and the next function which logs the message.

As observed from the output, javascript didn't wait for the response of the first function and the remaining code block got executed. So callbacks are used in a way to make sure that certain code doesn’t execute until the other code finishes execution.

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

    }
    else{
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

### Q : Debouncing and Throttling in JavaScript
A : DEBOUNCING
Debounce function limits the execution of a function call and waits for a certain amount of time before running it again.

Debouncing is a programming practice used to ensure that time-consuming tasks do not fire so often, that it stalls the performance of the web page. The debounced function will ignore all calls to it until the calls have stopped for a specified time period. Only then will it call the original function.
Debouncing forces a function to wait a certain amount of time before running again. In other words, it limits the rate at which a function gets invoked.

Implementing Debounce:
The general idea for debouncing is-
1) Start with 0 timeout.
2) If the debounced function is called again, reset the timer to the specified delay.
3) In case of timeout, call the debounced function.
Thus every call to a debounce function resets the timer and delays the call.

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

Throttling or sometimes is also called throttle function is a practice used in websites. To throttle a function means to ensure that the function is called at most once in a specified time period (for instance, once every 10 seconds). This means throttling will prevent a function from running if it has run “recently”. Throttling also ensures a function is run regularly at a fixed rate.
Throttling is used to call a function after every millisecond or a particular interval of time only the first click is executed immediately.

Implementing Throttle:
Throttle can be a little taxing as its desired behavior has different interpretations. Let’s start by limiting the rate at which we execute a function.
Gaming — In action games, the user often performs a key action by pushing a button (example: shooting, punching). But, as any gamer knows, users often press the buttons much more than is necessary, probably due to the excitement and intensity of the action. So the user might hit “Punch” 10 times in 5 seconds, but the game character can only throw one punch in one second. In such a situation, it makes sense to throttle the action. In this case, throttling the “Punch” action to one second would ignore the second button press each second.

Scroll event handler — Another application of throttling is in content-loading webpages like Facebook and Twitter where the user keeps on scrolling. In these scenarios, if the scroll event is fired too frequently, there might be a performance impact, as it contains lots of videos and images. Thus the scroll event must make use of throttling.

1. Throttling a button click so we can’t spam click
2. Throttling an API call
3. Throttling a mousemove/touchmove event handler
~~~
1) Debouncing is a technique where we can monitor the time delay of user action and once that delay reaches our predetermined threshold we can can make the function call.

2) Throttling is a technique where we make the function call in a predetermined time interval irrespective of continuous user actions.

3) Even though both debouncing and throttling seems like similar, both have their own use-cases. It’s not recommended to use throttling logic in search bar and we we cannot use debouncing in shooting game scenario or browser resizing or onScroll events.

Throttling or sometimes is also called throttle function is a practice used in websites. Throttling is used to call a function after every millisecond or a particular interval of time only the first click is executed immediately.
~~~

Debouncing is a technique where we can monitor the time delay of user action and once that delay reaches our predetermined threshold we can can make the function call. Throttling is a technique where we make the function call in a predetermined time interval irrespective of continuous user actions.


### Q : What are the differences between cookie, local storage and session storage
A : 
| Feature     			          | Cookie 			   | Local storage      | Session storage  |
| ----------- 				  | -----------                    | ----------- 	| ----------- 	   |
| Accessed on client or server side       | Both server-side & client-side | client-side only   | client-side only |
| size				          | 4KB	        		   | 5 MB	   	| 5 MB        	   |

LocalStorage is the same as SessionStorage but it persists the data even when the browser is closed and reopened(i.e it has no expiration time) whereas in sessionStorage data gets cleared when the page session ends.

### Q : What is the use of setTimeout?
A : The setTimeout() method is used to call a function or evaluate an expression after a specified number of milliseconds. For example, let's log a message after 2 seconds using setTimeout method,
```
setTimeout(function () {
  console.log("Good morning");
}, 2000);
```

### Q : What is the use of setInterval?
A : The setInterval() method is used to call a function or evaluate an expression at specified intervals (in milliseconds). For example, let's log a message after 2 seconds using setInterval method,

```
setInterval(function () {
  console.log("Good morning");
}, 2000);
```

### Q : what is setImmediate?
A : setImmediate() is designed to execute a script once the current poll (event loop) phase completes.
```
setImmediate(function () {
  console.log("Good morning");
});
```

### Q : S.O.L.I.D. in JS OOP
A : 
- S : Single responsibility principle : A class should have one and only one reason to change, meaning that a class should only have one job.

- O : Open closed principle : Objects or entities should be open for extension, but closed for modification. Open for extension means that we should be able to add new features or components to the application without breaking existing code. Closed for modification means that we should not introduce breaking changes to existing functionality, because that would force you to refactor a lot of existing code 

- L : Liskov substitution principle : All this is stating is that every subclass/derived class should be substitutable for their base/parent class. In other words, as simple as that, a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.

- I : Interface segregation principle : A client should never be forced to implement an interface that it doesn’t use or clients shouldn’t be forced to depend on methods they do not use.

- D : Dependency Inversion principle : Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.

--------------------------------------------------------------------------------------------------------------------------------------------------

# Node.js and REST APIs

### Q : REPL Function
A : 
Read − Reads user's input, parses the input into JavaScript data-structure, and stores in memory.

Eval − Takes and evaluates the data structure.

Print − Prints the result.

Loop − Loops the above command until the user presses ctrl-c twice.

The REPL feature of Node is very useful in experimenting with Node.js codes and to debug JavaScript codes.

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
A : Cross-Origin Resource Sharing (CORS) headers allow apps running in the browser to make requests to servers on different domains (also known as origins). CORS headers are set on the server side - the HTTP server is responsible for indicating that a given HTTP request can be cross-origin. CORS defines a way in which a browser and server can interact and determine whether or not it is safe to allow a cross-origin request.

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


### Q : Node.js Worker Threads
A : Worker Threads in Node.js is useful for performing heavy JavaScript tasks. With the help of threads, Worker makes it easy to run javascript codes in parallel making it much faster and efficient. We can do heavy tasks without even disturbing the main thread.

### Q : Child process
A : Node.js runs in a single-thread mode, but it uses an event-driven paradigm to handle concurrency. It also facilitates creation of child processes to leverage parallel processing on multi-core CPU based systems.

Child processes always have three streams child.stdin, child.stdout, and child.stderr which may be shared with the stdio streams of the parent process.

Node provides child_process module which has the following three major ways to create a child process.

* exec − child_process.exec method runs a command in a shell/console and buffers the output.

* spawn − child_process.spawn launches a new process with a given command.

* fork − The child_process.fork method is a special case of the spawn() to create child processes.

### Q : clustering in node.js
A : The cluster module provides a way of creating child processes that runs simultaneously and share the same server port. Node.js runs single threaded programming, which is very memory efficient, but to take advantage of computers multi-core systems, the Cluster module allows you to easily create child processes that each runs on their own single thread, to handle the load.

The Node.js Cluster module enables the creation of child processes (workers) that run simultaneously and share the same server port. Each spawned child has its own event loop, memory, and V8 instance. The child processes use IPC (Inter-process communication) to communicate with the parent Node.js process.

Having multiple processes to handle incoming requests means that several requests can be processed simultaneously and if there is a long-running/blocking operation on one worker, the other workers can continue handling other incoming requests — your app won't have come to a standstill until the blocking operation completes.

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

### Q : What are design patterns?
A : First of all, let’s start with an explanation of what design patterns are. In the simplest terms, they allow us to reuse code for recurring problems. Instead of solving the same problems again and again, we can reuse efficient code that already works.

Design patterns, simply put, are a way for you to structure your solution’s code in a way that allows you to gain some kind of benefit. Such as faster development speed, code reusability, and so on.

A design pattern is a general, reusable solution to a commonly occurring problem.

Why would you use design patterns? Here are some good reasons:

* They are well-documented and tested.
* They are reusable in many different situations.
* They are efficient.
* They will save you time.

There are three types of design patterns:

1. Creational — the creation of the object instances
2. Structural — the way the objects are designed
3. Behavioural — how objects interact with each other


## Singletons

- The singleton pattern is a design pattern that restricts the instantiation of a class to one object.

- The singleton patterns restrict the number of instantiations of a “class” to one. Creating singletons in Node.js
Node.js is an asynchronous event-driven JavaScript runtime and is the most effective when building scalable network applications. Node.js is free of locks, so there's no chance to dead-lock any process. is pretty straightforward, as require is there to help you.

We can get a glimpse of the purpose of this design pattern from its name: singleton. We use this design pattern when we only want a single instance of a class. That means we cannot create multiple instances — just one. If there is no instance, a new one is created. If there is an existing instance, it will use that one.
```
//area.js
var PI = Math.PI;

function circle (radius) {
  return radius * radius * PI;
}

module.exports.circle = circle;
```
It does not matter how many times you will require this module in your application; it will only exist as a single instance.
```
var areaCalc = require('./area');
```
console.log(areaCalc.circle(5));
Because of this behaviour of require, singletons are probably the most common Node.js design patterns among the modules in NPM

## Factory
- Once again, we can get an idea of what this design pattern does by looking at its name. The Factory design pattern allows us to define an interface or abstract class used to create an object. We then use the interface/abstract class to instantiate different objects.

- Consider an application where we have to create and use all types of vehicles. There are motor vehicles (cars, buses, trucks, motorcycles), railed vehicles (trains, trams), aircraft (airplanes, helicopters), and watercraft (ships, boats). Thus, instead of creating instances by calling the constructor of each class individually, we can implement the Factory pattern as follows:
```
import Motorvehicle from './Motorvehicle'; 
import Aircraft from './Aircraft'; 
import Railvehicle from './Railvehicle';  
const VehicleFactory = (type, make, model, year) => {   
    if (type === car) {     
        return new Motorvehicle('car', make, model, year);   
    } else if (type === airplane) {     
        return new Aircraft('airplane', make, model, year);   
    } else if (type === helicopter) {     
        return new Aircraft('helicopter', make, model, year);   
    } else {     
        return new Railvehicle('train', make, model, year);   
    } 
}  
module.exports = VehicleFactory;
```

* Factory pattern provides an interface/abstract class for creating objects.
* You can create different objects by using the same interface/abstract class.
* It improves the structure of the code and makes it easier to maintain it.

## Builder Pattern
- Separate the construction of a complex object from its representation so that the same construction process can create different representations

- The Builder pattern is used to create objects in "steps". Normally we will have functions or methods that add certain properties or methods to our object.

- The cool thing about this pattern is that we separate the creation of properties and methods into different entities.

## Prototype Pattern

- Specify the kind of objects to create using a prototypical instance, and create new objects by copying this prototype.

- The Prototype pattern allows you to create an object using another object as a blueprint, inheriting its properties and methods.

### Q : OOPS in Javascript
A : 
## 1. Polymorphism in JavaScript : 
- Polymorphism refers to the concept that there can be multiple forms of a single method, and depending upon the runtime scenario, one type of object can have different behavior. It utilizes “Inheritance” for this purpose.

- Polymorphism in JavaScript refers to the concept of reusing a single piece of code multiple times. By utilizing Polymorphism, you can define multiple forms of a method, and depending upon the runtime scenario, one type of object can have different behavior. 

- Animals are frequently used to explain Polymorphism. In the below-given example, “Animal” is a parent class whereas, Cat and Dog are its derived or child classes. The speak() method is common in both child classes. The user can select an object from any child class at runtime, and the JavaScript interpreter will invoke the “speak()” method accordingly.

```
class Animal {
    speak()
    {
      console.log("Animals have different sounds");
    }
  }
class Cat extends Animal {}
class Dog extends Animal {}

var cat = new Cat();  
cat.speak(); //Animals have different sounds
var dog  = new Dog();
dog.speak(); //Animals have different sounds
```

- Method overriding is a specific type of Polymorphism that permits a child class to implement the method already added in the parent or base class, in a different manner. Upon doing so, the child class overrides the method of the parent class.

```
class Animal {
    speak()
    {
      console.log("Animals have different sounds");
    }
  }
class Cat extends Animal {
speak(){
console.log("Cat says Meow Meow");}
  } 
  }
class Dog extends Animal {
speak(){
console.log("Dog say Woof Woof");}
  }  
  }

var cat = new Cat();  
cat.speak(); //Cat says Meow Meow
var dog  = new Dog();
dog.speak(); //Dog say Woof Woof
```
- Polymorphism enables the programmers to reuse the code, which saves time.
- Implicit type conversion is supported by Polymorphism.
- It allows a child class to have the same name method added in the parent class, with different functionality.
- In different scenarios, a method’s functionality is added differently.
- Single variables can be utilized for storing multiple data types.

## 2.) Object : 
- An Object is a unique entity that contains properties and methods. For example “car” is a real life Object, which has some characteristics like color, type, model, horsepower and performs certain actions like drive. The characteristics of an Object are called Properties in Object-Oriented Programming and the actions are called methods. An Object is an instance of a class. Objects are everywhere in JavaScript, almost every element is an Object whether it is a function, array, or string. A Method in javascript is a property of an object whose value is a function.

```
let person = {
    first_name:'Mukul',
    last_name: 'Latiyan',
 
    //method
    getFunction : function(){
        return (`The name of the person is
          ${person.first_name} ${person.last_name}`)
    },
    //object within object
    phone_number : {
        mobile:'12345',
        landline:'6789'
    }
}
console.log(person.getFunction()); //The name of the person is Mukul Latiyan.
console.log(person.phone_number.landline); //6789
```

## 3.) Classes :
- Classes are blueprint of an Object. A class can have many Objects because class is a template while Object are instances of the class or the concrete implementation. 
- Before we move further into implementation, we should know unlike other Object Oriented Language there are no classes in JavaScript we have only Object. To be more precise, JavaScript is a prototype based Object Oriented Language, which means it doesn’t have classes, rather it defines behaviors using a constructor function and then reuse it using the prototype. 
- Even the classes provided by ECMA2015 are objects.

```
class Vehicle {
  constructor(name, maker, engine) {
    this.name = name;
    this.maker =  maker;
    this.engine = engine;
  }
  getDetails(){
      return (`The name of the bike is ${this.name}.`)
  }
}
// Making object with the help of the constructor
let bike1 = new Vehicle('Hayabusa', 'Suzuki', '1340cc');
let bike2 = new Vehicle('Ninja', 'Kawasaki', '998cc');
 
console.log(bike1.name);    // Hayabusa
console.log(bike2.maker);   // Kawasaki
console.log(bike1.getDetails()); //The name of the bike is Hayabusa
```

## 4.) Encapsulation :
- The process of wrapping properties and functions within a single unit is known as encapsulation. 
```
class person{
    constructor(name,id){
        this.name = name;
        this.id = id;
    }
    add_Address(add){
        this.add = add;
    }
    getDetails(){
        console.log(`Name is ${this.name},Address is: ${this.add}`);
    }
}
 
let person1 = new person('Mukul',21);
person1.add_Address('Delhi');
person1.getDetails();
```

## 5.) Inheritance : 
- It is a concept in which some properties and methods of an Object are being used by another Object. Unlike most of the OOP languages where classes inherit classes, JavaScript Objects inherit Objects i.e. certain features (property and methods) of one object can be reused by other Objects. 
```
class person{
    constructor(name){
        this.name = name;
    }
    //method to return the string
    toString(){
        return (`Name of person: ${this.name}`);
    }
}
class student extends person{
    constructor(name,id){
        //super keyword for calling the above class constructor
        super(name);
        this.id = id;
    }
    toString(){
        return (`${super.toString()},Student ID: ${this.id}`);
    }
}
let student1 = new student('Mukul',22);
console.log(student1.toString());
```


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

### Q : What are the advantages of PostgreSQL?
A : Some of the advantages of PostgreSQL are open-source DBMS, community support, ACID compliance, diverse indexing techniques, full-text search, a variety of replication methods, and diversified extension functions, etc.

### Q : char and varchar difference in sql
A : VARCHAR is variable length, while CHAR is fixed length.

SQL varchar stores variable string length whereas SQL char stores fixed string length. This means SQL Server varchar holds only the characters we assign to it and char holds the maximum column space regardless of the string it holds.

### Q : What is the name of the process of splitting a large table into smaller pieces in PostgreSQL?
A : The name of the process of splitting a large table into smaller pieces in PostgreSQL is known as table partitioning.

### Q : What is the maximum size for a table in PostgreSQL?
A : PostgreSQL provides unlimited user database size, but it doesn't provide an unlimited size for tables. In PostgreSQL, the maximum size for a table is set to 32 TB.

### Q : Which commands are used to control transactions in PostgreSQL?
A : The following commands are used to control transactions in PostgreSQL:

BEGIN TRANSACTION
COMMIT
ROLLBACK

### Q : index POSTGRESQL
A : An Index is the structure or object by which we can retrieve specific rows or data faster. Indexes can be created using one or multiple columns or by using the partial data depending on your query requirement conditions.

Index will create a pointer to the actual rows in the specified table.

You can create an index by using the CREATE INDEX syntax.

* types 

1. B-tree : The most common and widely used index type is the B-tree index. This is the default index type for the CREATE INDEX command, unless you explicitly mention the type during index creation. 

If the indexed column is used to perform the comparison by using comparison operators such as <, <=, =, >=, and >, then the  Postgres optimizer uses the index created by the B-tree option for the specified column.

2. Hash index : The Hash index can be used only if the equality condition = is being used in the query.

3. GiST

4. SP-GiST

5. GIN

6. BRIN

### Q : What type of NoSQL database MongoDB is?
A : MongoDB is a document-oriented database. It stores the data in the form of the BSON structure-oriented databases. We store these documents in a collection.

### Q : Explain Namespace?
A : namespace is the series of the collection name and database name.

### Q : Explain Indexes in MongoDB?
A : In MongoDB, we use Indexes for executing the queries efficiently; without using Indexes, MongoDB should carry out a collection scan, i.e., scan all the documents of a collection, for selecting the documents which match the query statement. If a suitable index is available for a query, MongoDB will use an index for restricting the number of documents it should examine.

* Single field Index
* Compound Index
* Multikey Index
* Geospatial Indexes
* Text Index
* Hash Index
* Wildcard Index

### Q : What is a replica set?
A : We can specify the replica as a set of the mongo instances which host a similar data set. In the replica set, one node will be primary, and another one will be secondary. We replicate all the data from the primary to the secondary nodes.

### Q : What are Primary and Secondary Replica sets?
A : Primary and master nodes are the nodes that can accept writes. MongoDB's replication is 'single-master:' only one node can accept write operations at a time.

Secondary and slave nodes are read-only nodes that replicate from the primary.

### Q : Explain Sharding and Aggregation in MongoDB?
Aggregation: Aggregations are the activities that handle the data records and give the record results.
Sharding: Sharding means storing the data on multiple machines.

### Q : What does ObjectId contain?
ObjectId contains the following:

* Client machine ID
* Client process ID
* Byte incremented counter
* Timestamp

### Q : Explain Vertical Scaling and Horizontal Scaling?
A : 
* Vertical Scaling: Vertical Scaling increases storage and CPU resources for expanding the capacity. SQL databases are vertically scalable

* Horizontal Scaling: Horizontal Scaling splits the datasets and circulates the data over multiple shards or servers. NoSQL databases are horizontally scalable


### Q : S.O.L.I.D. in JS OOP
A : 
- S : Single responsibility principle : A class should have one and only one reason to change, meaning that a class should only have one job.

- O : Open closed principle : Objects or entities should be open for extension, but closed for modification. Open for extension means that we should be able to add new features or components to the application without breaking existing code. Closed for modification means that we should not introduce breaking changes to existing functionality, because that would force you to refactor a lot of existing code 

- L : Liskov substitution principle : All this is stating is that every subclass/derived class should be substitutable for their base/parent class. In other words, as simple as that, a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.

- I : Interface segregation principle : A client should never be forced to implement an interface that it doesn’t use or clients shouldn’t be forced to depend on methods they do not use.

- D : Dependency Inversion principle : Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.

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

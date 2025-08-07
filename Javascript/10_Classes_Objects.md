### Object 
- physical entity having some state and behaviour (properties and methods)
- Every object has a special property called prototype which is an object in itself.
- The prototype is nothing but a reference to some object through which all its properties and methods are inherited.
- Example: An array inhereits array methods and properties from its prototype objects which is Arrays
- We can set prototype using ```___proto__```
- If object and prototype has same method, the method of the object will be used.
``` javascript
const employee = {
   calcTax(){
      console.log("Tax rate is 10%);
   }
}
const rina = {
   salary: 10000
}
rina.__proto__ = employee
// This will inherit the properties from employee object
```

### Classes
- a blue-print / template with defined properties and methods used to create objects
- The objects created through the class will have properties and methods defined in class.
- If we want to create objects in bulk, with similar properties and behaviour, we can achieve it using classes
``` javascript
class MyClass {
   constructor(){
     ...
   }
   myMethod(){
     ...
  }
}
const myObj = new MyClass();
// this object will have a prototype referencing to MyClass having all the methods and constructor defined in it.
```

### Constructor
- it is a special method in class used to initialize object.
- every class has a default constructor with no arguments passed in it
- if we do not define any constructor in the class, the default constructor is called to intialiae the object with new keyword.
- if we want to assign properties with default values during initialization we use constructor
- a constructor can have multiple arguments
- if we define a parameterized constructor and dont pass any arguments when creating object,
  undefined will be passed as an argument through the constructor which kight cause unexpected behaviour
``` javascript
class Car {
   constructor(brand){
     this.brand = brand;
   }
}
const kia = new Car("Kia");
console.log(kia.brand) --> Kia
```

### Inheritance 
- passing down properties and methods from parent class to child class
- achieved using ```extends``` keyword
``` javascript
class Parent {
   hello(){
     console.log("hello");
   }
}
class Child extends Parent {}
const obj = new Child();
obj.hello(); // because the child class inherits method from parent class
```
**Method Overriding**
- if we define the method with same name in parent as well as child class, the one in the child class will be called.
- the method in the child class overrides the method in the parent class

**super keyword**
- used to call the constructor of parent class to access the properties and methods of parent class.
- it refers to the parent class through we can access its properties ans methods in the child class.
- if we use this keyword in the constructor of child class we need to invoke super before it to call constructor of parent class.
- Also, before exiting the constructor of the child class, we neded to use super()
- Otherwise it will throw reference error
- This is helpful to pass some important information from child class to parent class, through parametirized constructor.
``` javascript
class Parent {
   constructor(name){
    console.log("This is a parent class);
    this.name = name;
   }
   hello(){
     console.log("hello");
   }
}
class Child extends Parent {
   constructor(name){
      super(name);
      this.relation = "child"
      console.log("This is a child class");
      console.log("Exiting constructor");
   }
}
const obj = new Child("Anna");
obj.hello(); // because the child class inherits method from parent class
```

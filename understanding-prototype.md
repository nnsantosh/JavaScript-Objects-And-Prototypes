You can create behavior that impacts multiple objects by using prototypes.<br/>
Consider below example: <br/>
function MotorBike(cadence, speed, gear, pressure){ <br/>
  this.cadence = cadence; <br/>
  this.speed = speed; <br/>
  this.gear = gear; <br/>
  this.pressure = pressure; <br/>
  this.inflateTires = function(){<br/>
    this.pressure += 3;<br/>
  }<br/>
}<br/>
var bike1 = new MotorBike(50,20,4,30);<br/>
var bike2 = new MotorBike(50,20,4,30);<br/>

In this case the inflateTires function creates new instance of function object for every new MotorBike object that is created using the constructor function.
So every object is getting its own copy of inflateTires function.

Whenever JS engine processes a function it does not create one function object but it creates two objects:
1. The first object is the function object itself
2. The second object that gets created for every function object is called the prototype object.

The JS engine creates property on the function object that points to the prototype object.
Example: function foo(){}

You can access the function object using function name: foo
You can access the prototype object of the function using: foo.prototype

This prototype property comes into action whenever you create objects using new keyword for a function.
Example: var myObj = new foo();
Now if you observe the myObj it has a property: __proto__
This __proto__ refers to the prototype object of the foo function.

So whenever we create object using new keyword in JS it creates the __proto__ property on that object.

So if we create another object : var myObj2 = new foo();
This object also gets __proto__ property that refers to the prototype object of the foo function.

To validate this try the following:
create a new property on the prototype object: foo.prototype.test = "This is property of prototype object";
Now access this using: myObj.__proto__.test and myObj2.__proto__.test

So foo.prototype === myObj.__proto__ is true

Refer diagram:
![Inheritance](https://github.com/nnsantosh/JavaScript-Objects-And-Prototypes/blob/master/prototype.jpg)

Whenever you try to access property on a object in javascript if the property is not present in the object then JS engine tries to look it up in the prototype of that object. This happens implicitly.

So in the above example lets do myObj.hello
Since the property hello is not present in the myObj JS engine tries to look up this property on the myObj.__proto__.hello
If property is present in the prototype it returns it else will return undefined.

This is some kind of deferring of responsibility. If the object has it it returns it else it defers it to the prototype object.

The main use of this prototype object is that since all the objects created using the new function refer to the same prototype object you can inherit behavior using this prototype object.
So if you add functions/properties to this prototype object all the objects created using the new keyword/constructor function can inherit this behaviour.

Example:
function Employee(name){
  this.name = name;
}
var emp1 = new Employee("Sam");
var emp2 = new Employee("Pam");

Now execute emp1.printName() it returns undefined.
Similarly emp2.printName() it returns undefined.

Employee.prototype.printName = function(){
  console.log("name is: "+this.name);
}

Now execute emp1.printName() and it returns name is: Sam
Similarly emp2.printName() and it returns name is: Pam

So using this prototype we can add behavior dynamically at runtime to the objects in JavaScript.
Even after creating objects at later point of time if we need any new behavior we can add it using prototype and all objects created using that function will inherit this behavior and this is referred to as prototypal inheritance.

## Properties of prototype object:
Prototype object has a property called "constructor" that refers to the function

Example:
function Employee(name){
  this.name = name;
}
var emp1 = new Employee("Sam");

var proto = Employee.prototype;
proto.constructor will refer to function Employee:
function Employee(name){
  this.name = name;
}

This is useful to find out what was the function that created this object.
Example: emp1.__proto__.constructor

This is also useful to create new object using constructor function. Below Example:
var newEmpObj = emp1.__proto__.constructor("Megan");

It is always recommended not to use the dundo proto object and instead use the prototype object on the function that creates the objects to add new behavior.

## The Object function
JS has some global objects like the window object. Similarly it has another global function called Object which is of type function.
So you can create objects using the Object Function:
var myObj = new Object();
This is same as :
var simple = {};
In order to prove this do the following:
myObj.__proto__ === simple.__proto__ and this will return true

So whenever you are creating objects in javascript without using new keyword, you are implicitly calling the global Object function with new keyword to create that object.

## Object's Prototype
Whenever we create a function prototype object is created for that function.
The prototype object also has dundo proto property "__proto__" which refers to the Object's prototype
This is because the prototype object was created implicitly without using new keyword which means new Object() was called to create the prototype object.
So the dundo proto property of the prototype would refer to the Object function's prototype which is Object's prototype.
So whenever you look up a property for an object created using constructor function and if it does not exist then that property is looked up in the object's prototype and if that does not exist there also then it is also looked up in the Object's prototype.
Refer diagram:
![Object's prototype](https://github.com/nnsantosh/JavaScript-Objects-And-Prototypes/blob/master/Object_prototype.jpg)

Example:
function Employee(name){
  this.name = name;
}

var emp = new Employee("Sam");
emp.prop = "Employee";
emp.__proto__.parentProp = "Parent of Employee";
emp.__proto__.__proto__ === Object.prototype returns true
Object.prototype.grandParentProp = "Grand Parent";


So now if we do emp.grandParentProp it will return "Grand Parent"
But not only this we have included the grandParentProp property for every object in our system.

So by default if there is something in Object's prototype it is going to get accessed by every object unless that object has property of the same name.
Note that the Object's prototype has also a dundo proto property __proto__ that points to null.

So the Object's prototype is like global grand father of all objects in Javascript.

## Inheritance in Javascript using Prototypes
Let us say we have an Employee constructor function :
function Employee(name){
  this.name = name;
}

Let us say we add function getName to the prototype object of this Employee function
Employee.prototype.getName = function(){
  return this.name;
}

Now let us say we create another constructor function Manager:
function Manager(name,dept){
  this.name = name;
  this.dept = dept;
}

Manager.prototype.getDept = function(){
  return this.dept;
}

var emp1 = new Employee("Santosh");
var mgr1 = new Manager("Sukesh","IT");

emp1.getName() will return "Santosh"
mgr1.getDept() will return "IT"

Now if we do mgr1.getName() then it will return undefined since Manager object does not have getName() function

So both the objects Prototype objects refer to the grand parent: Object's prototype
But if we add the property getName to Object.prototype then it will become available to all objects in the system.
Instead we can point the Manager's prototype to the Employee's prototype.

So if any property is not present in manager then it will look up the manager's prototype. And if property is missing in manager's prototype then it will look up the Employee's prototype.

The way to do this is:
mgr1.__proto__.__proto__ = Employee.prototype;

Refer diagram:
![Inheritance](https://github.com/nnsantosh/JavaScript-Objects-And-Prototypes/blob/master/inheritance.jpg)

Now if we do mgr1.getName() then we will get "Sukesh"

Now manager object will get access to all the properties of Employee prototype.

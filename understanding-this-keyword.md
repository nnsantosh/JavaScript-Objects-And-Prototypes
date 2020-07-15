When there is a function that is called it is always called in a particular execution context.

There are two default arguments to every function call in Javascript : arguments and this

In general the key word this refers to the global object. For example in browser the global object is window object.

However depending on the context under which it is used it changes.

1. Consider below function:

    function bark(){
      console.log("bow bow!!");
      console.log(this);
    }

    When a function is called as bark();
    The this refers to the global object in this function.

2. if the above function is part of object like:

    var obj = {};
    obj.bark = function(){
      console.log("bow bow!!");
      console.log(this);
    }
    Now this is called as obj.bark();

    Now in the above function this refers to the object obj

3. new bark();

    For normal function using keyword new will not have any impact unless it is a constructor function.
    However whenever new keyword is used to call a function javascript inserts following line at the start of the function:
    var this = {}
    So in this case this refers to the empty object.

4. Now consider the below example:
function MotorBike(cadence, speed, gear){
  this.cadence = cadence;
  this.speed = speed;
  this.gear = gear;
}

var bike1 = new MotorBike(50,20,4);

Now add a function property called inflateTires to this function:

function MotorBike(cadence, speed, gear, pressure){
  this.cadence = cadence;
  this.speed = speed;
  this.gear = gear;
  this.pressure = pressure;
  this.inflateTires = function(){
    this.pressure += 3;
  }
}
var bike2 = new MotorBike(50,20,4,30);
bike2.inflateTires();
The function is being executed in the bike2 object's context.
After the above call the pressure property value of bike2 object will change to 33.

Let us say we have another object called BikeMechanic and bike mechanic should be able to inflate tire pressure of the bike objects handed to him/her.

So basically we want to take out the inflateTires function outside the context of MotorBike object and have it be a part of another object.

function BikeMechanic(name){
  this.name = name;
}

var billy = new BikeMechanic("Bill");
Now we need to give billy access to the inflateTires functionality.
billy.inflateTires = bike1.inflateTires;
Now if we call billy.inflateTires();
We get NaN
This is because inflateTires function needs property pressure which is not present in billy object.
So this.pressure will be undefined
undefined + 3 will be NaN so pressure property value of billy object will be NaN

So we want to pass the bike object to the mechanic so that he/she can inflate the tires of the bike.
billy.inflateTires.call(bike1);
The call function by default accepts an object as its first argument and binds that object to the this reference.

So lets take example:
function bark(){
    this.abc = def;
}
bark.call({});
Javascript does the following:   Whenever you execute the bark function it binds the this reference to the object that was passed in the call method.
So now we have a choice to change the object that this refers to in a function while invoking the function.

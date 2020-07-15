When there is a function that is called it is always called in a particular execution context. </br>

There are two default arguments to every function call in Javascript : arguments and this </br>

In general the key word this refers to the global object. For example in browser the global object is window object. </br>

However depending on the context under which it is used it changes. </br>

1. Consider below function: </br>

    function bark(){ </br>
      console.log("bow bow!!"); </br>
      console.log(this); </br>
    }

    When a function is called as bark(); </br>
    The this refers to the global object in this function. </br>

2. if the above function is part of object like: </br>

    var obj = {}; </br>
    obj.bark = function(){ </br>
      console.log("bow bow!!"); </br>
      console.log(this); </br>
    } </br>
    Now this is called as obj.bark(); </br>

    Now in the above function this refers to the object obj </br>

3. new bark();</br>

    For normal function using keyword new will not have any impact unless it is a constructor function. </br>
    However whenever new keyword is used to call a function javascript inserts following line at the start of the function: </br>
    var this = {} </br>
    So in this case this refers to the empty object. </br>

4. Now consider the below example: </br>
function MotorBike(cadence, speed, gear){ </br>
  this.cadence = cadence; </br>
  this.speed = speed; </br>
  this.gear = gear; </br>
} </br>

var bike1 = new MotorBike(50,20,4); </br>

Now add a function property called inflateTires to this function: </br>

function MotorBike(cadence, speed, gear, pressure){ </br>
  this.cadence = cadence; </br>
  this.speed = speed; </br>
  this.gear = gear; </br>
  this.pressure = pressure; </br>
  this.inflateTires = function(){ </br>
    this.pressure += 3; </br>
  } </br>
} </br>
var bike2 = new MotorBike(50,20,4,30); </br>
bike2.inflateTires(); </br>
The function is being executed in the bike2 object's context. </br>
After the above call the pressure property value of bike2 object will change to 33. </br>

Let us say we have another object called BikeMechanic and bike mechanic should be able to inflate tire pressure of the bike objects handed to him/her. </br>

So basically we want to take out the inflateTires function outside the context of MotorBike object and have it be a part of another object. </br>

function BikeMechanic(name){ </br>
  this.name = name; </br>
} </br>

var billy = new BikeMechanic("Bill"); </br>
Now we need to give billy access to the inflateTires functionality. </br>
billy.inflateTires = bike1.inflateTires; </br>
Now if we call billy.inflateTires(); </br>
We get NaN </br>
This is because inflateTires function needs property pressure which is not present in billy object. </br>
So this.pressure will be undefined </br>
undefined + 3 will be NaN so pressure property value of billy object will be NaN </br>

So we want to pass the bike object to the mechanic so that he/she can inflate the tires of the bike. </br>
billy.inflateTires.call(bike1); </br>
The call function by default accepts an object as its first argument and binds that object to the this reference. </br>
But by passing the bike1 object to the call function we imply that whenever there is a this reference in that function it should refer to the object passed in the call function.

So lets take example: </br>
function bark(){ </br>
    this.abc = def; </br>
} </br>
bark.call({}); </br>
Javascript does the following:   <br/>
Whenever you execute the bark function it binds the this reference to the object that was passed in the call method. </br>
So now we have a choice to change the object that this refers to in a function while invoking the function using the call function property. </br>

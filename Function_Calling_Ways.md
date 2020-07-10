There are four ways of calling function in javascript

Example: Consider below function

function bark(){
  console.log("bow bow!!");
}

1. The above function can be called as bark();

2. if the above function is part of object like
    var obj = {};
    obj.bark = function(){
      console.log("bow bow!!");
    }
Now this is called as obj.bark();

3. new bark();
For normal function using keyword new will not have any impact unless it is a constructor function.

4. bark.call();
Notice that the call function is a property of every javascript function object.

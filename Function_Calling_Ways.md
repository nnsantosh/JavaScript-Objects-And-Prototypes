There are four ways of calling function in javascript <br/>

Example: Consider below function <br/>

function bark(){ <br/>
 &nbsp;&nbsp;&nbsp;console.log("bow bow!!"); <br/>
} <br/>

1. The above function can be called as bark(); <br/>

2. if the above function is part of object like <br/>
    var obj = {}; <br/> <br/>
    obj.bark = function(){ <br/>
      &nbsp;&nbsp;&nbsp;console.log("bow bow!!"); <br/>
    } <br/>
Now this is called as obj.bark(); <br/>

3. new bark(); <br/>
For normal function using keyword new will not have any impact unless it is a constructor function. <br/>

4. bark.call(); <br/>
Notice that the call function is a property of every javascript function object. <br/>

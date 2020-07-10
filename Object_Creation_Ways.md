In Javascript there are four ways of creating object:

1. var myObj = {"firstName":"Santosh","lastName":"Nijalingappa"};

2. Using a function that returns object

function createEmployee(firstname,lastname){
    var empObj = {};
    empObj.firstName = firstname;
    empObj.lastName = lastname;
    return empObj;

}

var myEmployeeObj = createEmployee("Santosh","Nijalingappa");

3. Using constructor function

function Employee(firstname,lastname){
  this.firstName = firstname;
  this.lastName = lastname;
}

var myEmployeeObj = new Employee("Santosh","Nijalingappa");

Whenever new keyword is used to create object in javascript using constructor function following lines are implicitly added:
function Employee(firstname,lastname){
  var this = {};
  this.firstName = firstname;
  this.lastName = lastname;
  return this;
}
Notice the first line and last line are added by Javascript implicitly.

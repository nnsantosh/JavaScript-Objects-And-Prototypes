In Javascript there are four ways of creating object: <br/>

1. var myObj = {"firstName":"Santosh","lastName":"Nijalingappa"}; <br/>

2. Using a function that returns object <br/>

    function createEmployee(firstname,lastname){ <br/>
    &nbsp;&nbsp;&nbsp;var empObj = {}; <br/>
    &nbsp;&nbsp;&nbsp;empObj.firstName = firstname; <br/>
    &nbsp;&nbsp;&nbsp;empObj.lastName = lastname; <br/>
    &nbsp;&nbsp;&nbsp;return empObj; <br/>

    } <br/>

    var myEmployeeObj = createEmployee("Santosh","Nijalingappa"); <br/>

3. Using constructor function <br/>

    function Employee(firstname,lastname){ <br/>
    &nbsp;&nbsp;&nbsp;this.firstName = firstname; <br/>
    &nbsp;&nbsp;&nbsp;this.lastName = lastname; <br/>
    } <br/>

    var myEmployeeObj = new Employee("Santosh","Nijalingappa"); <br/>

    Whenever new keyword is used to create object in javascript using constructor function following lines are implicitly added:<br/>
    function Employee(firstname,lastname){ <br/>
    &nbsp;&nbsp;&nbsp;var this = {}; <br/>
    &nbsp;&nbsp;&nbsp;this.firstName = firstname; <br/>
    &nbsp;&nbsp;&nbsp;this.lastName = lastname; <br/>
    &nbsp;&nbsp;&nbsp;return this; <br/>
    } <br/>
    Notice the first line and last line are added by Javascript implicitly. <br/>

4. Using Object Function <br/>
    var myObj = new Object();
    

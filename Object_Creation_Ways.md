In Javascript there are four ways of creating object: <br/>

1. var myObj = {"firstName":"Santosh","lastName":"Nijalingappa"}; <br/>

2. Using a function that returns object <br/>

    function createEmployee(firstname,lastname){ <br/>
            var empObj = {}; <br/>
            empObj.firstName = firstname; <br/>
            empObj.lastName = lastname; <br/>
            return empObj; <br/>

    } <br/>

    var myEmployeeObj = createEmployee("Santosh","Nijalingappa"); <br/>

3. Using constructor function <br/>

    function Employee(firstname,lastname){ <br/>
            this.firstName = firstname; <br/>
            this.lastName = lastname; <br/>
    } <br/>

    var myEmployeeObj = new Employee("Santosh","Nijalingappa"); <br/>

    Whenever new keyword is used to create object in javascript using constructor function following lines are implicitly added:<br/>
    function Employee(firstname,lastname){ <br/>
            var this = {}; <br/>
            this.firstName = firstname; <br/>
            this.lastName = lastname; <br/>
            return this; <br/>
    } <br/>
    Notice the first line and last line are added by Javascript implicitly. <br/>

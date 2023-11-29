# Cypress-automation-begin
This is a repo where contains all the code for my first practice on automation project using Cypress framework.

## I/What I have learned
- [x] understand Cypress definition, its architecture and its benefits
- [x] how to install Node.js, VS Code, Cypress and set up project
- [x] know about Cypress Test runner
- [x] command lines for running Cypress, specifying which spec files to run, launching other browsers, recording tests to Cypress Cloud
- [x] find CSS locators to perform Cypress API when writing test
- [x] basic assertion in writing tests with Cypress
- [x] Cypress asynchronous nature and its promise handling
- [x] automation to handling alerts, popups, child windows
- [x] Cypress framework (how to retrieve data from Cypress fixtures, implement page objects, customed commands)
- [x] data-driven testing, retrieve data for testing from SQL database, CSV file, and Excel file
- [x] practice Cypress Cucumber practice integration
- [x] mock https request & response using Cypress intercept

## II/ Deep dive into each learning part ###
### 1/ What is Cypress? What is its architecture and its benefits? ####
- Definitions
    - Cypress framework is a JavaScript-based end-to-end testing framework. 
    - Cypress framework is a JavaScript-based end-to-end testing framework. 
    - Cypress is Frontend automation testing tool and it is built for web applications.
    - Cypress is built on Node.js and comes packaged as a npm module.
- Architecture: unlike other testing tool like Selenium/Protractor/Appium, Cypress operates by running inside the browser.
- Benefits:
    - It addresses the key pain point when testing
        - Automatically waits for commands & assertions before moving on.
        - Test edge testcases by mocking to server response (can also handle API validations).
        - Take snapshots when the test runs (before and after hitting Cypress command).
        - View videos of your entire tests execution.

### 2/ Install tools & dependencies
#### 2.1/ Install Node.js

Node.js is an open-source, cross-platform, back-end JavaScript runtime environment that runs on the V8 engine and executes JavaScript code outside a web browser

Download Node.js
  - Link (https://nodejs.org/en/download) to download Node.js and install it to your device after downloading

#### 2.2/ Install VS Code

Visual Studio Code, also commonly referred to as VS Code, is a source-code editor developed by Microsoft for Windows, Linux and macOS. Features include support for debugging, syntax highlighting, intelligent code completion, snippets, code refactoring, and embedded Git.

Download VS Code
    - Link (https://code.visualstudio.com/download)


#### 2.3/ Create a new Project with Package.json

Package.json file is a JSON file that exists at the root of a JavaScript/Node projects. It holds metadata relevant to the project and it is used for managing the project's dependencies.

***Steps to create it***
```js
mkdir CypressAutomation //this command helps to create a new folder
cd CypressAutomation //this command helps you go inside the CypressAutomation folder
npm -i init //this command helps you to create package.json file and keep hitting Enter for receiving the default values
```

***Install Cypress and make an entry for it in package.json***
```js
npm cypress install --save -dev
```

#### 2.3/ Knows about Cypress Runner

Cypress Test Runner is a graphical user interface (GUI) that allows you to easily visualize and debug your tests. It provides a dashboard with a list of your tests and a test runner window that displays the commands and results of each test, and a browser window that shows the application being tested.

**Commands for opening Cypress**
```js
node_modules/.bin/cypress open
```
OR
```js
npx cypress open
```

**Commands for running Cypress on browser/headless mode**
```js
npx cypress run --headless //run on headless mode
```

```js
npx cypress run --headed --browser chrome //run on Chrome browser for example
```

**Command for running all the files**
```js
npx cypress run --headed --browser chrome
```
**NOTE**: Remember to config the spec pattern in cypress.config.js file first, for example you want to run all the files with extension `.js` in cypress\integration\examples folder, config inside the section `e2e`

```js
e2e:{
    specPattern: 'cypress/integration/examples/*.js'
}
```

**Command for running specific file (not all the files)**
```js
npx cypress run --spec "cypress/e2e/examples/actions.cy.js" --headed --browser chrome //paste the relative path of the file inside the double quote ""
```
#### 2.4/ Setup Cypress Cloud and record tests 

Cypress Cloud is a place where tester can view and debug past test results from your CI environment, analyze and diagnose test health.

***Setup Cypress Cloud***

- Open Cypress Runner
- Login by choosing the username icon at the top right corner
- Create a project
- Add project ID in config.file.js file
 
```js
module.exports = {
projectID: "ngijqu" //projectID here is just an example
}
```

***Record tests via command***
```js
npx cypress run --record --key 359d1830-a95f-441b-8695-2b7981fba90a //key is generated by Cypress Cloud after you created project there
```

### 3/ Find CSS locators when writing Cypress tests

In CSS, selectors are patterns used to select the element(s) you want to style. Selectors are important it will help Cypress finds exact element which tester wants to interact with.

There are several ways to detect CSS locators

***If an element has an ID***
```js
cy.get('#idname') //with hash(#) icon before idname
```

***If an element has class name***
```js
cy.get('.classname') //with dot(.) icon before classname
```

If many CSS seletors have the same classname, so differentiate them with tagname beforehand
```js
cy.get('tagname.classname') //with dot(.) icon between the tagname and classname
```

***Customized with any attribute***
```js
cy.get('tagname[attribute=value]') //with attribute and its value being blocked inside square brackets
```

***Travel the tagname from parent to child to get the item***
```js
cy.get('ParentTagName ChildTagName') //with space( ) between Parent and Child
```

***Selects every `p` element that is the numberth child of its parent***
```js
cy.get('a p:nth-child(2)') //Selects every <p> element that is the second child of its parent a
```

***Selects every `p` element that is the numberth child of its parent, counting from the last child***
```js
cy.get('a p:nth-last-child(2)') //Selects every <p> element that is the second child of its parent a, counting from the last child
```

**NOTE**: You can add extension ChroPath or SelectorsHub to the browser to verify CSS selectors first to see how many elements matching with selectors OR you can take advantage of Cypress Runner to inspect the elements but it is not recommended.

### 4/ Common Cypress Queries and Assertions API

***Describe the test suite for each spec file***
```js
describe('My First Test Suite', function () { ////describe part "My First Test" is a test suite.
    it('My First Test Case', function () {
     //test step will go inside {} here
        })
})     
```

***Visit a page***
```js
describe('My First Test Suite', function () {
    it('My First Test Case', function () {
        cy.visit('https://www.google.com') //url will be wrapped inside single quotes
})
})
```

***Query for an element***
```js
describe('My First Test Suite', function () {
    it('My First Test Case', function () {
        cy.visit('https://www.google.com');
        cy.get('.button-cfm') //CSS locators being stated at no.3 above
})
})
```
OR

*When finding in a page in which it contains specific text*

```js
describe('My First Test Suite', function () {
    it('My First Test Case', function () {
        cy.visit('https://www.google.com');
        cy.contains('text');
```

**NOTE**: Difference between cy.get() and .find() in Cypress

- cy.get() is used to get the specific selector.
- .find() is used to get the descendent DOM elements of a specific selector. .find() cannot be chained off cy
- For example:

```js
cy.get('@productLocator').find('.product') //find product within productLocator
```
***Click an element and type in an element***

Click an element
```js
describe('My First Test Suite', function () {
    it('My First Test Case', function () {
        cy.visit('https://www.google.com');

        //find an element which contains "text" and click it
        cy.contains('text').click()
```

Type something in an element
```js
describe('My First Test Suite', function () {
    it('My First Test Case', function () {
        cy.visit('https://www.google.com');

        //Get the search input field and type "product" in it
        cy.get('.search-product').type('product')
```
***Basic Assertions API***

Assertion describes the desired state of your elements, your objects, and your application.

- Assert length of multiple elements
```js
cy.get('.product:visible').should('have.length', 4) //get all the products that have classname '.product' and check whether or not it presents 4 items
```
OR
```js
expect('.product:visible').to.have.length(4) 
```

- Assert a element whether it has a value
```js
cy.get('#form').should('have.value', 'abc') 
```

- Assert an element whether it has an attribute AND whether its attribute equals to a value
```js
cy.get('#form').should('have.attr', 'name', 'Potato') //get element with id named 'form' and assert that if it has attribute 'name' and whether the value of 'name' is 'Potato'
```

- Assert a checkbox/radio button whether it is checked/unchecked
```js
cy.get('#checkBoxOption1').check().should('be.checked') //assert if a checkbox is checked
cy.get('#checkBoxOption1').uncheck().should('not.be.checked') //assert if a checkbox is unchecked
```

### 5/ Asynchronous nature of Cypress
- Definition for both synchronous and asynchronous
    - In synchronous process, tasks are executed in a sequential and blocking manner. Each task must wait for another task finishes before it starts.
    - In asynchronous process, tasks can overlap or run independently of one another. An operation doesn't need to wait for the previous one to finish before starting.

- Asynchronous nature of Cypress
    - Cypress is asynchronous nature and it has a mechanism that if you concatenate one command with another Cypress command, then Cypress understands that both Cypress can translate and return a promise. (*Promise is a state of step executed. Promises come in 3 results: rejection, resolved, pending.*)
    - Cypress commands **DO NOT** return their subjects.
```js
const abc = cy.get('.classname'); //actually you cannot do this because Cypress doesn't return the object
abc.click()
```

- Instead, Cypress commands yield their subjects. Meaning their subjects are yielded from one command to the next and wait to be executed.

    
```js
// Visiting a web page with a form
cy.visit('https://example.com');

// Typing text into an input field
cy.get('input[name="username"]').type('john_doe');

// The subject (input field) is automatically yielded to the next command
// Now, we can perform additional actions on the same input field
cy.get('input[name="password"]').type('secretpassword');
```

- When you use a Cypress command, such as **cy.get()** or **cy.click()**, it returns a special object representing the subject of the command. The **.then()** method allows you to perform additional actions on this subject.
```js
cy.get('.my-element').then((element) => {
  // 'element' here is the subject yielded by cy.get()
  // Perform additional actions with the subject by using cy.wrap()
  cy.wrap(element).should('have.class', 'active');
});
```

### 6/ Cypress framework
#### 6.1/ Retrieve data from Cypress fixtures (data-driven test)
- Cypress is providing Fixtures as a feature to drive data from external sources. Input data under **fixtures** folder, inside the file which can be named example.json
```js
{
    "name": "Potato",
    "gender": "Male",
    "ProductName": ["Blackberry", "Nokia Edge", "iphone X"]
}
```
- Retrieve data from **fixtures** before you write down test steps inside **it**
- Run fixtures before all tests run by using **before** hook

```js
describe('My First Test Suite', function () {
    before(function () {
        // runs once before all tests
        //get access to the example.json file and resolve a promise by then method
        cy.fixture('example').then(function(data)
        {
        this.data = data
        })
        //"this.data" is a variable that can be accessed for the whole file. "Data" only can be accessed inside the "before" loop
        })
    })
it('My First Test Case', function () {

        cy.visit('https://www.abc.com')
        cy.get('div > input[name="name"]').type(this.data.name) //will be "Potato"
        cy.get('select').select(this.data.gender) //will be "Male"
})
})

```


  
          
          

  


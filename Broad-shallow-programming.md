# Broad-shallow-programming

### Table of contents
- [Front-end](#front-end)
- [Data format](#data-format)
   - [XML](#xmlextensible-markup-language)
   - [CSV](#csvcomma-separated-values)
   - [JSON](#jsonjavascript-object-notation)
- [API](#apiapplication-programming-interface)
   - [REST API](#rest-apirepresentational-state-transfer)
   - [SOAP](#soapsimple-object-access-protocol)
   - [GraphQL](#graphqlgraph-query-language)
   - [gRPC](#grpcgoogle-remote-procedure-call)
- [Web API](#web-api)
   - [DOM](#domdocument-object-model)
   - [CSSOM](#cssomcss-object-model)
   - [AJAX](#ajaxasynchronous-javascript-and-xml)
- [Call Stack](#call-stack)
   - [Stack trace](#stack-trace)
   - [Stack frame](#stack-frame)
- [Functional-programming](#functional-programming)
   - [First-class objects](#first-class-objects)
   - [Closure](#Closure)
   - [Lexical environment(Lexical scoping)](#lexical-environmentlexical-scoping)


## Front-end


## Data format
### XML(eXtensible Markup Language)
- A tag-based markup language that allows data to be represented in a hierarchical structure and stores data in a human-readable format.
```xml
```

### CSV(Comma-Separated Values)
- A text file format that separates each data value with a comma, primarily used for storing tabular data.
```csv
```

### JSON(JavaScript Object Notation)
- A lightweight data interchange format derived from JavaScript, which represents data in the form of objects, making it easy to read and write and easily manageable in most programming languages.
```json
```


## API(Application Programming Interface)
- Internal API(=Private API)
- Public API

### REST API(REpresentational State Transfer)
- RESTful API
- REST is an architectural style based on the HTTP protocol.
- It uses JSON or XML formats to send and receive data, and accesses resources via URLs.
- It is stateless and supports caching.
- Data-driven

### SOAP(Simple Object Access Protocol)
- A protocol based on XML, primarily used for communication between web services.
- Function-driven
- WSDL(Web Services Description Language)


### GraphQL(Graph Query Language)
- A query language developed by Facebook that allows clients to define the structure of the data they need in their requests.
- It uses a single endpoint and can handle complex data requests in one go.
- It provides a strong type system, allowing clients to clearly define the shape of the data they can receive.
- Data-focused and flexible

### gRPC(google Remote Procedure Call)


## Web API
### DOM(Document Object Model)
- The Document Object Model(DOM) is the data representation of the objects that comprise the structure and content of a document on the web.
- The Document Object Model(DOM) is a programming interface for web documents.

### CSSOM(CSS Object Model)

### AJAX(Asynchronous Javascript And Xml)

## Call Stack
- The call stack is one of the key data structures used to manage the flow of function calls when a computer program is running.
- It primarily uses a stack structure to store information about function calls.

### Stack trace
- Refers to the information that shows the list of currently called functions and the location where each function was called when an error or exception occurs during program execution.

### Stack frame
- A data structure created when a function is called, which includes the function’s local variables, parameters, and return address.

## Functional-programming
- It is a way of writing programming code.
- Minimize side effects.
   - Minimize the use of variables that developers directly handle as much as possible.
- Use pure functions.
   - A function that returns the same output for the same input, regardless of when or how many times it is executed.
      ```javascript
      function add(a, b) {
        return a + b
      }
      ```
- Immutability principle
   - It does not modify the original data. Changes must always be applied by creating a copy.
      ```javascript
      const numbers = [1, 2, 3]
      
      const newNumbers = [...numbers, 4]
      ```
- Referential transparency
   - The call statement of a functional code can be replaced with its return value.
      ```javascript
      const add = (a, b) => a + b
      
      const add_3_4 = add(3, 4) // This is equivalent to the following
      // const add_3_4 = 7
      
      console.log(add_3_4 === add(3, 4))
      console.log(add_3_4 === 7) // This is equivalent to the following
      ```
- Higher-order function
   - A function that takes another function as an argument or returns a function as its return value.
      - Like map, filter or reduce in javascript.
      - These methods take functions (e.g., callback functions) as arguments and perform specific operations on each element of the array.

### First-class objects
- A first-class object is an object in a programming language that can be assigned to a variable, passed as an argument to a function, and used as a return value.
- In javascript, functions are also objects.
- First-class object languages
   - JavaScript, Python, Ruby, C#, Swift, Kotlin, Rust
- Non-first-class object languages
   - C, C++, Java(~7), Fortran, Pascal, COBOL, BASIC, Visual Basic

### Closure
- Dictionary definition
   - A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). 
   - In other words, a closure gives a function access to its outer scope. 
   - In JavaScript, closures are created every time a function is created, at function creation time.
- When a function is declared, the lexical environment stores two pieces of information.
   1. The function's execution context(scope of function, like local variable)
   2. Outer reference information when a function is declared.
- When use the closure?
   1. Data encaptulation/private
   2. State maintenance
   3. Currying in Functional-programming

- Example 01
   ```javascript
   function delayLog(message, time) {
     setTimeout(function () {
       console.log(message)
     }, time)
   }
   
   delayLog('Remeber this!', 1000)
   ```
<br>

- Example 02
   ```javascript
   const globalVar = 'globalVar'
   
   function outer(outerParam) {
     const outerVar = 'outerVar'
     console.log(`outer func of outerVar   = ${outerVar}`)
     console.log(`outer func of outerParam = ${outerParam}`)
   
     function inner(innerParam) {
       console.log(`inner func of globalVar  = ${globalVar}`)
       console.log(`inner func of outerVar   = ${outerVar}`)
       console.log(`inner func of outerParam = ${outerParam}`)
   
       const innerVar = 'innerVar'
       console.log(`inner func of innerVar   = ${innerVar}`)
       console.log(`inner func of innerParam = ${innerParam}`)
     }
     return inner
   }
   
   let externalInner = outer('outerParam') // outer is dead.
   // Expected output:
   // outer func of outerVar   = outerVar
   // outer func of outerParam = outerParam
   
   console.log(typeof outerVar) // undefined
   console.log(typeof outerParam) // undefined
   console.log(typeof innerVar) // undefined
   console.log(typeof innerParam) // undefined
   
   externalInner('innerParam') // but externalInner has inner stored.
   // Expected output:
   // inner func of globalVar  = globalVar
   // inner func of outerVar   = outerVar
   // inner func of outerParam = outerParam
   // inner func of innerVar   = innerVar
   // inner func of innerParam = innerParam
   
   externalInner = null // outer's variable will be collected from garbage collector when next garbage collection time.
   ```
<br>


- Example 03
   ```javascript
   function createCounter(addValue) {
     let count = 0
   
     function doCountUp() {
       count += addValue
       console.log(count)
     }
   
     return doCountUp
   }
   
   const counterBy1 = createCounter(1)
   const counterBy3 = createCounter(3)
   
   counterBy1() // Expected output: 1
   counterBy1() // Expected output: 2
   counterBy1() // Expected output: 3
   
   counterBy3() // Expected output: 3
   counterBy3() // Expected output: 6
   counterBy3() // Expected output: 9
   ```
<br>

### Lexical environment(Lexical scoping)
- It refers to an environment that forms a scope based on the location where variables are declared.

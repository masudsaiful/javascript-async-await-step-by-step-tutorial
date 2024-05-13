**                                                                       **


At one time, developers wrote procedural JavaScript, meaning function-based JavaScript programming. But over time, JavaScript features and characteristics kept updating. Developers had to struggle a lot to handle single-threaded architecture, blocking, and execution sequence issues while writing programs. They had to write programming in a very cumbersome way to control which function would execute after which, to handle it beautifully. To overcome single-threaded issues, blocking issues, and synchronous programming problems, official JavaScript (ECMAScript) kept adding various features or characteristics at different times so that through multi-threaded, non-blocking, and asynchronous ways, many tasks could output simultaneously. This made web programming even smoother, more efficient, and developer-friendly.

Since JavaScript is inherently a single-threaded, blocking, and synchronous programming language, and in subsequent versions of ECMAScript, various updated features were added, combining all these with browser-dependent features and utilizing web APIs, we can write multi-threaded flavors, non-blocking, and asynchronous programming using JavaScript. In modern JavaScript, for handling asynchronous programming, in 2015, the ES6 standard introduced us to Promises objects, through which asynchronous operations can be tracked. Then in 2017, ECMA introduced the Async/Await concept, which works with Promises and helps handle asynchronous operations with even more proficiency, making it easier and more developer-friendly to write multi-threaded JavaScript code with better results.

## Before understanding Async/Await we should first need to understand the concept of the followings. More or less they are: 

A) Javascript Functions

B) Single-threaded, blocking and synchronous

C) Function Sequence and synchronous programming

D) Problems with synchronous programming

E) Callback

F) multi-threaded, non-blocking and asynchronous

G) Problems with Asynchronous programing using Callback (Callback Hell)

H) Javascript Promises

I) Async/Await

## Let's a short overview all of them:

### A) Javascript Function
#### i) Name Function
##### Declaration or Definition:
```javascript

# Function has a name and declared or defined as usually:

function functionName (param1, param2, ...) {

}
```

##### Invokation or Calling:
```javascript

# Function will execute when they are called or invoked like belows:

// Inside Javascript code
function functionName (param1, param2, ...) {

}
functionName(param1, param2, ...)


// Basically above code will be invoked automatically by browser Window Object, so above code will be the same as belows:
function functionName (param1, param2, ...) {

}
window.functionName(param1, param2, ...)


// When an event occurs in HTML:
function functionName (param1, param2, ...) {

}
<p onclick="functionName (param1, param2, ...)" />


// When an event occurs in Javascript:
function functionName (param1, param2, ...) {

}
object.onclick = function(){functionName};


// When an event occurs in Javascript using Event Handler:
function functionName (param1, param2, ...) {

}
object.addEventListener("click", functionName);


// Invoking a function as method in Javascript Object:
const Obj = {
  firstName:"f_name",
  lastName: "l_name",
  functionName: function (param1, param2, ...) {
    return this.firstName + " " + this.lastName + param1 + param2;
  }
}
Obj.functionName(param1, param2, ...);


// Invoking using Function Constructor:
function functionName(param1, param2, ...) {
  this.firstName = 'f_name';
  this.lastName  = "l_name";
  this.param1Val = param1;
  this.param2Val = param2;
}
const Obj = new functionName(param1, param2, ...);
Obj.firstName;
```

##### Return Value and Catch the Value:
```javascript

# Javascript Function can return value and catch the value in different ways:

// Returning value statement
function functionName (param1, param2, ...) {
  return param1 + param2;
}


// Returning value can assign to a variable where function is called
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let m = functionName (param1, param2, ...)


// The result value can be used in any statement or expression
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let m = functionName (param1, param2, ...)
let n = 'Something' + m


// Function call can be used directly as variable value where it is invoked
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let n = 'Something' + functionName (param1, param2, ...)
```

##### Hoisting:
```javascript

# Function call declaration can be happened before their definition. This is called Function hoisting:

// Calling before defining
functionName (param1, param2, ...)

function functionName (param1, param2, ...) {
  return param1 + param2;
}
```


#### ii) Anonymous Function
##### Declaration or Definition:
```javascript

# Function with no name is called Anonymous Function:

// This function has no name so it is called Anonymous Function
function (param1, param2, ...) {

}


// Anonymous Function can be defined using an expression
const m = function (param1, param2, ...) {return param1 + param2};


// Anonymous Function can be defined by assigning to a variable and later this variable will act as a function
const m = function (param1, param2, ...) {return param1 + param2};
m(param1, param2, ...)


// Anonymous Function can be defined directly as a callback function in another function
let x = 16
let y = 9
setTimeout(function (param1, param2) { 
    console.log(param1 + param2) // 25; 
}, 1000, x, y);


# NOTE: Anonymous Function can not be hoisted. They only execute when calling after declaration.

// Example
const m = function (param1, param2, ...) {return param1 + param2};
m(param1, param2, ...)
```

##### Invokation or Calling:
```javascript

// Function without name can be assigned to a variable using expression. The variable then can be used as function invokation
const m = function (param1, param2, ...) {return param1 + param2};
let n = m(param1, param2, ...)
let o = 'something' + n


// calling the variable directly In Javascript code without assigning to another variable
const m = function (param1, param2, ...) {return param1 + param2};
m(param1, param2, ...)
...


// Anonymous function can also be used as self-invoking function
(function (param1, param2, ...) {
  let x = param1;
  let y = param2
})(param1, param2, ...);


// Invoking directly as a callback function to another function parameter
let x = 16
let y = 9
setTimeout(function (param1, param2) { 
    console.log(param1 + param2) // 25; 
}, 1000, x, y);


// Invoking function variable as a callback function to another function parameter
let anonymousFunc = function (param1, param2) {
	return param1+param2;
}
function anotherFunction(a, b, callback) { 
	console.log(a + b + callback(a, b)) // 50;
}
anotherFunction(9, 16, anonymousFunc)


# Though often assigned to any variable while working, anonymous function variable invokation must be in function call format (functionName())

// This will return entire function
const arrowFuncName = function () {
  return 'Something';
}
console.log(arrowFuncName) // () => { return 'Something'; }


// This will return correct value
const arrowFuncName = function () {
  return 'Something';
}
console.log( arrowFuncName() ) // Something
```


#### iii) Arrow Function
##### ES6 introduced Arrow Function in 2015:
```javascript

# It's a shorter syntax for writing function expression. It's also short syntax of anonymous function:

// Example 1
# Anonymous Function
function () {
  return 'something';
}

same as,

# Arrow Function
() => {
  return 'something'
}


// Example 2
# Anonymous Function Expression assigned to a variable
const m = function () {return 'something'};

same as,

# Arrow Function Expression assigned to a variable
const m = () => { return 'something' };


// Example 3
# Anonymous Function Expression with parameter
const m = function (param1, param2) {return param1 + param2};

same as,

# Arrow Function Expression with parameter
const m = (param1, param2) => { return param1 + param2 };


// If Arrow function has single statement and return a value, it can be written as belows
const m = (param1, param2) => param1 + param2; // Omitted curly brackets {} and 'return' keyword


// If Arrow function has single parameter and single statement, it can be written as belows
const m = param1 => 'something' + param1; // Omitted curly brackets {}, 'return' keyword and parenthesis ()


// If Arrow function use 'return' keyword, must use 'curly brackets {}'
# Either a single statement
const m = param1 => { return 'something' + param1 };

or multiple statement
# const m = param1 => {
  // do something
  return 'something' + param1
};


// Arrow Function invokations or Callings are same as those of Anonymous Function described above


# Though often assigned to any variable while working, arrow function variable invokation must be in function call format (functionName())

// This will return entire function
const arrowFuncName = () => {
  return 'Something';
}
console.log(arrowFuncName) // () => { return 'Something'; }


// This will return correct value
const arrowFuncName = () => {
  return 'Something';
}
console.log( arrowFuncName() ) // Something


NOTE: Though Arrow Function actually the shorter syntax of Anonymous Function, it's also can't be hoisted.
```


### B) Single-threaded, blocking and synchronous
(From now on towards we will use arrow functions of all examples)


#### By default Javascript is single-threaded, blocking and synchronous nature. Let's see what are they in below.
##### Single-threaded:
In Javascript programming language while running code it can execute only one instruction at a time where multi-threaded programming languages can run multiple instructions at once. For single-threaded nature within the single call stack, Javascript code is read and gets executed line by line. Call stack concept is the same as the stack data structure. If you know the data structure, you will know the concept of Call stack. Whenever a line of code gets inside the call stack and wheever it's time to execute it gets executed and moves out of the stack and then next line of code and then next line of code and thus maintaining sequential execution. Let's have a look of the following example.
```javascript
      const x = () => {
        return 'something'
      }

      const y = () => {
        return x()
      }

      const z = () => {
        return y()
      }

      let result = z()

      console.log(result);
```
According Javascript single-threaded architecture let's track the above sample code what's happening in the single 'Call Stack'.

a) Instructions of each line of code are added to the stack frame of single call stack in LIFO (Last in first out) way

b) console.lgo(result) first in

c) then z() function

d) then y() function

e) then x() function

f) code executed sequentially 

g) Later deleting and thus releasing the call stack to empty 


##### Blocking:
Though Javascript code work sequentially and in the single-threaded stack frame, execution occur one instruction at a time, there may be very chance for the following line of instruction to wait untill it's previous execution completed. It is called blocking. Blocking is the nature of synchronous programming. Let's consider the previous example.
```javascript
      const x = () => {
        return 'something'
      }

      const y = () => {
        return x()
      }

      const z = () => {
        return y()
      }

      let result = z()

      console.log(result) // something;
```
Above three functions [ x(), y() and z() ] will work sequentially where z() function need to wait untill the y() function deliver it's result. So, z() will face blocking from the previous execution. Same to y() function task must wait for the previous one [x()] to be completed before moving to the next. This time-consuming execution which can block it's following instruction may happen for the reason of any external API call or any I/O operation or any server end dB connection request or other similar reasons.


##### Synchronous:
In javascript code within the synchronous calls, all the work is done line by line one after another i.e. the first task is executed then the second task is executed, no matter how much time one task will take. When one thread is locked, the thread following it in line is blocked. After escaping from block, execution will start for the next instruction. Look at this two illustrations below.
```javascript

      // Example 1
      const func1 = () => {
        console.log('something1')
      }

      const func2 = () => {
        console.log('something2')
      }

      const func3 = () => {
        console.log('something3')
      }

      func1()
      func2()
      func3()



      // Example 2
      const func1 = () => {
        console.log('something1')
      }

      const func2 = () => {
        console.log('something2')
      }

      const func3 = () => {
        console.log('something3')
      }

      func3()
      func2()
      func1()

```
The code illustrated in Example1 will print output 'something1', 'something2' and 'something3' sequentially no matter how long the blocking occur in any part inside these functions but will execute according their call sequence i.e. func1(), func2() and func3()


In the Example2 we can now seen that the output sequence orders are 'something3', 'something2' and 'something1'. This is because their function call execution occured line by line one after another according they are invoked and one instruction at a time i.e. func3(), func2() and func1()


### C) Function Sequence and synchronous programming
#### What we have already learned let's recape those again, 


##### Javascript is,

i) single-threaded in nature,

ii) blocking architecture and

ii) synchronous execution by default 



##### Javascript code execution happen,

i) line by line

ii) sequentially one after another

iii) one instruction at a time 

iv) next instruction will wait untill the previous instruction completed it's task, which means blocking



##### Javascript code execution based on following terminologies and Browser based engine
i) Javascript run time environment

ii) Javascript engine

iii) Memory Heap

iv) call stack

v) stack frame

vi) LIFO

vii) Callback Queue

viii) Event Loop

ix) Web APIs etc.


#### Function Sequence:
Functions are executed in the sequence they are called, not the sequence they are defined
Let's examine the following examples.
```javascript
//Example 1
const secondFunc = () =>  'Second';
const thirdFunc = () =>  'Third';
const firstFunc = () => 'First';


console.log(firstFunc()); // First
console.log(secondFunc()); // Second
console.log(thirdFunc()); // Third



//Example 2
const firstFunc = () => 'First';
const thirdFunc = () =>  'Third';
const secondFunc = () =>  'Second';


console.log(firstFunc()); // First
console.log(secondFunc()); // Second
console.log(thirdFunc()); // Third



//Example 3
const thirdFunc = () =>  'Third';
const firstFunc = () => 'First';
const secondFunc = () =>  'Second';


console.log(thirdFunc()); // Third
console.log(secondFunc()); // Second
console.log(firstFunc()); // First
```
Example1 and Example2 are always output the results i.e. 'First', 'Second' and 'Third' because functions are invoked sequentially like these, firstFunc(), secondFunc() and thirdFunc(). Whatever their declarations ordering are managed but result always depends on function call sequence.



Again in Example3 the result will be i.e. 'Third', 'Second' and 'First' because the calling sequence are in these order i.e. thirdFunc(), secondFunc() and firstFunc()



#### Synchronous Programming:
As we already knew Javascript execute functions sequentially but sometimes we would like to have better control over when to execute a function. In synchronous programming we can change the function execution order by customizing and interfering the sequence of instructions of any code to fullfil the need.


Suppose we want to do an order in a restaurant, and then update the order status, and then display the order status with greetings.
We can call an order function (orderFunc), save the order items with extra complimentary items, and then call the status function (orderStatusFunc), save the order status, and then call another function (displayOrderStatusFunc) to display the order status using greetings function (greetingsFunc) to display greetings besides order status.
```javascript
// Synchronous Programing: Example 1
const orderFunc = (item1, item2) => {
	let complimentaryItem = 'Calzone'
	let items = item1 + ', ' + item2 + ', ' + complimentaryItem 
	return items
}

const orderStatusFunc = item => {
	if (item) {
		let status = item + ', ' + 'Ready to deliver'
		return status
	}
}

const greetingsFunc = () => {
	return 'Warm hearted greetings for accepting our hospitality'
}

const displayOrderStatusFunc = (param1, param2) => {
	if (param1 && param2) {
		let display = param1 + '. ' + param2
		return display
	}
}

const order = orderFunc('pizza', 'burger')
const displayOrderStatus = displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))

console.log(displayOrderStatus) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"
```


Or, we could call a order function (orderFunc), and let the order function call the order status function (orderStatusFunc), and then let the order status function call the order status display function (displayOrderStatusFunc). Then after let the order status display function call the greetings function. Let's re-write the above code as below.  
```javascript
// Synchronous Programing: Example 2
const orderFunc = (item1, item2) => {
	let complimentaryItem = 'Calzone'
	let items = item1 + ', ' + item2 + ', ' + complimentaryItem
	let status = orderStatusFunc(items)
	return status
}

const orderStatusFunc = item => {
	if (item) {
		let status = item + ', ' + 'Ready to deliver'
		let display = displayOrderStatusFunc(status)
		return display
	}
}

const displayOrderStatusFunc = param => {
	if (param) {
		let greetings = greetingsFunc()
		let display = greetings + '. ' + param 
		return display
	}
}

const greetingsFunc = () => {
	return 'Warm hearted greetings for accepting our hospitality'
}

const order = orderFunc('pizza', 'burger')
console.log(order) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"
```


If you ever design patterns in OOP (Object-Oriented Programming), you'll find a lot of coherence with the above examples. Now let's try to understand how the two examples above are functioning and how we manage a better control over when to execute a function in synchronous programming. 

If we look at in 'Synchronous Programming: Example1' in this line,

```javascript
displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))
```

it will display output the greetings message in first part and order status in second part,

```javascript
console.log(displayOrderStatus) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"
```

Now change order status in first argument and greetings message in second arguments like below, 

```
displayOrderStatusFunc(orderStatusFunc(order), greetingsFunc())
```

the output will be now,

```javascript
console.log(displayOrderStatus) // "pizza, burger, Calzone, Ready to deliver. Warm hearted greetings for accepting our hospitality"
```

Next examine the 'Synchronous Programming: Example2'. We always wanted to display warm greetings message in first place fixed and delivery status at second place fixed in this example.

```javascript
console.log(order) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"
```

Moreover we let the each function to control other function call inside their body and thus better controlling over when to execute a function.

```javascript
const orderFunc = (item1, item2) => {
	...
	let status = orderStatusFunc(items)
	...
}

const orderStatusFunc = item => {
	if (item) {
		...
		let display = displayOrderStatusFunc(status)
		...
	}
}

const displayOrderStatusFunc = param => {
	if (param) {
		let greetings = greetingsFunc()
		...
	}
}

const greetingsFunc = () => {
	...
}

const order = orderFunc('pizza', 'burger')
```
This is how we can better control the function execution sequences when writing synchronous programming.


### D) Problems with synchronous programming
Synchronous programming is straightforward. It’s easier to write code. Basically, synchronous programming can be used when the aim is for simplicity rather than efficiency. Because synchronous programming is the default, developers don’t need to worry about whether or not it’s possible to build asynchronous applications. But when the code becomes incrementally larger it's hard to manage numerous actions, time-consuming waits, can't prevent to stop lots of execution where sequence are controlled previously, Worse user experience when massive hits of too many requests etc. We will now analyze the problems below.

#### Please see the Synchronous Programming Examples again:

```javascript
// Synchronous Programing: Example 1
const orderFunc = (item1, item2) => {
	let complimentaryItem = 'Calzone'
	let items = item1 + ', ' + item2 + ', ' + complimentaryItem 
	return items
}

const orderStatusFunc = item => {
	if (item) {
		let status = item + ', ' + 'Ready to deliver'
		return status
	}
}

const greetingsFunc = () => {
	return 'Warm hearted greetings for accepting our hospitality'
}

const displayOrderStatusFunc = (param1, param2) => {
	if (param1 && param2) {
		let display = param1 + '. ' + param2
		return display
	}
}

const order = orderFunc('pizza', 'burger')
const displayOrderStatus = displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))
console.log(displayOrderStatus) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"


// Synchronous Programing: Example 2
const orderFunc = (item1, item2) => {
	let complimentaryItem = 'Calzone'
	let items = item1 + ', ' + item2 + ', ' + complimentaryItem
	let status = orderStatusFunc(items)
	return status
}

const orderStatusFunc = item => {
	if (item) {
		let status = item + ', ' + 'Ready to deliver'
		let display = displayOrderStatusFunc(status)
		return display
	}
}

const displayOrderStatusFunc = param => {
	if (param) {
		let greetings = greetingsFunc()
		let display = greetings + '. ' + param 
		return display
	}
}

const greetingsFunc = () => {
	return 'Warm hearted greetings for accepting our hospitality'
}

const order = orderFunc('pizza', 'burger')
console.log(order) // "Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver"
```

##### The problems with the above Examples are:
a) We have to call four functions to display the result in Example1. 
###### i) orderFunc('pizza', 'burger'), 
###### ii) displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order)),
###### iii) greetingsFunc() and 
###### iv) orderStatusFunc(order) 

So, it will be nightmare to manage lots of function call in a larger application.


b) From the Example2 it is not possible to prevent the orderFunc('pizza', 'burger')  function from displaying the greetings message. That means there need more flexible and efficient controlling to manage the function sequence.


c) Blocking can make wait to display the result if delay happen in the order status function of the above code i.e. orderStatusFunc(order). In practical world dependency functions can interact with external APIs or dB based data fetched tasks. It's obvious that time-consuming wait or blocking interrupt create delay to the next function execution. So, need to handle that by writing asynchronous programming using browser based javascript engine and web APIs which we will discuss later in this article.


###### Now it's time to know about 'Callback' and next on to start the concept of 'Asynchronous'


### E) Javascript Callback Function
Callback is a function passed as an urgument to another function. The parent function which is taken the argument will utilize it or invoke it later inside it's frame after completing the other tasks. 
#### How to use Callback Function? 
##### a) Simple callback function syntax:
```javascript
// Example 1
normalFunc(callbackFunc) // "I am normal function", "I am callback function"  

function callbackFunc() {
  console.log('I am callback function')
}

function normalFunc(callbackParam) {
  console.log('I am normal function')
  callbackParam()
}

// Example 2
normalFunc(callbackFunc1, callbackFunc2) // "I am callback function2", "I am normal function", "I am callback function1"   

function callbackFunc1() {
  console.log('I am callback function1')
}

function callbackFunc2() {
  console.log('I am callback function2')
}

function normalFunc(callbackParam1, callbackParam2) {
  callbackParam2()
  console.log('I am normal function')
  callbackParam1()
}
```
Let's explain the callback function advantages of above codes
###### i) CallbackFunc() is a callback function because it's passed as argument to normalFunc(callbackFunc) function
###### ii) CallbackFunc() function passed as argument to normalFunc(callbackFunc) function without using parenthesis '()'. When passed callback function as argument remember not to use parenthesis.
###### iii) CallbackFunc() function is received as argument to normalFunc(callbackParam) function. When received callback function as argument any name can be used. i.e. callbackParam
###### iv) Inside normalFunc(callbackParam) function callbackParam() function is called after completing the parent function's other tasks or can be placed in any optimal position according development needs.
###### v) Inside normalFunc(callbackParam) function the callback argument i.e. callbackParam is now invoked as a function by using parenthesis '()' i.e. callbackParam()
###### vi) Function as a argument without parenthesis '()' i.e. normalFunc(callbackFunc) feel much as a normal parameter. So, keeping consistency, neat and clean code.
###### vii) In Example2, more than one callback can be passed. 
###### viii) In Example2, more important is where the callback functions invoked, less important is argument sequences. See the following snippets in Example2.

```javascript
function normalFunc(callbackParam1, callbackParam2) {
  callbackParam2()
  console.log('I am normal function')
  callbackParam1()
}
```
Here callback function invoked sequences are callbackParam2() and then next callbackParam1() and hence function call sequences are managed in a single function block.


###### ix) In Example2, only one function call to display the result, thus hassell free when comparing to bulk functions call. 

```javascript
normalFunc(callbackFunc1, callbackFunc2)
```


###### x) In both Examples, we can prevent the parent function from displaying the result by not passing callback arguments. So, more fine control over the functions call. 



##### b) Callback function syntax with parameter:
```javascript
// Example 1: Callback function using arguments
normalFunc(callbackFunc) // "I am normal function", "Are you callback function? Yes, I am..."  

function callbackFunc(notifyParam) {
  console.log(notifyParam + 'Yes, I am...')
}

function normalFunc(callbackParam) {
  console.log('I am normal function')
  let notify = 'Are you callback function? '
  callbackParam(notify)
}

// Example 2: Multiple callback function using arguments
normalFunc(callbackFunc1, callbackFunc2) // "I am normal function", "Are you callback function? Yes, I am callback function2", "Are you callback function? Yes, I am callback function1"   

function callbackFunc1(notifyParam) {
  console.log(notifyParam + 'Yes, I am callback function1')
}

function callbackFunc2(notifyParam) {
  console.log(notifyParam + 'Yes, I am callback function2')
}

function normalFunc(callbackParam1, callbackParam2) {
  console.log('I am normal function')
  let notify = 'Are you callback function? '
  callbackParam2(notify)
  callbackParam1(notify)
}
```
Another advantages to use callback function. 
###### xi) Both of the examples we can see when callback function passed as argument from parent call no need to mention parameter signature (parenthesis '()') rather when invoked inside parent body then need parameter.
```javascript
// Example 1: Callback function using arguments - No need parameter (parenthesis '()') to pass in callbackFunc
normalFunc(callbackFunc)

function callbackFunc(notifyParam) {
  ...
}

function normalFunc(callbackParam) {
  ...

  // Now need argument to pass
  callbackParam(notify)
}

// Example 2: Multiple callback function using arguments - No need to pass arguments (parenthesis '()') with callbackFunc1 and callbackFunc2
normalFunc(callbackFunc1, callbackFunc2) 

function callbackFunc1(notifyParam) {
  ...
}

function callbackFunc2(notifyParam) {
  ...
}

function normalFunc(callbackParam1, callbackParam2) {
  ...

  // Now need to pass arguments in both callback functions. i.e. callbackParam2(notify), callbackParam1(notify)
  callbackParam2(notify)
  callbackParam1(notify)
}
```

##### c) Callback function syntax using Anonyumous and Arrow syntax:
```javascript

// Example 1: Simple callback function call from Name Function
function simpleFunc(callback) {
  console.log('I am simple function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) // "I am simple function", "You are callback function"


same as,


// Example 2: Simple callback function call from Anonymous Function
const simpleFunc = function(callback) {
  console.log('I am anonymous function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) // "I am anonymous function", "You are callback function"


same as,


// Example 3: Simple callback function call from Arrow Function
const simpleFunc = callback => {
  console.log('I am arrow function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) // "I am arrow function", "You are callback function"


same as,


// Example 4: Anonymous callback function call from Anonymous Function
const simpleFunc = function(callback) {
  console.log('I am anonymous function')
  let message = 'You are anonymous callback function'
  callback(message)

}

const simpleCallbackFunc = function (message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) // "I am anonymous function", "You are anonymous callback function"


same as,


// Example 5: Arrow callback function call from Arrow Function
const simpleFunc = callback => {
  console.log('I am arrow function')
  let message = 'You are arrow callback function'
  callback(message)

}

const simpleCallbackFunc = message => {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) // "I am arrow function", "You are arrow callback function"


same as,


// Example 6: Callback Function defined and passed as arguments simultaneously from Parent Function 
const simpleFunc = callback => {
  console.log('I am parent function')
  let message = 'You are callback function'
  callback(message)

}

simpleFunc(message => {
  console.log(message)
}) // "I am parent function", "You are callback function"
```


It's seems little different with others in the above Example6 code. Callback function itself defined and passed concurrently as argument through parent parameter. Instead of passing the name of a function as an argument to another function, we can always pass a whole function instead.
```javascript
// Passing the whole function
simpleFunc(message => {
  console.log(message)
})
```


Enough with the callback description.  Let's see some few more examples how callback function act with the Web API things like: setTimeout() function, after that we will leap to know about 'Asynchronous Programming'
```javascript
// Example 1: setTimeout function using callback
setTimeout(a => {
  console.log('Print me after ' + a +  ' seconds')
}, 3000, '3') // Print me after 3 seconds



// Example 2: setTimeout function using callback inside from another function
const anotherFunc = () => {
  setTimeout(a => {
    console.log('I will come after ' + a +  ' seconds')
  }, 3000, '3')
}

const parentFunc = callback => {
  callback()
  console.log('Parent calling callback')
}

parentFunc(anotherFunc) // "Parent calling callback", "I will come after 3 seconds"



// Example 3: setTimeout function using callback inside from another function with external argument
const employeeFunc = countParam1 => {
  setTimeout(countParam2 => {
    console.log('Hurray! I am here after ' + countParam2 +  ' seconds')
  }, countParam1*1000, countParam1)
}

const bossFunc = callback => {
  let count = 3
  callback(count)
  console.log('Boss calling employee')
  console.log('Plz, come after 3 seconds')
}

bossFunc(employeeFunc) // "Boss calling employee", "Plz, come after 3 seconds", "Hurray! I am here after 3 seconds"
```
Did you see the shining parts are on the above codes? Let's find out the sun.

Imagine your are fetching huge size of dB request from backend API in replace of setTimeout() method. i.e. 'fetch()'. You have to wait for full response but in between the times there make no sense to postponed other stuffs as because the software will become slow even it can be night ghost if numerious fetch request happen in an application. Using callback you have triggered an action. 

###### i) The action (here callback function) will found asynchronous function (here, setTimeout(). There are others like: fetch(), setInterval, geolocation, promises etc. these are also called Web APIs)

###### ii) Javascript will hand over the asynchronous function to browser based javascript engine ( In chrome it's' V8 ) to deal with these Web API using some terminologies like: Memory Heap, Call Stack, Call Stack Queue, Event Loop (Details of these out of scope in here)

###### iii) Now Javascript for it's single-threaded architecturel nature will start to execute the next instructions of code.

###### iv) In one side browser is dealing with Web APIs and other side javascript doing it's work by executing following instructions line by line, so, concurrently happening numerous tasks.

###### v) Whenever browser ended with dealing it will blank the Call Stack Frame, back to Web API method and released, handed over the result to response in Javascript code. 

###### vi) The response are avilable now in Javascript code where it has been returned.

So, using callback we are not getting block in Javascript code. Thus, the callback function really shine where asynchronous functions are used.






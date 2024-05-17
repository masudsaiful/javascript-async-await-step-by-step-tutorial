**                                                                       **


At one time, developers wrote procedural JavaScript, meaning function-based JavaScript programming. But over time, JavaScript features and characteristics kept updating. Developers faced challenges in managing single-threaded architecture, blocking, and execution sequence issues when writing programs. They often had to write code in a cumbersome manner to control the sequence of function execution, to handle it beautifully. To overcome single-threaded issues, blocking issues, and synchronous programming problems, official JavaScript (ECMAScript) kept adding various features or characteristics at different times so that through multi-threaded, non-blocking, and asynchronous ways, many tasks could output simultaneously. This made web programming even smoother, more efficient, and developer-friendly.

Since JavaScript is inherently a single-threaded, blocking, and synchronous programming language and in subsequent versions of ECMAScript, various updated features were added. Combining these with browser-dependent features and utilizing web APIs, developers can write multi-threaded, non-blocking, and asynchronous JavaScript code. In modern JavaScript, for handling asynchronous programming, in 2015, the ES6 standard introduced the concept of Promises objects, which allow for tracking asynchronous operations. Then in 2017, ECMA introduced the Async/Await concept, which works with Promises and helps to handle asynchronous operations with even more proficiency, making it easier and more developer-friendly to write multi-threaded JavaScript code with better results.

## Before understanding Async/Await we should first need to understand the concept of the followings. More or less they are: 

A) **Javascript Functions**

B) **Single-threaded, blocking and synchronous**

C) **Function Sequence and synchronous programming**

D) **Problems with synchronous programming**

E) **Callback**

F) **multi-threaded, non-blocking and asynchronous**

G) **Problems with Asynchronous programing using Callback (Callback Hell)**

H) **Javascript Promises**

I) **Async/Await**

I) **Recap everything at a glance**


## Let's a short overview all of them:

### A) Javascript Function
#### i) Name Function
##### Declaration or Definition:
```javascript

Function has a name and declared or defined as usually:

function functionName (param1, param2, ...) {

}
```

##### Invokation or Calling:
```javascript

Function will execute when they are called or invoked like belows:

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

Javascript Function can return value and catch the value in different ways:

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

Function call declaration can be happened before their definition. This is called Function hoisting:

// Calling before defining
functionName (param1, param2, ...)

function functionName (param1, param2, ...) {
  return param1 + param2;
}
```


#### ii) Anonymous Function
##### Declaration or Definition:
```javascript

Function with no name is called Anonymous Function:

// This function has no name so it is called Anonymous Function
function (param1, param2, ...) {

}


// Anonymous Function can be defined using an expression
const m = function (param1, param2, ...) {return param1 + param2};


// Anonymous Function can be defined by assigning to a variable and later this variable will act as a function
const m = function (param1, param2, ...) {return param1 + param2};
m(param1, param2, ...)


// Anonymous Function can be defined directly as a callback function in another function (i.e. in here Web API function setTimeout())
let x = 16
let y = 9
setTimeout(function (param1, param2) { 
    console.log(param1 + param2) // 25; 
}, 1000, x, y);


NOTE: Anonymous Function can not be hoisted. They only execute when calling after declaration.

Example:
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


// Invoking directly as a callback function to another function (i.e. in here browser based Web API function setTimeout()) parameter 
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
In Javascript programming language while running code it can execute only one instruction at a time where multi-threaded programming languages can run multiple instructions at once. For single-threaded nature within the single **call stack**, Javascript code is read and gets executed line by line. Call stack concept is same as stack data structure. If you know the data structure, you will know the concept of Call stack. Whenever a line of code gets inside the call stack and whenever it's time to execute it gets executed and moves out of the stack and then next line of code and then next line of code and thus maintaining sequential execution. Let's have a look of the following example.
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
According Javascript single-threaded architecture let's track the above code sample what's happening in the single **'Call Stack'**.

a) Instructions of each line of code are added to the stack frame of single call stack in **LIFO (Last in first out)** way

b) Initial execution of **console.log(result)** as well as **z()** function

c) **z()** will wait to return until **y()** completed tasks

d) then **y()** function

e) then **x()** function

f) so, code executed sequentially one by one in only one call stack and a single memory heap and only one execution at a time

g) when execution completed, releasing the call stack from this task to empty 


##### Blocking:
Though Javascript code work sequentially and in the single-threaded stack frame, execution occur one instruction at a time, there may be very chance for the following line of instruction to wait untill it's previous execution completed. It is called **blocking**. Blocking is the nature of synchronous programming. Let's consider the following example.
```javascript
      // Example
      const x = () => {
          console.log('processing...')
          for (let p = 0; p >= 0; p++) {
              if (p == 10000000000) {
                  return p
              }
          }
      }

      const y = () => {
          return x()
      }

      const display = () => {
          return y()

      }

      let result = display()
      console.log('Result: ')
      console.log(result) // 1000000000
```
Run the program and you will see execution can take few moments to display result. 

**display()** is blocked untill **y()** completed it's task.

Same to **x()** keeping wait the execution of **y()** where **x()** itself not yet finished the task.

This **time-consuming** execution which can block it's following instruction may happen for the reason of any external **API call** or any **I/O operation** or any server end **dB connection** request or other similar issues.


##### Synchronous:
In javascript code within the synchronous calls, all the work is done line by line one after another. The first task is executed then the second task is executed, no matter how much time one task will take. When one thread is locked, the thread following it in line is blocked. After escaping from block, execution will start for the next instruction. Look at this two illustrations below.
```javascript
    // Example 1
    const func1 = () => {
        console.log('processing something1...')
        for (let p = 0; p >= 0; p++) {
            if (p == 10000000000) {
                return 'something1'
            }
        }
    }

    const func2 = () => {
        console.log('something2')
    }

    const func3 = () => {
        console.log('something3')
    }

    console.log(func1())
    func2()
    func3()

    // "processing something1..."
    // "something1"
    // "something2"
    // "something3"




    // Example 2
    const func1 = () => {
        console.log('processing something1...')
        for (let p = 0; p >= 0; p++) {
            if (p == 10000000000) {
                return 'something1'
            }
        }
    }

    const func2 = () => {
        console.log('something2')
    }

    const func3 = () => {
        console.log('something3')
    }

    func2()
    console.log(func1())
    func3()

    // something2
    // processing something1...
    // something1
    // something3

```
The code illustrated in **Example1** will print output **'something1', 'something2' and 'something3'** sequentially no matter how long the blocking (**processing something1...** will take long to execute) occur in any part inside these functions but will execute according their call sequence i.e. **func1(), func2() and func3()**


In the **Example2** we can now seen that the output sequence orders are **'something2', 'something1' and 'something3'**. This is because their function call execution occured line by line one after another according their invokation sequences and only one instruction at a time i.e. **func2(), func1() and func3()**. The noteworthy thing here is that after execution of **func2**, **func3()** will wait until **func1()** has finished the work.


### C) Function Sequence and synchronous programming
#### What we have already learned let's recape those again, 


##### Javascript is,

i) single-threaded in nature,

ii) blocking architecture and

ii) synchronous execution by default 



##### Javascript code execution happen,

i) line by line

ii) sequentially one after another

iii) only one instruction at a time 

iv) next instruction will wait untill the previous instruction completed it's task, which means blocking



##### Javascript code execution based on following terminologies and Browser based engine
(We will not go in-depth discussion in this article about the terminologies)

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
So, functions are executed in the sequence they are called, not the sequence they are defined.

Let's examine the following examples,
```javascript
//Example 1: Simple function sequences
const secondFunc = () =>  'Second';
const thirdFunc = () =>  'Third';
const firstFunc = () => 'First';


console.log(firstFunc()); // First
console.log(secondFunc()); // Second
console.log(thirdFunc()); // Third



//Example 2: Nested function sequences
const firstFunc = () => {
  const secondFunc = () => {
    const thirdFunc = () => {
      console.log('Third')
    }
    console.log('Second')
    thirdFunc()
  }
  console.log('First')
  secondFunc()
}

const fourthFunc = () => {
  console.log('Fourth')
}

const fifthFunc = () => {
  fourthFunc()
  console.log('Fifth')
}

const sixthFunc = () => {
  return 'Sixth'
}

const seventhFunc = (param) => {
  console.log(param)
  return 'Seventh'
}

firstFunc()
fifthFunc()
let six = sixthFunc()
seventhFunc(six)

// First
// Second
// Third
// Fourth
// Fifth
// Sixth
// Seventh
```
**Example1** shows simple functions execution sequentially

**Example2** shows the variations of nested function call sequences. We can call child function inside the parent body whereas child function defined outside the body (**fifthFunc()** ) or both calling and definition can be handle inside the parent body (**firstFunc()**). 

Whatever their declaration ordering are managed but result always depends on function call sequences.


#### Synchronous Programming:
As we already knew Javascript execute functions sequentially but sometimes we would like to have better control over when to execute a function. In synchronous programming we can change the function execution order by customizing and interfering the sequence of instructions of any code to fullfil the need.


Suppose we want to do an order in a restaurant, and then update the order status, and then display the order status with greetings.
We can call an order function (**orderFunc**), save the order items with extra complimentary items, and then call the status function (**orderStatusFunc**), save the order status, and then call another function (**displayOrderStatusFunc**) to display the order status using greetings function (**greetingsFunc**) to display greetings besides order status.
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


Or, we could call a order function (**orderFunc**), and let the order function call the order status function (**orderStatusFunc**), and then let the order status function call the order status display function (**displayOrderStatusFunc**). Then after let the order status display function call the greetings function (**greetingsFunc**). Let's re-write the above code as below.  
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


If you ever design patterns in OOP (Object-Oriented Programming), you may be find some similar coherence with the above examples. 

Now let's try to understand how the two examples above are functioning and how we manage a better control over when to execute functions in synchronous programming. 

If we look at in '**Synchronous Programming: Example1**' in this line,
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

The display will change now,
```javascript
console.log(displayOrderStatus) // "pizza, burger, Calzone, Ready to deliver. Warm hearted greetings for accepting our hospitality"
```

Furthermore, we can also discuss it in this way that we have called a function **orderFunc('pizza', 'burger')**, saved the result and called another function **displayOrderStatusFunc()** to use it and thus better controlling to output the result.
```javascript
const order = orderFunc('pizza', 'burger')
const displayOrderStatus = displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))
```

Next examine the '**Synchronous Programming: Example2**'.

We always wanted to display warm greetings message in first place fixed and delivery status at second place fixed. We called **greetingsFunc()** there and passed status message to control everything.

```javascript
const displayOrderStatusFunc = param => {
	if (param) {
		let greetings = greetingsFunc()
		let display = greetings + '. ' + param 
		return display
	}
}
```

Moreover, we let the each function to control other function call inside their bodies to reduce bulk function execution when initiate. Thus better controlling over when to execute the functions.

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
So far here I just want to show how we can better control the function execution sequences when writing synchronous programming.


### D) Problems with synchronous programming
Synchronous programming is straightforward. It’s easier to write code. Basically, synchronous programming can be used when the aim is for simplicity rather than efficiency. Because synchronous programming is the default, developers don’t need to worry about whether or not it’s possible to build asynchronous applications. But when the code becomes incrementally larger it's hard to manage numerous actions, time-consuming waits, Preventing problems to stop lots of function execution sequences that are controlled internally from other functions, Worse user experience when massive hits of too many requests etc. We will now analyze the problems below.

**Let's see the synchronous programming examples again**,

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

**The problems with the above Examples are**,
a) We have to call four functions to display the result in **example1**. 
###### i) orderFunc(), 
###### ii) displayOrderStatusFunc(),
###### iii) greetingsFunc() and 
###### iv) orderStatusFunc() 

So, it will be nightmare to manage lots of function call in a larger application.


b) From the **example2** it is not possible to prevent the **orderFunc()**  function from displaying the greetings message. That means there need more flexible and efficient controlling to manage the function sequence.


c) Blocking can make wait to display the result if delay happen in the order status function **orderStatusFunc(order)** of the above codes. In practical world dependency functions can interact with external APIs or dB based data fetched tasks. It's obvious that time-consuming wait or blocking interruption create delay to the next function execution. So, need to handle that behind the scene by writing asynchronous programming using browser based javascript engine and web API methods which we will discuss later in this article.


##### Now it's time to know about 'Callback' and next on to start the concept of 'Asynchronous'
### E) Javascript Callback Function
Callback is a function passed as an urgument to another function. The parent function which is taken the argument will utilize it or invoke it later inside it's frame after completing the other tasks. 
#### How to use Callback Function? 
##### a) Simple callback function syntax:
```javascript
// Example 1
normalFunc(callbackFunc)  

function callbackFunc() {
  console.log('I am callback function')
}

function normalFunc(callbackParam) {
  console.log('I am normal function')
  callbackParam()
}
// "I am normal function", "I am callback function"


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


Enough with the callback description.  

**Let's see some few more examples how callback function act with the Web API things like: setTimeout() function, after that we will leap to know about 'Multi-Threaded, Non-Blocking and Asynchronous Programming'**
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



// Example 3: setTimeout function using callback inside from another function with arguments
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
Above code mentioning in Example3 will display These two result first, **"Boss calling employee", "Plz, come after 3 seconds"**

Second, it will display **"Hurray! I am here after 3 seconds"**. Though **"callback(count)"** is called at first but will back with result after 3 seconds. This is because **setTimeout()** itself calling a full body callback function as first parameters and time count start in milisecond at second parameter. After timing reached its destination the full body callback function will execute.

**Did you see the shining parts are on the above codes? Let's find out the sun.**

Imagine your are fetching huge size of dB request from backend API in replace of setTimeout() method. i.e. 'fetch()'. You have to wait for full response but in between the times there make no sense to postponed other stuffs as because the software will become slow even it can be night ghost if numerious fetch request happen in an application. 

**Using callback you have triggered an action.** 

###### i) The action (here callback function. i.e employeeFunc and callback(count)) will found asynchronous function (here, setTimeout(). There are others like: fetch(), setInterval, geolocation, promises etc. these are also called Web APIs)

###### ii) Javascript will hand over the asynchronous function to browser based javascript engine ( In chrome it's' V8 ) to deal with these Web API using some terminologies like: Memory Heap, Call Stack, Call Stack Queue, Event Loop (Details of these out of scope in here) etc.

###### iii) Now Javascript for it's single-threaded architectural nature will start to execute the next instructions of code.

###### iv) In one side browser is dealing with Web APIs and other side javascript doing it's work by executing following instructions line by line. So, concurrently happening numerous tasks.

###### v) Whenever 'setTimeout()' timer reached the destination, browser ended with dealing. It will blank this task from Callback Queue, back to Web API method, started to help the Javascript to properly execute setTimeout() callback function, release it's activity from Web API and lastly setTimeout() return an ID of timer to Javascript code.

###### vi) Now the response are avilable to use in Javascript code later.

**Handling asynchronous functions using callback is a popular solution to make Javascript code non-blocking. Thus, the callback function really shine when use with asynchronoous programming.**


### F) Multi-threaded, Non-Blocking and Asynchronous
We have already got idea from the above parts of this article that Javascript is by default **Single-threaded, Blocking and Synchronous** programming language. But modern JavaScript has pushed this notion back and moved forward. Programmers can now be able to code multi-threaded programming with Javascript.


#### i) Multi-threaded
Lot of tasks simultaneously execution in a programming language is called multi-threaded programming. Some of multi-threaded programming languages are Java, C++, PHP etc. Javascript is not by nature multi-threaded but with the help of asynchronous funtions and browser based Javascript run time environment programmers can write multi-threaded code. Though javascript execute code line by line at a time, using asynchronous methods in javascript code can handle numerous tasks In tandemly. 

**Have a look in the following codebase that I am trying to express the Javascript's multi-threaded nature despite of it's single-threaded architecture**.

Suppose an Accounts software performs auto transaction from it's branches. Two branches act transaction in every 5 second and another branch in every 4 second. All transactions happen twice a daily. A notification system generate transaction message in every second. Accounts software got the message to display the status. Let's see the example code below.
```javascript
// Example:
const accounts = () => {
  let branch1Deposit = ''
  let branch2Deposit = ''
  let branch3Deposit = ''

  const branch1 = () => {
    branch1Deposit = 'Branch1 has no deposit'

    const branch1Account = amount => {
      branch1Deposit = amount
    }

    setTimeout(branch1Account, 5000, 'Branch1 has deposited amount1')

    setTimeout(branch1Account, 10000, 'Branch1 has deposited amount2')
  }

  const branch2 = () => {
    branch2Deposit = 'Branch2 has no deposit'

    const branch2Account = amount => {
      branch2Deposit = amount
    }

    setTimeout(branch2Account, 5000, 'Branch2 has deposited amount1')

    setTimeout(branch2Account, 10000, 'Branch2 has deposited amount2')

  }
  
 	const branch3 = () => {
    branch3Deposit = 'Branch3 has no deposit'

    const branch3Account = amount => {
      branch3Deposit = amount
    }

    setTimeout(branch3Account, 4000, 'Branch3 has deposited amount1')

    setTimeout(branch3Account, 8000, 'Branch3 has deposited amount2')

  }

  let timer = 0
  notification = () => {
    timer += 1
    if (timer <= 15) {
      console.log('Timer ' + timer + ": ")
      console.log(branch2Deposit)
      console.log(branch1Deposit)
      console.log(branch3Deposit)
      setTimeout(notification, 1000)
    }
  }

  branch2()
  branch1()
  branch3()
  notification()
}

accounts()


// Output:
"Timer 1: "
"Branch2 has no deposit"
"Branch1 has no deposit"
"Branch3 has no deposit"
"Timer 2: "
"Branch2 has no deposit"
"Branch1 has no deposit"
"Branch3 has no deposit"
"Timer 3: "
"Branch2 has no deposit"
"Branch1 has no deposit"
"Branch3 has no deposit"
"Timer 4: "
"Branch2 has no deposit"
"Branch1 has no deposit"
"Branch3 has no deposit"
"Timer 5: "
"Branch2 has no deposit"
"Branch1 has no deposit"
"Branch3 has deposited amount1"
"Timer 6: "
"Branch2 has deposited amount1"
"Branch1 has deposited amount1"
"Branch3 has deposited amount1"
"Timer 7: "
"Branch2 has deposited amount1"
"Branch1 has deposited amount1"
"Branch3 has deposited amount1"
"Timer 8: "
"Branch2 has deposited amount1"
"Branch1 has deposited amount1"
"Branch3 has deposited amount1"
"Timer 9: "
"Branch2 has deposited amount1"
"Branch1 has deposited amount1"
"Branch3 has deposited amount2"
"Timer 10: "
"Branch2 has deposited amount1"
"Branch1 has deposited amount1"
"Branch3 has deposited amount2"
"Timer 11: "
"Branch2 has deposited amount2"
"Branch1 has deposited amount2"
"Branch3 has deposited amount2"
"Timer 12: "
"Branch2 has deposited amount2"
"Branch1 has deposited amount2"
"Branch3 has deposited amount2"
"Timer 13: "
"Branch2 has deposited amount2"
"Branch1 has deposited amount2"
"Branch3 has deposited amount2"
"Timer 14: "
"Branch2 has deposited amount2"
"Branch1 has deposited amount2"
"Branch3 has deposited amount2"
"Timer 15: "
"Branch2 has deposited amount2"
"Branch1 has deposited amount2"
"Branch3 has deposited amount2"
```
**Javascript is a single-threaded programming language because**,

1) Javascript run the above code in these function sequences according their call **accounts(), branch2(), branch1(), branch3() and notification()**.

2) only one process at a time, one after another. It can't process all of the above methods simultaneously. If previous one completed then next will start.

3) Blocking may occur to stop the following processes. i.e. If **accounts()** not work for some reasons all others next execution will be hold off.


**JavaScript can create the impression of being a multi-threaded programming language because**,


**Above code we can modified as belows**.
```javascript
// Example
let message = ''
let timer = 0

const autoTrans = () => {
  let cnt = 0
  let branch1Deposit = ''
  let branch2Deposit = ''
  let branch3Deposit = ''

  const branch1 = () => {
    branch1Deposit = 'Branch1 has no deposit'

    const branch1Account = amount => {
      branch1Deposit = amount
    }

    setTimeout(branch1Account, 5000, 'Branch1 has deposited amount1')

    setTimeout(branch1Account, 10000, 'Branch1 has deposited amount2')
  }

  const branch2 = () => {
    branch2Deposit = 'Branch2 has no deposit'

    const branch2Account = amount => {
      branch2Deposit = amount
    }

    setTimeout(branch2Account, 5000, 'Branch2 has deposited amount1')

    setTimeout(branch2Account, 10000, 'Branch2 has deposited amount2')

  }
  
 	const branch3 = () => {
    branch3Deposit = 'Branch3 has no deposit'

    const branch3Account = amount => {
      branch3Deposit = amount
    }

    setTimeout(branch3Account, 4000, 'Branch3 has deposited amount1')

    setTimeout(branch3Account, 8000, 'Branch3 has deposited amount2')

  }
  
  const notification = () => {
    cnt += 1
    if (cnt <= 15) {
      message = branch1Deposit +  '\n' + branch2Deposit + '\n' + branch3Deposit + '\n'
      setTimeout(notification, 1000)
    }
  }
  
  branch1()
  branch2()
  branch3()
  notification()
}

const display = () => {
  timer += 1
  if (timer <= 15) {
  	console.log('Timer ' + timer + ":")
    console.log(message)
    setTimeout(display, 1000)
  }
}

const accounts = (callback1, callback2) => {
	callback1()
  callback2()
}

accounts(autoTrans, display)
```


#### i) Non-Blocking

```javascript

```


## Conclusion

I've endeavored to provide a concise overview of the transition from legacy JavaScript to the contemporary async/await model in this article. Instead of delving into intricate technical discussions about single-threaded or multi-threaded systems, I've focused on presenting theoretical insights alongside practical examples in a manner that's clear, elegant, and succinct.

I would be greatly pleased if anyone identifies any errors or inaccuracies within this content and notifies me through comments. Such feedback would motivate me to produce more articles in the future. 


**                                                                       **





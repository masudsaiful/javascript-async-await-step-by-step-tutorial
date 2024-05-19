**                                                                       **


At one time, developers wrote procedural JavaScript, meaning function-based JavaScript programming. But over time, JavaScript features and characteristics kept updating. Developers faced challenges in managing single-threaded architecture, blocking, and execution sequence issues when writing programs. They often had to write code in a cumbersome manner to control the sequence of function execution, to handle it beautifully. To overcome single-threaded issues, blocking issues, and synchronous programming problems, official JavaScript (ECMAScript) kept adding various features or characteristics at different times so that through multi-threaded, non-blocking, and asynchronous ways, many tasks could output simultaneously. This made web programming even smoother, more efficient, and developer-friendly.

Since JavaScript is inherently a single-threaded, blocking, and synchronous programming language and in subsequent versions of ECMAScript, various updated features were added. Combining these with browser-dependent features and utilizing web APIs, developers can write multi-threaded, non-blocking, and asynchronous JavaScript code. In modern JavaScript, for handling asynchronous programming, in 2015, the ES6 standard introduced the concept of Promises objects, which allow for tracking asynchronous operations. Then in 2017, ECMA introduced the Async/Await concept, which works with Promises and helps to handle asynchronous operations with even more proficiency, making it easier and more developer-friendly to write multi-threaded JavaScript code with better results.

## Before understanding Async/Await we should first need to understand the concept of the followings. More or less they are: 

###### A) Javascript Functions

###### B) Single-threaded, blocking and synchronous

###### C) Function Sequence and synchronous programming

###### D) Problems with synchronous programming

###### E) Callback

###### F) multi-threaded, non-blocking and asynchronous

###### G) Problems with Asynchronous programing using Callback (Callback Hell)

###### H) Javascript Promises

###### I) Async/Await

###### I) Recap everything at a glance


## Let's a short overview all of them:
###### (Please read all sections consecutively for ease of understanding. One section is inextricably linked with another section.)

### A) Javascript Function
#### i) Name Function
##### Declaration or Definition:
```javascript
Function has a name and declared or defined as usually:

function functionName (param1, param2, ...) {
  ...
}
```


##### Invokation or Calling:
```javascript
Function will execute when they are called or invoked like belows:

// inside Javascript code
<script>
  function functionName (param1, param2, ...) {
    ...
  }
  functionName(param1, param2, ...)
</script>


// basically above code will be invoked automatically by browser Window Object 
// so, above code will be the same as below
<script>
  function functionName (param1, param2, ...) {
    ...
  }
  window.functionName(param1, param2, ...)
</script>


// when an event occurs in HTML
function functionName (param1, param2, ...) {
  ...
}
<p onclick="functionName (param1, param2, ...)" />


// when an event occurs in Javascript
function functionName (param1, param2, ...) {
  ...
}
object.onclick = function(){functionName};


// when an event occurs in Javascript using Event Handler
function functionName (param1, param2, ...) {
  ...
}
object.addEventListener("click", functionName);


// invoking a function as method in Javascript Object
const Obj = {
  firstName:"f_name",
  lastName: "l_name",
  functionName: function (param1, param2, ...) {
    return this.firstName + " " + this.lastName + param1 + param2;
  }
}
Obj.functionName(param1, param2, ...);


// invoking using Function Constructor
function functionName(param1, param2, ...) {
  this.firstName = 'f_name';
  this.lastName  = "l_name";
  this.param1Key = param1;
  this.param2Key = param2;
}
const Obj = new functionName(param1, param2, ...);
Obj.param1Key;
```


##### Return Value and Catch the Value:
```javascript
Javascript Function can return value and catch the value in different ways:

// returning value statement
function functionName (param1, param2, ...) {
  return param1 + param2;
}


// returning value can assign to a variable where function is called
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let m = functionName (param1, param2, ...)


// the result value can be used in any statement or expression
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let m = functionName (param1, param2, ...)
let n = 'Something' + m


// function call can be used directly as variable value where it is invoked
function functionName (param1, param2, ...) {
  return param1 + param2;
}
let n = 'Something' + functionName (param1, param2, ...)
```


##### Hoisting:
```javascript
Function call declaration can be happened before their definition. This is called Function hoisting:

// calling before defining
functionName (param1, param2, ...)

function functionName (param1, param2, ...) {
  return param1 + param2;
}
```


#### ii) Anonymous Function
##### Declaration or Definition:
```javascript
Function with no name is called Anonymous Function:

// this function has no name so it is called Anonymous Function
function (param1, param2, ...) {
  ...
}


// anonymous Function can be defined using an expression
const m = function (param1, param2, ...) {return param1 + param2};


// anonymous Function can be defined by assigning to a variable 
// and later this variable will act as a function
const m = function (param1, param2, ...) {console.log(param1 + param2)};
m(param1, param2, ...)


Anonymous Function can be defined directly as a full body callback function 
to another function argument: 

// anonymous Function can be defined as a full body callback function 
// to a web API function argument
let x = 16
let y = 9
setTimeout(function (param1, param2) { 
    console.log(param1 + param2) 
}, 1000, x, y);

# Output: 25


// anonymous Function can be defined as a full body callback function 
// to a name function argument
function nameFunc(param) {
  return param()
}

let param1 = 16
let param2 = 9
nameFunc(function () {
  console.log(param1+param2)
})

# Output: 25


NOTE: Anonymous Function can not be hoisted. They only execute when calling after declaration.

// example: anonymous function call only work after declaration like below
const anonymousFunc = function (param1, param2, ...) {return param1 + param2};
anonymousFunc(param1, param2, ...)
```


##### Invokation or Calling:
```javascript
Function without name can be assigned to a variable. 
The variable then can be used for invokation or calling purposes:

// anonymous function invokation using variable in Javascript code
...
...
const m = function (param1, param2, ...) {return param1 + param2};
m(param1, param2, ...)
...
...


// anonymous function invokation using variable and assigning the invokation to another variable
const m = function (param1, param2, ...) {return param1 + param2};
let n = m(param1, param2, ...)


// anonymous function invokation directly In Javascript code without assigning to any another variable
...
...
const m = function (param1, param2, ...) {console.log (param1 + param2)};
m(param1, param2, ...)
...
...


// anonymous function invokation directly In a statement
const m = function (param1, param2, ...) {return param1 + param2};
let n = 'something' + m(param1, param2, ...)


// anonymous function invokation directly In an expression
const m = function (param1, param2, ...) {return param1 + param2};
console.log('something' + m(param1, param2, ...))


// anonymous function invokation as a self-invoking function
(function (param1, param2, ...) {
  let x = param1;
  let y = param2
})(param1, param2, ...);


Anonymous function invokation directly as a full body function definition to another function argument. 
It is called callback function:

// full body anonymous function definition called to a web API function argument as a callback function
let x = 16
let y = 9
setTimeout(function (param1, param2) { 
    console.log(param1 + param2) 
}, 1000, x, y);

# Output: 25


// full body anonymous function definition called to another function argument as a callback function
function nameFunc(param) {
  return param()
}

let param1 = 16
let param2 = 9
nameFunc(function () {
  console.log(param1+param2)
})

# Output: 25


Anonymous function invokation using function variable to another function argument as a callback function:

// anonymous function invokation using variable as a callback function to another function argument
let anonymousFunc = function (param1, param2) {
	return param1+param2;
}
function anotherFunction(a, b, callback) { 
	console.log(a + b + callback(a, b))
}
anotherFunction(9, 16, anonymousFunc)

# Output: 50


Though often assigned to any variable in Javascript, anonymous function variable invokation must be in 
function call format 'functionName()':

// this will return entire function definition
const arrowFuncName = function () {
  return 'Something';
}
console.log(arrowFuncName) 

# Output: () => { return 'Something'; }


// this will return correct value
const arrowFuncName = function () {
  return 'Something';
}
console.log( arrowFuncName() )

# Output: Something


Anonymous Function invokation using variable as a cllback function no need to use parenthesis '()' 
when passing, but inside the parent function need to use parenthesis '()':

// anonymous function invokation using variable as a callback function to another function argument 
// here, 'anonymousFunc' function no need to use parenthesis '()' 
// but inside the parent function anonymous function 'callback()' need to use parenthesis
let anonymousFunc = function (param1, param2) {
	return param1+param2;
}
function anotherFunction(a, b, callback) { 
	console.log(a + b + callback(a, b))
}
anotherFunction(9, 16, anonymousFunc)

# Output: 50
```


#### iii) Arrow Function
##### ES6 introduced Arrow Function in 2015:
```javascript
It's a shorter syntax for writing function expression. It's also short syntax of anonymous function:

// example 1
Anonymous Function:
function () {
  return 'something';
}

same as,

Arrow Function:
() => {
  return 'something'
}


// example 2
Anonymous Function Expression assigned to a variable:
const m = function () {return 'something'};

same as,

Arrow Function Expression assigned to a variable:
const m = () => { return 'something' };


// example 3
Anonymous Function Expression with parameter:
const m = function (param1, param2) {return param1 + param2};

same as,

Arrow Function Expression with parameter:
const m = (param1, param2) => { return param1 + param2 };


// if Arrow function has single statement and return a value, it can be written as belows
const m = (param1, param2) => param1 + param2;

NOTE: Omitted curly brackets '{}' and 'return' keyword.



// if Arrow function has single parameter and single statement, it can be written as belows
const m = param1 => 'something' + param1; 

NOTE: Omitted curly brackets '{}', 'return' keyword and parenthesis '()'.



// if Arrow function use 'return' keyword, must use curly brackets '{}'
Either a single statement:
const m = param1 => { return 'something' + param1 };

or,

multiple statement:
const m = param1 => {
  // do something
  return 'something' + param1
};



// arrow Function invokations or Callings are same as those of Anonymous Function described above



Though often assigned to any variable while working, 
arrow function variable invokation must be in function call format 'functionName()':

// this will return entire function
const arrowFuncName = () => {
  return 'Something';
}
console.log(arrowFuncName) 

# Output: () => { return 'Something'; }



// this will return correct value
const arrowFuncName = () => {
  return 'Something';
}
console.log( arrowFuncName() ) 

# Output: Something



Arrow Function invokation using variable as a cllback function, 
No need use parenthesis '()' when passing, 
but inside the parent function need to use parenthesis '()':

// arrow function invokation using variable as a callback function to another function argument 
// here, 'arrowFunc' function no need to use parenthesis '()' 
// but inside the parent function 'callback()' need to use parenthesis
let arrowFunc = (param1, param2) => {
	return param1+param2;
}
function anotherNameFunction(a, b, callback) { 
	console.log(a + b + callback(a, b))
}
anotherNameFunction(9, 16, arrowFunc)



NOTE: Though Arrow Function actually the shorter syntax of Anonymous Function, 
      it's also can't be hoisted.
```


### B) Single-threaded, blocking and synchronous
#### By default Javascript is single-threaded, blocking and synchronous nature. Let's see what are they in below.
###### (From now on towards we will use arrow functions of all following examples) ######


##### Single-threaded:
In Javascript programming language while running code it can execute only one instruction at a time where multi-threaded programming languages can run multiple instructions at once. For single-threaded nature within the single **call stack**, Javascript code is read and gets executed line by line. Call stack concept is same as stack data structure. If you know the data structure, you will know the concept of Call stack. Whenever a line of code gets inside the call stack and whenever it's time to execute it gets executed and moves out of the stack and then next line of code and then next line of code and thus maintaining sequential execution. Let's have a look of the following example.
```javascript
// example
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


According Javascript single-threaded architecture let's track the above code sample what's happening in the single **'Call Stack'**

###### a) Instructions of each line of code are added to the stack frame of single call stack in **LIFO (Last in first out)** way

###### b) Initial execution of **console.log(result)** as well as **z()** function

###### c) **z()** will wait to return until **y()** completed tasks

###### d) then **y()** function

###### e) then **x()** function

###### f) so, code executed sequentially one by one in only one call stack contexting by a single memory heap only one execution at a time

###### g) when execution completed, releasing the call stack as well as call stack frame, stack queue, event loop all are releasig from this task to empty 


##### Blocking:
Though Javascript code work sequentially and in the single-threaded stack frame, execution occur one instruction at a time, there may be very chance for the following line of instruction to wait untill it's previous execution completed. It is called **blocking**. Blocking is the nature of synchronous programming. Let's consider the following example.
```javascript
      // example
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
      console.log(result) 

      # Output: 1000000000
```


Run the program and you will see execution can take few moments to display the result. In here, 

**display()** is blocked untill **y()** completed it's task.

Same to **x()** keeping wait the execution of **y()** whereas **x()** itself not yet finished the task.

This **time-consuming** execution which can block it's following instruction may happen for the reason of any external **API call** or any **I/O operation** or any server end **dB connection** request or other similar issues.


##### Synchronous:
In javascript code within the synchronous calls, all the work is done line by line one after another. The first task is executed then the second task is executed, no matter how much time one task will take. When one thread is locked, the thread following it in line is blocked. After escaping from block, execution will start for the next instruction. Look at this two illustrations below.
```javascript
    // example 1
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

    # Output: processing something1...
              something1
              something2
              something3



    // example 2
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

    # Output: something2
              processing something1...
              something1
              something3
```


The code illustrated in **example1** will print output **'something1', 'something2' and 'something3'** sequentially no matter how long the blocking (**processing something1...** will take long to execute) occur in any part inside these functions but will execute according their call sequence i.e. **func1(), func2() and func3()**


In the **example2** we can now seen that the output sequence orders are **'something2', 'something1' and 'something3'**. This is because their function call execution occured line by line one after another according their invokation sequences and only one instruction at a time i.e. **func2(), func1() and func3()**. The noteworthy thing here is that after execution of **func2** function, the next instructed function **func1()** make delay to execute **func3()** function because **func1()** function yet not finished it's porcess.


### C) Function Sequence and synchronous programming
#### What we have learned let's recape those again 


##### Javascript is:

###### i) single-threaded in nature,

###### ii) blocking architecture and

###### ii) synchronous execution by default 


##### Javascript code execution happen,

###### i) line by line

###### ii) sequentially one after another

###### iii) only one instruction at a time 

###### iv) next instruction will wait untill the previous instruction completed it's task, which means blocking


##### Javascript code execution based on following terminologies and Browser based engine:
###### (We will not go in-depth discussion in this article about the terminologies)

###### i) Javascript run time environment

###### ii) Javascript engine

###### iii) Memory Heap

###### iv) call stack

###### v) stack frame

###### vi) LIFO

###### vii) Callback Queue

###### viii) Event Loop

###### ix) Web APIs etc.


#### Function Sequence:
So, functions are executed in the sequence they are called, not the sequence they are defined.
Let's examine the following examples,

```javascript
// example 1: Simple function sequences
const secondFunc = () =>  'Second';
const thirdFunc = () =>  'Third';
const firstFunc = () => 'First';


console.log(firstFunc());
console.log(secondFunc());
console.log(thirdFunc());

# Output: First
          Second
          Third


// example 2: Nested function sequences
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

# Output: First
          Second
          Third
          Fourth
          Fifth
          Sixth
          Seventh
```


**example1** shows simple functions execution sequentially.

**example2** shows the variations of nested function call sequences. We can call child function inside the parent body whereas child function defined outside the body (see in **fifthFunc** ) or both calling and definition can be handle inside the parent body (**firstFunc**). 

Whatever their declaration ordering are managed but result always depends on function call sequences. When doing synchronous programming it's sometimes challenging to handle and manage lots of function sequences with optimal ways. 


#### Synchronous Programming:
As we already knew Javascript execute functions sequentially but sometimes we would like to have better control over when to execute a function. In synchronous programming we can change the function execution order by customizing and interfering the sequence of instructions of any code to fullfil the need.


Suppose we want to do an order in a restaurant, and then update the order status, and then display the order status with greetings.
We can call an order function (**orderFunc**), save the order items with extra complimentary items, and then call the status function (**orderStatusFunc**), save the order status, and then call another function (**displayOrderStatusFunc**) to display the order status using greetings function (**greetingsFunc**) to display greetings besides order status.
```javascript
// synchronous Programing: example 1
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

console.log(displayOrderStatus) 

# Output: Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver
```


Or, we could call a order function (**orderFunc**), and let the order function call the order status function (**orderStatusFunc**), and then let the order status function call the order status display function (**displayOrderStatusFunc**). Then after let the order status display function call the greetings function (**greetingsFunc**). Let's re-write the above code as below.  
```javascript
// synchronous Programing: example 2
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
console.log(order) 

# Output: Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver
```


If you ever design patterns in OOP (Object-Oriented Programming), you may be find some similar coherence with the above examples. 

Now let's try to understand how the two simple examples above are functioning and how we manage a better control over when to execute functions in synchronous programming. 

If we look at in '**Synchronous Programming: example1**' in this line,
```javascript
displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))
```


it will display output the greetings message in first part and order status in second part,
```javascript
console.log(displayOrderStatus) 

# Output: Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver
```


Now change order status in first argument and greetings message in second arguments like below, 
```javascript
displayOrderStatusFunc(orderStatusFunc(order), greetingsFunc())
```


The display will change now,
```javascript
console.log(displayOrderStatus) 

# Output: pizza, burger, Calzone, Ready to deliver. Warm hearted greetings for accepting our hospitality
```


Furthermore, we can also discuss it in this way that we have called a function **orderFunc('pizza', 'burger')**, saved the result and called another function **displayOrderStatusFunc()** to use it and thus better controlling to output the result.
```javascript
const order = orderFunc('pizza', 'burger')
const displayOrderStatus = displayOrderStatusFunc(greetingsFunc(), orderStatusFunc(order))
```


Next examine the '**Synchronous Programming: example2**'.

We always wanted to display warm greetings message in first place fixed and delivery status at second place fixed. We called **greetingsFunc** there and passed status message **param** to control the expected display always in fixed order.

```javascript
const displayOrderStatusFunc = param => {
	if (param) {
		let greetings = greetingsFunc()
		let display = greetings + '. ' + param 
		return display
	}
}
```


Moreover, we let the each function to control other function call inside their bodies to reduce bulk function execution at the initialized time. Thus better controlling over when to execute the functions.

```javascript
Previous example overview how the function called inside other functions:

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


So far here, I have just tried to explain how we can better control the function execution sequences when writing synchronous programming.


### D) Problems with synchronous programming
Synchronous programming is straightforward. It’s easier to write code. Basically, synchronous programming can be used when the aim is for simplicity rather than efficiency. Because synchronous programming is the default, developers don’t need to worry about whether or not it’s possible to build asynchronous applications. But when the code becomes incrementally larger it's hard to manage numerous actions, time-consuming waits, Preventing problems to stop lots of function execution sequences that are controlled internally from other functions, Worse user experience when massive hits of too many requests etc. We will now analyze the problems below.

**Let's see the synchronous programming examples again**,

```javascript
// synchronous programing: example 1
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
console.log(displayOrderStatus) 

# Output: Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver


// synchronous programing: example 2
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
console.log(order) 

# Output: Warm hearted greetings for accepting our hospitality. pizza, burger, Calzone, Ready to deliver
```


**The problems with the above examples are**,

a) We have to call four functions to display the result in **example1**. 
###### i) orderFunc(), 
###### ii) displayOrderStatusFunc(),
###### iii) greetingsFunc() and 
###### iv) orderStatusFunc() 

So, it will be nightmare to manage lots of function call in a larger application.


b) From the **example2** it is not possible to prevent the **orderFunc()**  function from displaying the greetings message. That means there need more flexible and efficient controlling to manage the function sequence.


c) Blocking can make wait to display the result if delay happen in the order status function **orderStatusFunc(order)** of the above codes. In practical world dependency functions can interact with external APIs or dB based data fetched tasks. It's obvious that time-consuming wait or blocking interruption create delay to the next function execution. So, need to handle that behind the scene by writing asynchronous programming using browser based javascript engine and web API methods which we will discuss later in this article.


**Now it's time to know about 'Callback' and next on to start the concept of 'Asynchronous'**.

### E) Javascript Callback Function

Callback is a function passed as an urgument to another function. The parent function which is taken the argument will utilize it or invoke it later inside it's frame after completing the other tasks.

#### How to use Callback Function? 

##### a) Simple callback function syntax:

```javascript
// example 1
normalFunc(callbackFunc)  

function callbackFunc() {
  console.log('I am callback function')
}

function normalFunc(callbackParam) {
  console.log('I am normal function')
  callbackParam()
}

# Output: I am normal function, 
          I am callback function


// example 2
normalFunc(callbackFunc1, callbackFunc2)  

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

# Output: I am callback function2, 
          I am normal function, 
          I am callback function1" 
```


Let's explain the callback function advantages from above codes,

###### i) 'callbackFunc' is a callback function because it's passed as argument to parent function
###### ii) 'callbackFunc' function passed as argument to parent function without using parenthesis '()'. When passed callback function as argument remember not to use parenthesis.
###### iii) Receiving callback function can be of any name 'callbackParam'
###### iv) Receiving callback function can be utilized at any places as function invokation inside the parent function.
###### v) Function as an argument without parenthesis '()' feel much as a normal parameter passing. So, keeping code consistence, neat and clean.
###### vi) According example2, more than one callback can be passed. 
###### vii) In example2, more important is where the callback functions invoked, less important is argument sequences. See the following snippets in example2.

```javascript
function normalFunc(callbackParam1, callbackParam2) {
  callbackParam2()
  console.log('I am normal function')
  callbackParam1()
}
```


Here callback function call sequences are **callbackParam2()** and then next **callbackParam1()** and hence function call sequences are managed in a single function block.


###### viii) In example2, only one function call to display the result, thus hassell free when comparing to bulk functions call at the program initializing time. 

```javascript
normalFunc(callbackFunc1, callbackFunc2)
```


###### ix) In both examples, we can prevent the parent function from displaying the result by not passing callback arguments. So, more fine control over the functions call. 


##### b) Callback function syntax with parameter:
```javascript
// example 1: callback function using arguments
normalFunc(callbackFunc) 

function callbackFunc(notifyParam) {
  console.log(notifyParam + 'Yes, I am...')
}

function normalFunc(callbackParam) {
  console.log('I am normal function')
  let notify = 'Are you callback function? '
  callbackParam(notify)
}

# Output: I am normal function,
          Are you callback function? 
          Yes, I am...


// example 2: multiple callback function using arguments
normalFunc(callbackFunc1, callbackFunc2)   

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

# Output: I am normal function,
          Are you callback function? 
          Yes, I am callback function2, 
          Are you callback function? 
          Yes, I am callback function1
```


Another advantages to use callback function is,

###### x) Both of the examples above we can also find that parametirized callback function also don't need to use parenthesis '()' at passing time. After receiving argument and invokation time inside the parent function we have to use that.

```javascript
// example 1: parametirized single callback function at passing time
// no need to use parenthesis '()'
normalFunc(callbackFunc)

function callbackFunc(notifyParam) {
  ...
}

function normalFunc(callbackParam) {
  ...
  // now need argument to pass
  callbackParam(notify)
}

// example 2: parametirized multiple callback function at passing time
// no need to use parenthesis '()'
normalFunc(callbackFunc1, callbackFunc2) 

function callbackFunc1(notifyParam) {
  ...
}

function callbackFunc2(notifyParam) {
  ...
}

function normalFunc(callbackParam1, callbackParam2) {
  ...
  // now need to pass arguments in both callback functions. 
  // i.e. callbackParam2(notify), callbackParam1(notify)
  callbackParam2(notify)
  callbackParam1(notify)
}
```


##### c) Callback function syntax using Anonymous and Arrow syntax:
```javascript
// example 1: simple callback function call from name function
function simpleFunc(callback) {
  console.log('I am simple function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) 

# Output: I am simple function
          You are callback function


same as,


// example 2: simple callback function call from anonymous function
const simpleFunc = function(callback) {
  console.log('I am anonymous function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) 

# Output: I am anonymous function,
          You are callback function


same as,


// example 3: simple callback function call from arrow function
const simpleFunc = callback => {
  console.log('I am arrow function')
  let message = 'You are callback function'
  callback(message)

}

function simpleCallbackFunc(message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) 

# Output: I am arrow function,
          You are callback function


same as,


// example 4: anonymous callback function call from anonymous function
const simpleFunc = function(callback) {
  console.log('I am anonymous function')
  let message = 'You are anonymous callback function'
  callback(message)

}

const simpleCallbackFunc = function (message) {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) 

# Output: I am anonymous function,
          You are anonymous callback function


same as,


// example 5: arrow callback function call from arrow function
const simpleFunc = callback => {
  console.log('I am arrow function')
  let message = 'You are arrow callback function'
  callback(message)

}

const simpleCallbackFunc = message => {
  console.log(message)
}

simpleFunc(simpleCallbackFunc) 

# Output: I am arrow function,
          You are arrow callback function


same as,


// example 6: callback function defined and passed simultaneously as arguments to parent function 
const parentFunc = callback => {
  console.log('I am parent function')
  let message = 'You are callback function'
  callback(message)

}

parentFunc(message => {
  console.log(message)
}) 

# Output: I am parent function,
          You are callback function
```


It's seems little different with others in the above **example6** code. Callback function itself defined and passed concurrently as argument through parent function. Instead of passing the name of a function as an argument to another function, we can always pass a whole function instead.
```javascript
// passing the whole function
parentFunc(message => {
  console.log(message)
})


// passing the whole function to setTimeout web API function
setTimeout((message) => {
  console.log(message)
}, 1000, message)
```


Enough with the callback description. Now,  

Let's see some few more examples how callback function act with the **Web API** things like: **setTimeout() function**. After that we will leap to know about **Multi-Threaded, Non-Blocking and Asynchronous Programming**

```javascript
// example 1: setTimeout function using callback
setTimeout(a => {
  console.log('Print me after ' + a +  ' seconds')
}, 3000, '3') 

# Output: Print me after 3 seconds



// example 2: setTimeout function using callback inside from another function
const anotherFunc = () => {
  setTimeout(a => {
    console.log('I will come after ' + a +  ' seconds')
  }, 3000, '3')
}

const parentFunc = callback => {
  callback()
  console.log('Parent calling callback')
}

parentFunc(anotherFunc) 

# Output: Parent calling callback,
          I will come after 3 seconds



// example 3: setTimeout function using callback inside from another function with arguments
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

bossFunc(employeeFunc) 

# Output: Boss calling employee,
          Plz, come after 3 seconds,
          Hurray! I am here after 3 seconds
```


All of the above examples we have used **setTimeout** functions which are calling the whole callbacks in their arguments. The callback functions start execution after the providing time-out arguments given above are meets their criteria. 

Consider the **example3**. Two scenarios you can have seen.

Firstly, it will display these two messages, 

**Boss calling employee**,

**Plz, come after 3 seconds**.

Secondly, Javascript runtime environment engine (like: **v8** for **Chrome Browser**) take care to handle **setTimeout** web API function.

after 3 seconds it will display the following message,

**Hurray! I am here after 3 seconds**

Though we have called firstly **callback(count)** function in the following line of code, 

```javascript
const bossFunc = callback => {
  let count = 3
  callback(count)
  console.log('Boss calling employee')
  console.log('Plz, come after 3 seconds')
}
```
instead of displaying the following line first,

**Hurray! I am here after 3 seconds**

these two lines is displaying first,

**Boss calling employee**,

**Plz, come after 3 seconds**.

it is because of using asynchronous function **setTimeout** which will execute a callback funtion after a given period of time.

Parallelly Javascript will continue its execution synchronously and let the Javascript engine to do it's jobs in the background to handle asynchronous methods. By taking control of the result of asynchronous operations using a callback mechanism, synchronous JavaScript greatly improves execution efficiency.

**Now you may have seen the callback function greatly shine when it is executed by an asynchronous function**.

Imagine your are fetching huge size of dB request from backend API. In blocking and synchronous mechanism you have to wait for full dB response but in between the times there make no sense to postponed other stuffs as because the software will become slow even it can be night ghost if numerious request happen to backend server in an application. Implementing callback action using asynchronous functions like: **fetch()**, server requests will continue jobs behind the scene while Javascript code execution continue sequentially. Browser finishing the asynchronous tasks let the response to take over by callback to know Javascript that it has done the works. 

**It can simply says as belows**,

###### Using asynchronous function a callback action can be triggered to perform pre or subsequent related tasks.

###### Callback actions are kinda providing breeze between gaps of synchronous and asynchronous operations.

###### Using asynchronous with callback the flow in execution will not be interrupted. 


Handling asynchronous functions using callback is a popular solution to make Javascript code non-blocking. Developers can use it to control long running tasks in the background while the other instructions continue executing. There may sometimes need to adopt of heavy lifting of callback uses or too much nested callbacks call then everything becomes difficult and hard to manage which is called **Callback Hell**. We will discuss that part later.  




### F) Multi-threaded, Non-Blocking and Asynchronous
We have already got idea from the above parts of this article that Javascript is by default **Single-threaded, Blocking and Synchronous** programming language. But modern JavaScript has pushed this notion back and moved forward. Programmers can now be able to code multi-threaded programming with Javascript.


#### i) Multi-threaded
Lot of tasks simultaneously execution in a programming language is called multi-threaded programming. Some of multi-threaded programming languages are Java, C++, PHP etc. Javascript is not by nature multi-threaded but with the help of asynchronous funtions and browser based Javascript run time environment programmers can write multi-threaded code. Though javascript execute code line by line at a time, using asynchronous methods in javascript code can handle numerous tasks In tandemly. 

**Have a look in the following codebase that I am trying to express the Javascript's multi-threaded nature despite of it's single-threaded architecture**.

Suppose an Accounts software performs auto transaction from it's branches. Two branches act transaction in every 5 second and another branch in every 4 second. All transactions happen twice a daily. A notification system generate transaction message in every second. Accounts software got the message to display the status. Let's see the example code below.
```javascript
// example:
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

# Output:
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
// example
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





**                                                                       **


At one time, developers wrote procedural JavaScript, meaning function-based JavaScript programming. But over time, JavaScript features and characteristics kept updating. Developers faced challenges in managing single-threaded architecture, blocking, and execution sequence issues when writing programs. They often had to write code in a cumbersome manner to control the sequence of function execution, to handle it beautifully. To overcome single-threaded issues, blocking issues, and synchronous programming problems, official JavaScript (ECMAScript) kept adding various features or characteristics at different times so that through multi-threaded, non-blocking, and asynchronous ways, many tasks could output simultaneously. This made web programming even smoother, more efficient, and developer-friendly.

Since JavaScript is inherently a single-threaded, blocking, and synchronous programming language and in subsequent versions of ECMAScript, various updated features were added. Combining these with browser-dependent features and utilizing web APIs, developers can write multi-threaded, non-blocking, and asynchronous JavaScript code. In modern JavaScript, for handling asynchronous programming, in 2015, the ES6 standard introduced the concept of Promises objects, which allow for tracking asynchronous operations. Then in 2017, ECMA introduced the Async/Await concept, which works with Promises and helps to handle asynchronous operations with even more proficiency, making it easier and more developer-friendly to write multi-threaded JavaScript code with better results.

## Before understanding Async/Await we should first need to understand the concept of the followings. More or less they are: 

###### A) [Javascript Functions](#a-javascript-functions-1)

###### B) [Single-threaded, blocking and synchronous](#b-single-threaded-blocking-and-synchronous-1)

###### C) [Function Sequence and synchronous programming](#c-function-sequence-and-synchronous-programming-1)

###### D) [Problems with synchronous programming](#d-problems-with-synchronous-programming-1)

###### E) [Callback](#e-javascript-callback-function)

###### F) [multi-threaded, non-blocking and asynchronous](#f-multi-threaded-non-blocking-and-asynchronous-1)

###### G) [Problems with Asynchronous programing using Callback (Callback Hell)](#g-problems-with-asynchronous-programing-using-callback-callback-hell-1)

###### H) [Javascript Promises](#h-javascript-promises-1)

###### I) [Async/Await](#i-javascript-asyncawait)




## Let's a short overview all of them:
###### (Please read all sections consecutively for ease of understanding. One section is inextricably linked with another section.)

### A) Javascript Functions
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
// so, above code will be the same as belows
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

// example: anonymous function call only work after declaration like belows
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
#### By default Javascript is single-threaded, blocking and synchronous nature. Let's see what are they in belows.
###### (From now on towards we will use arrow functions of all following examples) ######


##### Single-threaded:
In Javascript programming language while running code it can execute only one instruction at a time where multi-threaded programming languages can run multiple instructions at once. For single-threaded nature within the single **call stack**, Javascript code is read and gets executed line by line. Call stack concept is same as stack data structure. If you know the data structure, you will know the concept of Call stack. Whenever a line of code gets inside the call stack and whenever it's time to execute, it gets executed and moves out of the stack and then next line of code and then next line of code and thus maintaining sequential execution. Let's have a look of the following example.
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
In javascript code within the synchronous calls, all the work is done line by line one after another. The first task is executed then the second task is executed, no matter how much time one task will take. When one thread is locked, the thread following it in line is blocked. After escaping from block, execution will start for the next instruction. Look at this two illustrations belows.
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
So, functions are also executed in the sequence they are called, not the sequence they are defined.
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


Or, we could call a order function (**orderFunc**), and let the order function call the order status function (**orderStatusFunc**), and then let the order status function call the order status display function (**displayOrderStatusFunc**). Then after let the order status display function call the greetings function (**greetingsFunc**). Let's re-write the above code as belows.  
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


Now change order status in first argument and greetings message in second arguments like belows, 
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
Synchronous programming is straightforward. It’s easier to write code. Basically, synchronous programming can be used when the aim is for simplicity rather than efficiency. Because synchronous programming is the default, developers don’t need to worry about whether or not it’s possible to build asynchronous applications. But when the code becomes incrementally larger it's hard to manage numerous actions, time-consuming waits, Preventing problems to stop lots of function execution sequences that are controlled internally from other functions, Worse user experience when massive hits of too many requests etc. We will now analyze the problems belows.

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


#### Web APIs and Callback Function?   

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

Suppose an Accounts software performs auto transaction from it's branches. Two branches act transaction in every 5 second and another branch in every 4 second. All transactions happen twice a daily. A notification system generate transaction message in every second. Accounts software got the message to display updated status of when which branch performed auto transaction. 

**Let's see the example code belows**,
```javascript
// example:
const accounts = () => {
  let depositResult = ''

  const accountHelper = (param, amount) => {
    const helper = depositResult.split('\n').map(function(line) {
      if (line.indexOf(param) == -1) {
        return line
      } else {
        return line.replace(line, amount)
      }
    }).join('\n')

    return helper
  }

  const branch1 = (param) => {
    depositResult += param + ' has no deposit \n'

    const branch1Account = amount => {
      depositResult = accountHelper(param, amount)
    }

    setTimeout(branch1Account, 5000, 'Branch1 has deposited amount1')
    setTimeout(branch1Account, 10000, 'Branch1 has deposited amount2')
  }

  const branch2 = (param) => {
    depositResult += param + ' has no deposit \n'

    const branch2Account = amount => {
      depositResult = accountHelper(param, amount)
    }

    setTimeout(branch2Account, 5000, 'Branch2 has deposited amount1')
    setTimeout(branch2Account, 10000, 'Branch2 has deposited amount2')
  }

  const branch3 = (param) => {
    depositResult += param + ' has no deposit \n'

    const branch3Account = amount => {
      depositResult = accountHelper(param, amount)
    }

    setTimeout(branch3Account, 4000, 'Branch3 has deposited amount1')
    setTimeout(branch3Account, 8000, 'Branch3 has deposited amount2')
  }

  let timer = 0
  notification = () => {
    timer += 1
    if (timer <= 15) {
      console.log('Timer ' + timer + ": ")
      console.log(depositResult)
      setTimeout(notification, 1000)
    }
  }

  branch2('Branch2')
  branch1('Branch1')
  branch3('Branch3')
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

1) Javascript run the above code in these function sequences according their call, 

**accounts()**, 

**branch2()**,

**branch1()**, 

**branch3()** and 

**notification()**

2) only one process at a time, one after another. It can't process all of the above methods simultaneously. If previous one completed then next will start it's tasks as follows,

**accounts()** initialize the execution 

**branch2()** start to process it's code block like belows,

      1) assigning message to variable

      2) initializing asynchronous function

      3) browser taking responsibility to handle asynchronous task contexting by memory heap

      4) callback waiting to take responsibility when web API is done

      5) Javascript won't wait during asynchronous task rather continue next **branch1** execution

      6) Javascript will talk to the callback response

**branch1()** will start next ...

**branch3()** will start next ...

**notification()** running on a loop through **setTimeout** function as a callback in every second will display updated messages.

All the **branch** functions execution occured according Javascript single-threaded architecture that's why we are getting transaction results in every second by these sequences,

**branch2()**

**branch1()**

**branch3()**

meanwhile, all the **branch** asynchronous functions that are doing auto transacton tasks are running in the background using **setTimeout** periods and thus updating the notification messages of that periods which we get to know in every seconds.

So, it can easily be detect from the above lines of code that, despite of it's single-threaded architecture, Javascript also come to light in with it's multi-threaded architectural flavour using aynchronous mechanism.



#### ii) non-blocking
Consider a manufacturing company. For their regular production they have to maintain an automation system to monitor the quality standards line up with the following procedure. The quality standard tests are several steps and depends on each other. If one step delay then other following steps will be off until the previous step passed. 


**The automation flow should be like this**,

    Production

        Quality Standard Test

            - Requirements Standard Check

            - Raw Materials Check

            - Tools and Equipments Check

            - Corrective Actions and Implementation Check

        Quality Standard Check Completed


We will first try to do a simple sample code in **synchronous** way and then **asynchronous** way for better understanding the difference of Javascript **blocking** and **non-blocking** scopes.

**Let's do the code in synchronous way using callback**,

```javascript
const automation = (productionCallback) => {
  return productionCallback()
}

const production = (qualityCallback) => {
  const quantity = 'Production Capacity: 100 \n\n'
  return qualityCallback(quantity)
}

const quality = (callback, quantity) => {
  const qualityStatus = quantity + 'Quality Standard Status: \n\n'
  return callback(qualityStatus)
}

const display = automation(() => {
  return production((quantity) => {
    return quality((qualityStatus) => {
      let status = ''
      const requirements = (status) => {
        for (let i = 0; i >= 0; i++) {
          if (i == 1999999999) {
            return status + 'requirements: pass \n\n'
          }
        }
      }

      const materials = (status) => {
        return status + 'materials: pass \n'
      }

      const equipments = (status) => {
        return status + 'equipments: pass \n'
      }

      const correctives = (status) => {
        return status + 'correctives: pass \n'
      }

      status = materials(status)
      status = equipments(status)
      status = correctives(status)
      status = requirements(status)

      console.log(qualityStatus)
      console.log(status)
      console.log('Quality Standard Check Completed')

      return ''

    }, quantity)
  })
})

console.log(display)


# Output:

Production Capacity: 100 
Quality Standard Status: 

materials: pass 
equipments: pass 
correctives: pass 
requirements: pass 

Quality Standard Check Completed
```
If we run the programme we can see that the output will take few seconds to display the result as there are some delay happening while **requirements** quality standard testing function is running. This causes the next lines of instructions and logs remaining off. Here actually occured **blocking** for the following lines of execution. The returning value fell in a loop condition in the **requirements** function to take sometimes to return the value. When the loop ends, it will return a value, and consequently, a chain of other function blocks will be executed.

```javascript
  ...
  ...
  const requirements = (status) => {
    for (let i = 0; i >= 0; i++) {
      if (i == 1999999999) {
        return status + 'requirements: pass \n\n'
      }
    }
  }
  ...
  ...
```

Before converting the above code snippet in **asynchronous** way and **non-blocking** let's first think what should be the desire output that we are expecting. Well, Though there are several quality standard testing the company prefer for their production line up to go smoothly thats are **requirements**, **materials**, **equipments**, and **correctives**. We surely don't want to be off the others QA checking rather **requirements** will continue it's delay result and others QA standard testing will be running on paralally. When all of the testing results will come, the QA standards Testing will be completed. We only be able to output the result **asynchronously** with the help of **web API** method and by using **callback** mechanism.

**Let's customize the code in aynchronous way using web API method and callback function**,

```javascript
const automation = (productionCallback) => {
  return productionCallback()
}

const production = (qualityCallback) => {
  const quantity = 'Production Capacity: 100 \n\n'
  return qualityCallback(quantity)
}

const quality = (callback, quantity) => {
  const qualityStatus = quantity + 'Quality Standard Status: \n\n'
  return callback(qualityStatus)
}

const display = automation(() => {
  return production((quantity) => {
    return quality((qualityStatus) => {
      let status = ''
      const requirements = (status) => {
        for (let i = 0; i >= 0; i++) {
          if (i == 1999999999) {
            return status + 'requirements: pass \n\n'
          }
        }
      }

      const materials = (status) => {
        return status + 'materials: pass \n'
      }

      const equipments = (status) => {
        return status + 'equipments: pass \n'
      }

      const correctives = (status) => {
        return status + 'correctives: pass \n'
      }

      status = materials(status)
      status = equipments(status)
      status = correctives(status)

      reqStatus = ''
      const intervalID = setInterval(() => {
        reqStatus = requirements('')
        if (reqStatus !== '') {
          console.log(reqStatus)
          console.log('Quality Standard Check Completed')
          clearInterval(intervalID)
        }
      }, 1000)

      console.log(qualityStatus)
      console.log(status)
      console.log('Quality Standard Check Incomplete')

      return ''

    }, quantity)
  })
})

console.log(display)

## Output1: First time it will display as belows:

Production Capacity: 100 
Quality Standard Status: 
materials: pass 
equipments: pass 
correctives: pass 
Quality Standard Check Incomplete

## Output2: After a while it will display as belows:

requirements: pass 
Quality Standard Check Completed
```
From the article we have already learned many times that Javascript execute it's code line by line, one after another sequentially and only one execution at a time. That's why the automation system above will execute these three functions sequentially **materials**, **equipments**, **correctives**. In previous example the next sequence was **requirements** function that causes **blocking** for the rest of the code chain and logs. In here **requirements** function call implemented by a **web API** method **setInterval** which will run in every second and checks for any particular value returned by the **requirements** function. 
```javascript
    ...
    ...
    reqStatus = ''
    const intervalID = setInterval(() => {
      reqStatus = requirements('')
      if (reqStatus !== '') {
        console.log(reqStatus)
        console.log('Quality Standard Check Completed')
        clearInterval(intervalID)
      }
    }, 1000)
    ...
    ...
```

Paralally Javascript executing finctions line by line sequentially and web APIs asynchronous methods executing time-taking functions by browser based Javascript engine with the help of event loop, call stack and memory heap. So, we can see all of the desire output and logs in non-blocking manner yet the time-consuming **requirements** function is dealing with **setInterval** web APIs without blocking the others. Thus we can realize how Javascript act as a non-blocking architectural language. 

#### iii) asynchronous
Despite of its single-threaded architecture, Javascript perform paralally multiple executions using web API methods that we have just seen in the above code example. So, sequentially lots of tasks executing simultaneously handling by browser based Javascript run time environment technically minimize the blocking issues and given output feel like multi-threaded programming behind the scene but still be able to be responsive to other events while that task runs is called asynchronous programming.



### G) Problems with Asynchronous programing using Callback (Callback Hell)
From here on, the section will get a bit longer as we dive into transforming a basic program into a more complex one. Eventually, we will explore how callback hell can complicate our coding experience significantly. Now, Let's begin side by side with a story upon which we'll base our program's transformation step by step.

**Story: Chapter1** - Imagine a Club asks its coach to select a team using a lottery system and then use another lottery system to assign dressing room lockers to the chosen players. Player selection will occur sequentially, as will locker selection.
```javascript
    const parentFunc = () => {
      setTimeout(() => {
        console.log('Player Selection Lottery System: \n')
        console.log('Player1: A')
      }, 1000)

      setTimeout(() => {
        console.log('Player2: B')
      }, 2000)

      setTimeout(() => {
        console.log('Player3: C')
      }, 3000)

      setTimeout(() => {
        console.log('Locker Selection Lottery System:')
        console.log('Player1: X')
      }, 4000)

      setTimeout(() => {
        console.log('Player2: Y')
      }, 5000)

      setTimeout(() => {
        console.log('Player3: Z')
      }, 6000)
    }

    parentFunc()


# Output:

Player Selection Lottery System: 
Player1: A
Player2: B
Player3: C

Locker Selection Lottery System:
Player1: X
Player2: Y
Player3: Z
```
Very simple example. We just used **setTimeout** of different time-out parameters to manage display sequentially.

**Story: Chapter2** - Upon reviewing the program, it appears that after manual selection, only the information is sequentially presented, which isn't automated. So, the programmers decided the selection part will be processed using a **random method** to ensure that the desired players are chosen from a pool of many players and thus the lockers for the selected players.
```javascript
const parentFunc = () => {
  players = ['A', 'B', 'C', 'D']
  lockers = ['W', 'X', 'Y', 'Z']

  setTimeout(() => {
    console.log('Player Selection Lottery System:')
    selected = Math.floor(Math.random() * players.length)
    selected = players[selected]
    console.log('Player1: ' + selected)
    players.splice(players.indexOf(selected), 1)
  }, 1000)

  setTimeout(() => {
    selected = Math.floor(Math.random() * players.length)
    selected = players[selected]
    console.log('Player2: ' + selected)
    players.splice(players.indexOf(selected), 1)
  }, 2000)

  setTimeout(() => {
    selected = Math.floor(Math.random() * players.length)
    selected = players[selected]
    console.log('Player3: ' + selected)
    players.splice(players.indexOf(selected), 1)
  }, 3000)

  setTimeout(() => {
    console.log('Locker Selection Lottery System:')
    selected = Math.floor(Math.random() * lockers.length)
    selected = lockers[selected]
    console.log('Player1: ' + selected)
    lockers.splice(lockers.indexOf(selected), 1)
  }, 4000)

  setTimeout(() => {
    selected = Math.floor(Math.random() * lockers.length)
    selected = lockers[selected]
    console.log('Player2: ' + selected)
    lockers.splice(lockers.indexOf(selected), 1)
  }, 5000)

  setTimeout(() => {
    selected = Math.floor(Math.random() * lockers.length)
    selected = lockers[selected]
    console.log('Player3: ' + selected)
    lockers.splice(lockers.indexOf(selected), 1)
  }, 6000)
}

parentFunc()


# Output:

Player Selection Lottery System:
Player1: D
Player2: A
Player3: B

Locker Selection Lottery System:
Player1: X
Player2: Z
Player3: W
```

**Story: Chapter3** - Team has performed well. They are delighted that both players and lockers are being automatically selected from the pool using **random** functions. But the code reviewers team didn't happy. Their point is clear: we will provide our clients with the best product possible. Here, the **repetition** of the **random function** won't be permissible. It must be encapsulated within a method. So, let's do it.

```javascript
const parentFunc = () => {
  players = ['A', 'B', 'C', 'D']
  const randomPlayers = (players) => {
    selected = Math.floor(Math.random() * players.length)
    selected = players[selected]
    players.splice(players.indexOf(selected), 1)
    return selected
  }

  lockers = ['W', 'x', 'Y', 'Z']
  const randomLockers = (lockers) => {
    selected = Math.floor(Math.random() * lockers.length)
    selected = lockers[selected]
    lockers.splice(lockers.indexOf(selected), 1)
    return selected
  }

  setTimeout(() => {
    console.log('Player Selection Lottery System:')
    console.log('Player1: ' + randomPlayers(players))
  }, 1000)

  setTimeout(() => {
    console.log('Player2: ' + randomPlayers(players))
  }, 2000)

  setTimeout(() => {
    console.log('Player3: ' + randomPlayers(players))
  }, 3000)

  setTimeout(() => {
    console.log('locker Selection Lottery System:')
    console.log('Player1: ' + randomLockers(lockers))
  }, 4000)

  setTimeout(() => {
    console.log('Player2: ' + randomLockers(lockers))
  }, 5000)

  setTimeout(() => {
    console.log('Player3: ' + randomLockers(lockers))
  }, 6000)
}

parentFunc()


# Output:

Player Selection Lottery System:
Player1: D
Player2: C
Player3: B

locker Selection Lottery System:
Player1: W
Player2: Z
Player3: x
```

**Story: Chapter4** - Inspite of separating the **randomLockers** and **randomPlayers** functions in the above code, developers find themselves facing the team leader again, receiving feedback from code reviewers. Now, the **random functions** which are executing to output the lottery system result need to be defined as separate independent functions outside the **parent** function scope entirely. Besides these it's not looking so good that all **setTimeout** functions are defined serially with different time-out parameter. So, these need to be encapsulated in such a way that all **setTimeout** functions are compacted into a **centrally managed** **callback** function, which receives a **timeout** parameter that can be passed to all its **nested child** functions parameter also. This way lottery display should maintain by the **setTimeout** function sequentially.
```javascript
players = ['A', 'B', 'C', 'D']
const randomPlayers = (param1 = null) => {
  selected = Math.floor(Math.random() * param1.length)
  selected = param1[selected]
  param1.splice(param1.indexOf(selected), 1)
  return selected
}

lockers = ['W', 'x', 'Y', 'Z']
const randomLockers = (param2) => {
  selected = Math.floor(Math.random() * param2.length)
  selected = param2[selected]
  param2.splice(param2.indexOf(selected), 1)
  return selected
}

const parentFunc = (callback1, callback2, param1, param2, timeout) => {
  setTimeout(() => {
    console.log('Player Selection Lottery System:')
    console.log('Player1: ' + callback1(param1))
    setTimeout(() => {
      console.log('Player2: ' + callback1(param1))
      setTimeout(() => {
        console.log('Player3: ' + callback1(param1))
        setTimeout(() => {
          console.log('Lockers Selection Lottery System:')
          console.log('Player1: ' + callback2(param2))
          setTimeout(() => {
            console.log('Player2: ' + callback2(param2))
            setTimeout(() => {
              console.log('Player3: ' + callback2(param2))
            }, timeout)
          }, timeout)
        }, timeout)
      }, timeout)
    }, timeout)
  }, timeout)
}

parentFunc(randomPlayers, randomLockers, players, lockers, 1000)

# Output :

Player Selection Lottery System:
Player1: B
Player2: A
Player3: D

Lockers Selection Lottery System:
Player1: W
Player2: Y
Player3: x
```

**Story: Chapter5** - The review team remarked that the above code looks much better than before, and a **pyramid structure** seems to be forming. After discussing with the team leader, it was decided that the display logs should be managed through a separate **display** function and the **setTimeout** functions should only produce sequential output. The client also decided that the lottery system should be automated to handle 7-8 players. Besides these it was also decided that the selected locker should indicate the related player at output result. Developer started their work In full swing.
```javascript
players = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
const randomPlayers = (param1 = null) => {
  selected = Math.floor(Math.random() * param1.length)
  selected = param1[selected]
  param1.splice(param1.indexOf(selected), 1)
  return selected
}

lockers = ['S', 'T', 'U', 'V', 'W', 'x', 'Y', 'Z']
const randomLockers = (param2) => {
  selected = Math.floor(Math.random() * param2.length)
  selected = param2[selected]
  param2.splice(param2.indexOf(selected), 1)
  return selected
}

const display = (displayCallback1, displayCallback2, displayParam1, displayParam2) => {
  playerName = displayCallback1(displayParam1)
  lockerName = displayCallback2(displayParam2)
  console.log('Player ' + playerName + ' : ' + 'Locker ' + lockerName)
}

const parentFunc = (callback1, callback2, param1, param2, timeout) => {
  console.log('Players : Lockers')
  setTimeout(() => {
    display(callback1, callback2, param1, param2)
    setTimeout(() => {
      display(callback1, callback2, param1, param2)
      setTimeout(() => {
        display(callback1, callback2, param1, param2)
        setTimeout(() => {
          display(callback1, callback2, param1, param2)
          setTimeout(() => {
            display(callback1, callback2, param1, param2)
            setTimeout(() => {
              display(callback1, callback2, param1, param2)
              setTimeout(() => {
                display(callback1, callback2, param1, param2)
                setTimeout(() => {
                  display(callback1, callback2, param1, param2)
                }, timeout)
              }, timeout)
            }, timeout)
          }, timeout)
        }, timeout)
      }, timeout)
    }, timeout)
  }, timeout)
}

parentFunc(randomPlayers, randomLockers, players, lockers, 1000)


# Output:

Players : Lockers
Player C : Locker x
Player F : Locker T
Player D : Locker V
Player B : Locker Z
Player H : Locker Y
Player A : Locker U
Player G : Locker W
Player E : Locker S
```
Befor on next story chapters, Let's dig into what the above code is doing. 

We have called **parentFunc**,
```javascript
parentFunc(randomPlayers, randomLockers, players, lockers, 1000) 
```

The function received the arguments,
```javascript
const parentFunc = (callback1, callback2, param1, param2, timeout) => { 
  ...
  ...
}
```

A chain of **setTimeout** functions inside each other of their **callback** to display output sequentially,
```javascript
const parentFunc = (callback1, callback2, param1, param2, timeout) => {
  console.log('Players : Lockers')
  setTimeout(() => {
    display(callback1, callback2, param1, param2)
    setTimeout(() => {
      display(callback1, callback2, param1, param2)
      ...
      ...
    }, timeout)
  }, timeout)
```

Each **setTimeout** function called **display** function like the below code where **display** function uses parameters from **parentFunc** function. The parameters are **callback1**, **callback2**, **param1**, **param2**, **timeout**. **timeout** is set as commonly to all **setTimeout** parameters.
```javascript
const parentFunc = (callback1, callback2, param1, param2, timeout) => {
  console.log('Players : Lockers')
  setTimeout(() => {
    display(callback1, callback2, param1, param2)
    setTimeout(() => {
      display(callback1, callback2, param1, param2)
      ...
      ...
    }, timeout)
  }, timeout)
```

**display** function received these arguments like the below code, where **displayCallback1** is actually calling **randomPlayers**, **displayCallback2** actually calling **randomLockers**, **displayParam1** actually calling **players** array and **displayParam2** calling **lockers** array. So, receiving output by **randomPlayers** and **randomLockers** functions are assigned to the variables **playerName** and **lockerName** respectively, and are displayed sequentially through the **setTimeout** function.
```javascript
const display = (displayCallback1, displayCallback2, displayParam1, displayParam2) => {
  playerName = displayCallback1(displayParam1)
  lockerName = displayCallback2(displayParam2)
  console.log('Player ' + playerName + ' : ' + 'Locker ' + lockerName)
}
```

**Story: Chapter6** - The review team and the team leader are still not satisfied. Despite all the changes, problems persist. The parent function is not completely free of display logs (**see the code below**).
```javascript
...
...
const parentFunc = (callback1, callback2, param1, param2, timeout) => {
  console.log('Players : Lockers')
  ...
  ...
}
...
...
```
Additionally, it was mentioned that everything should be controlled through a **centrally managed callback function**. By using centrally managed callback function, extra features or logs can be attached without interference inside the **parentFunc** function definition and thus it will be executed standalonely. The developer team jumped back into work, determined to get everything perfect this time. As they started handling **nested callback**, they suddenly **lost track**. **Maintaining** the code became **challenging**. They frequently confront **tough challenges** when reviewing their own code, despite it being their own creation. At the end they were able to produce an output.
```javascript
players = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
const randomPlayers = (param1) => {
  selected = Math.floor(Math.random() * param1.length)
  selected = param1[selected]
  param1.splice(param1.indexOf(selected), 1)
  return selected
}

lockers = ['S', 'T', 'U', 'V', 'W', 'x', 'Y', 'Z']
const randomLockers = (param2) => {
  selected = Math.floor(Math.random() * param2.length)
  selected = param2[selected]
  param2.splice(param2.indexOf(selected), 1)
  return selected
}

const display = (displayCallback1, displayCallback2, displayParam1, displayParam2) => {
  playerName = displayCallback1(displayParam1)
  lockerName = displayCallback2(displayParam2)
  console.log('Player ' + playerName + ' : ' + 'Locker ' + lockerName)
}

const parentFunc = (parentCallback) => {
  parentCallback((callback1, callback2, param1, param2, timeout) => {
    setTimeout(() => {
      display(callback1, callback2, param1, param2)
      setTimeout(() => {
        display(callback1, callback2, param1, param2)
        setTimeout(() => {
          display(callback1, callback2, param1, param2)
          setTimeout(() => {
            display(callback1, callback2, param1, param2)
            setTimeout(() => {
              display(callback1, callback2, param1, param2)
              setTimeout(() => {
                display(callback1, callback2, param1, param2)
                setTimeout(() => {
                  display(callback1, callback2, param1, param2)
                  setTimeout(() => {
                    display(callback1, callback2, param1, param2)
                  }, timeout)
                }, timeout)
              }, timeout)
            }, timeout)
          }, timeout)
        }, timeout)
      }, timeout)
    }, timeout)
  })
}

parentFunc((parentNestedCallback) => {
  console.log('Players : Lockers')
  parentNestedCallback(randomPlayers, randomLockers, players, lockers, 1000)
})


# Output:

Players : Lockers
Player D : Locker x
Player F : Locker Y
Player E : Locker U
Player H : Locker S
Player G : Locker Z
Player A : Locker W
Player C : Locker V
Player B : Locker T
```
**We will now dissect the code to understand what's happening and how it's structured**. 

Before that if you forgot, You can quickly review the sections described earlier in this article, particularly how an whole body callback function is passed as an argument to another function and how that argument can later be used. 

**parentFunc** function is calling and also passing a whole callback function as it's argument. The structure is,
```javascript
parentFunc(() => {
  ...
  ...
})
```

**parentFunc** function declaration will be executed and receive this whole callback argument as **parentCallback**,
```javascript
const parentFunc = (parentCallback) => {
  ...
  ...
}
```

The receiving callback argument **parentCallback** is now called and also passing a whole callback function as it's argument.
```javascript
const parentFunc = (parentCallback) => {
  parentCallback(() => {
    ...
    ...
  }
}
```


After calling **parentCallback** function, it will execute it's function definition which is the callback argument of **parentFunc** function. 
```javascript
parentFunc(() => {
  ...
  ...
})
```


Though **parentCallback** function also passing a whole callback argument in it's calling time, this argument will be received by **parentCallback** function definition as **parentNestedCallback** that means in the place where **parentFunc** passing a callback argument. 
```javascript
// 'parentCallback' passing a whole callback argument
const parentFunc = (parentCallback) => {
  parentCallback(() => {

  }
}

// 'parentCallback' receiving the whole callback argument as 'parentNestedCallback' inside the 'parentFunc' callback argument
parentFunc((parentNestedCallback) => {
  ...
  ...
})
```


Now **parentNestedCallback** function is called with passing some arguments, 
```javascript
parentFunc((parentNestedCallback) => {
  ...
  ...
  parentNestedCallback(randomPlayers, randomLockers, players, lockers, 1000)
})
```

**parentNestedCallback** will execute it's function definition which is actually the eintire callback argument of **parentCallback**. This entire callback now will receive the **parentNestedCallback** function arguments. 
```javascript
const parentFunc = (parentCallback) => {
  parentCallback((callback1, callback2, param1, param2, timeout) => {

  }
}
```


Using the above nested calbacks circulation, **display** getting all the necessary parameters to execute and output logs where **stTimeout** sequentially calling these **display** functions. 
```javascript
const parentFunc = (parentCallback) => {
  parentCallback((callback1, callback2, param1, param2, timeout) => {
    setTimeout(() => {
      display(callback1, callback2, param1, param2)
      setTimeout(() => {
        display(callback1, callback2, param1, param2)
        ...
        ...
      }
    }
  })
}
```


Now a centralized nested callback system handling all of the next instructions, moreover extra functionalities or logs can be added before or after the lottery automation system. 
```javascript
parentFunc((parentNestedCallback) => {
  console.log('Players : Lockers')
  parentNestedCallback(randomPlayers, randomLockers, players, lockers, 1000)
})
```
After studying the sections above and reviewing the code, it becomes evident that the more nested callbacks are used, the harder the code is to understand. This complexity is especially apparent to those working with Node.js. Because of this, most modern asynchronous JavaScript methods don't use callbacks. Instead, in JavaScript, asynchronous programming is solved using Promises instead.




### H) Javascript Promises
#### i) Comparing Side by side of Callback and Promises:

Understanding JavaScript **callback**s and **promises** is fundamental to mastering asynchronous programming in JavaScript. We have already learned lot about Callback from the upper sections of this article. Below, we will compare callbacks and promises side by side, and then we will dive into an in-depth exploration of promises.

##### When simulating an asynchronous operation using callback, eight things may exists in between the processes to handle operation,

i) A main function call to start the process

ii) A callback function passing as a main function argument

iii) Main function body

iv) Receiving the passing callback in main function body

v) A time-taking asynchronous function to process some tasks

vi) Some data if available 

vii) Callback function call to process the data

viii) Callback function body

```javascript
// Example: 
// Main function body, receiving callback, time-cunsuming asynchronous function, 
// available data, callback call   
const fetchData = (callback) => {
  setTimeout(() => {
    const data = {
      name: "Khan",
      age: 50
    };
    callback(data);
  }, 1000);
}

// Callback function body
function handleData(data) {
  console.log("Data received:", data);
}

// Main function call and passing a callback function
fetchData(handleData);


# Output:

Data received: {
  name: "Khan"
  age: 50,
}
```

##### We can also write the above code using whole callback syntax as belows,
```javascript
// Example: 
// Main function body, receiving callback, time-cunsuming asynchronous function, 
// available data, callback call   
const fetchData = (callback) => {
  setTimeout(() => {
    const data = {
      name: "Khan",
      age: 50
    };
    callback(data);
  }, 1000);
}

// Main function call, passing a callback function, callback function body
fetchData((data) => {
  console.log("Data received:", data);
});


# Output:

Data received: {
  name: "Khan"
  age: 50,
}
```

Callbacks can lead to complex and hard-to-maintain code, especially when multiple asynchronous operations depend on each other. The more nested callbacks are used, the more those processing terms will become intertwined. Consequently, understanding the code will become increasingly difficult. We already known that this is called **callback hell** or **pyramid of doom**.

##### Callback Hell,
```javascript
// Example:   
const fetchData = (callback) => {
  setTimeout(() => {
    const data = {
      name: 'Khan',
      age: 50
    }
    callback(null, data)
  }, 1000)
}

const fetchMoreData = (data, callback) => {
  setTimeout(() => {
    data.sex = 'Male'
    callback(null, data)
  }, 1000)
}

const fetchEvenMoreData = (data, callback) => {
  setTimeout(() => {
    data.profession = 'Software Engineer'
    callback(null, data)
  }, 1000)
}

const fetchFinalData = (data, callback) => {
  setTimeout(() => {
    data.interest = 'Movie'
    callback(null, data)
  }, 1000)
}

fetchData((error, data) => {
  if (Object.entries(data).length === 0) {
    console.error("Error fetching data:", error);
    return;
  }
  fetchMoreData(data, (error, data) => {
    if (Object.entries(data).length === 0) {
      console.error("Error fetching data:", error);
      return;
    }
    fetchEvenMoreData(data, (error, data) => {
      if (Object.entries(data).length === 0) {
        console.error("Error fetching data:", error);
        return;
      }
      fetchFinalData(data, (error, data) => {
        if (Object.entries(data).length === 0) {
          console.error("Error fetching data:", error);
          return;
        }
        console.log('Final Data:', data)
      })
    })
  })
});


# Output:

Final Data: {
  name: 'Khan', 
  age: 50, 
  sex: 'Male', 
  profession: 'Software Engineer', 
  interest: 'Movie'
}
```
After fetching available processed data, the nested one receives it, thus managing the nested chain. However, as the chain grows larger, reading and controlling the code will become increasingly difficult.


##### Let's convert the above code to Javascript Promises,
```javascript
// Example:   
const fetchData = () => {
  const result = new Promise((resolved, rejected) => {
    setTimeout(() => {
      const data = {
        name: 'Khan',
        age: 50
      }
      resolved(data)
    }, 1000)
  })
  return result
}

const fetchMoreData = data => {
  const result = new Promise((resolved, rejected) => {
    setTimeout(() => {
      data.sex = 'Male'
      resolved(data)
    }, 1000)
  })
  return result
}

const fetchEvenMoreData = data => {
  const result = new Promise((resolved, rejected) => {
    setTimeout(() => {
      data.profession = 'Software Engineer'
      resolved(data)
    }, 1000)
  })
  return result
}

const fetchFinalData = data => {
  const result = new Promise((resolved, rejected) => {
    setTimeout(() => {
      data.interest = 'Movie'
      resolved(data)
    }, 1000)
  })
  return result
}

fetchData()
  .then(data => {
    return fetchMoreData(data)
  })
  .then(data => {
    return fetchEvenMoreData(data)
  })
  .then(data => {
    return fetchFinalData(data)
  })
  .then(data => {
    console.log('Final Data:', data)
  })
  .catch(error => {
    console.log('Error:', error)
  })


# Output:

Final Data: {
  name: 'Khan', 
  age: 50, 
  sex: 'Male', 
  profession: 'Software Engineer', 
  interest: 'Movie'
}
```
Comparing both **callback hell** and **promises** code samples described above, it seems the later asynchronous operations are cleaner and more readable manner. 

##### Below are some more features specified that how we can get benifits of Promises over Callbacks.

**Readability** :- How easy it is to read and understand the code. We don't need to burden about **Nested Callbacks**.
```javascript
// Example: Callback readability
fetchData((data) => {
  fetchMoreData(data, (data) => {
    fetchEvenMoreData(data, (data) => {
      fetchFinalData(data, (data) => {
        console.log('Final Data:', data)
      })
    })
  })
});


// Example: promise readability
fetchData()
  .then(data => {
    return fetchMoreData(data)
  })
  .then(data => {
    return fetchEvenMoreData(data)
  })
  .then(data => {
    return fetchFinalData(data)
  })
  .then(data => {
    console.log('Final Data:', data)
  })
``` 


**Purpose** :- **Callback** Handle async operations by passing a function. **Promises** handle async operations with more control.
```javascript
// Example: Callback always by passing functions
const fetchData = (callback) => {
  setTimeout(() => {
    const data = {
      name: 'Khan',
      age: 50
    }
    callback(data)
  }, 1000)
}
...
...
fetchData((data) => {
  fetchMoreData(data, (data) => {
    fetchEvenMoreData(data, (data) => {
      fetchFinalData(data, (data) => {
        console.log('Final Data:', data)
      })
    })
  })
});


// Example: promise without passing functions
const fetchData = () => {
  const result = new Promise((resolved, rejected) => {
    setTimeout(() => {
      const data = {
        name: 'Khan',
        age: 50
      }
      resolved(data)
    }, 1000)
  })
  return result
}
...
...
fetchData()
  .then(data => {
    return fetchMoreData(data)
  })
  .then(data => {
    return fetchEvenMoreData(data)
  })
  .then(data => {
    return fetchFinalData(data)
  })
  .then(data => {
    console.log('Final Data:', data)
  })
``` 


**Error Handling** :- 

Using **Callback**, Must handle errors manually in each callback. 

Using **Promises**, Centralized error handling with **.catch()**.
```javascript
// Example: Callback error handling
fetchData((error, data) => {
  if (Object.entries(data).length === 0) {
    console.error("Error fetching data:", error);
    return;
  }
  fetchMoreData(data, (error, data) => {
    if (Object.entries(data).length === 0) {
      console.error("Error fetching data:", error);
      return;
    }
    fetchEvenMoreData(data, (error, data) => {
      if (Object.entries(data).length === 0) {
        console.error("Error fetching data:", error);
        return;
      }
      fetchFinalData(data, (error, data) => {
        if (Object.entries(data).length === 0) {
          console.error("Error fetching data:", error);
          return;
        }
        console.log('Final Data:', data)
      })
    })
  })
});


// Example: promise error handling
fetchData()
  .then(data => {
    return fetchMoreData(data)
  })
  .then(data => {
    return fetchEvenMoreData(data)
  })
  .then(data => {
    return fetchFinalData(data)
  })
  .then(data => {
    console.log('Final Data:', data)
  })
  .catch(error => {
    console.log('Error:', error)
  })
``` 


**Chaining** :- Nested callbacks can lead to callback hell. In promises, clean chaining with **.then()** 
```javascript
// Example: Callback chaining
fetchData((error, data) => {
  fetchMoreData(data, (error, data) => {
    fetchEvenMoreData(data, (error, data) => {
      fetchFinalData(data, (error, data) => {
        ...
        ...
      })
    })
  })
});


// Example: Promise .then() chaining
fetchData()
  .then(data => {
    ...
    ...
  })
  .then(data => {
    ...
    ...
  })
  .then(data => {
    ...
    ...
  })
  .then(data => {
    ...
    ...
  })
  .catch(error => {
    ...
    ...
  })
``` 


**State** :- Using callback asynchronous programming no built-in state management while in promises has states (**pending, fulfilled, rejected**). We will discuss that in details later. 


**Parallel Execution** :- 

Executing multiple asynchronous operations in parallel using callback is done by **seperated function call**.

Executing multiple asynchronous operations in parallel using promise is done by **Promise.all()** bindings.
```javascript
// Example: Callback parallel execution
// Logs both results when both tasks are done
function task1(callback) {
  setTimeout(() => {
    callback('Task 1 result');
  }, 1000);
}

function task2(callback) {
  setTimeout(() => {
    callback('Task 2 result');
  }, 1000);
}

let results = [];
task1(result1 => {
  results.push(result1);
  if (results.length === 2) {
    console.log(results);
  }
});
task2(result2 => {
  results.push(result2);
  if (results.length === 2) {
    console.log(results);
  }
});


# Output:

['Task 1 result', 'Task 2 result']


// Example: Promises parallel execution
// Logs both results when both tasks are done
function task1() {
  return new Promise((resolve) => {
    setTimeout(() => {
        resolve('Task 1 result');
    }, 1000);
  });
}

function task2() {
  return new Promise((resolve) => {
    setTimeout(() => {
        resolve('Task 2 result');
    }, 1000);
  });
}

Promise.all([task1(), task2()]).then(results => {
  console.log(results);
});


# Output:

['Task 1 result', 'Task 2 result']
``` 


**Work Flow** :- 

###### Callback Work Flow,

1) Start Asynchronous Operation: Initiate an asynchronous operation (e.g., fetching data).

2) Pass Callback: Provide a callback function to handle the result once the operation is complete.

3) Execute Callback: Once the operation completes, execute the callback with the result.

Executing multiple asynchronous operations in parallel using callback is done by 


###### Promises Work Flow,

1) Create Promise: Create a new promise, which starts the asynchronous operation.

2) Resolve or Reject: The promise is either resolved (successful completion) or rejected (failure).

3) Handle Result: Use .then() to handle the resolved value and .catch() to handle any errors.

4) Chain Operations: Chain multiple asynchronous operations together. 

Before fully getting acquainted with promises, we've spent time discussing both callbacks and promises side by side. This approach helps to build an early understanding of promises and their practical applications.


#### ii) Introduction to Promises:

##### Introduction: Promise is an object
A promise is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. They represent a value that may be available now, or in the future, or never.

While Promises are primarily designed to handle asynchronous operations, they can also be used in synchronous code. However, their primary use case is managing asynchronous behavior in JavaScript. Promises allowing us to chain operations.

##### Purpose of Promises
Promises help in managing asynchronous operations in JavaScript, making code more readable and maintainable. They provide a way to handle the result or failure of asynchronous tasks without getting lost in callback hell.


##### Promises Object Properties: State and Result
The Promise object supports two properties: 

a) **state** 

b) **result**.

A promise can be one of three states: 

a) **Pending:** The initial state. The promise is neither fulfilled nor rejected. The result is undefined

b) **Fulfilled:** When a promise is fulfilled, it means the asynchronous operation has completed successfully, and it holds a value as its result.

c) **Rejected:** When a promise is rejected, it means the asynchronous operation has failed, and it holds a reason for the failure.

**NOTE:** Promise properties state and result can't be accessed. We have to use promise method to handle promises.


##### Creating a Promise: Promise Syntax

i) you use the new **Promise() constructor**, 

ii) which takes a function with two parameters: **resolve** and **reject**. 

iii) Inside this function, you perform the asynchronous operation 

iv) then call **resolve()** when it **succeeds** or 

v) **reject()** when it **fails**.
```javascript
// Example: Promises syntax
const promiseObj = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    let success = true; // Assuming the operation succeeded
    if (success) {
      resolve("Data successfully fetched!");
    } else {
      reject("Error: Failed to fetch data!");
    }
  }, 2000);
});
```


##### Accessing Promise States and Results: Promise Callbacks and Promise Methods
a) **Promise Callbacks: Resolve and Reject:**

In the context of JavaScript promises, **resolve** and **reject** are callback functions provided by the Promise constructor. They are used to transition the promise from its initial pending state to either a fulfilled state (using resolve) or a rejected state (using reject).

i) **resolve(value)**: The promise is fulfilled with the given value

ii) **reject(reason)**: The promise is rejected with the given reason

iii) We can use anything name in replace of **resolve** and **reject**

iv) But always remember the first parameter will be **resolve** callback and the second parameter **reject** 

```javascript
// Example: Promise resolve, reject
let promiseObj = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve("Operation successful!");
  } else {
    reject("Operation failed!");
  }
});
```

b) **Promise Methods: .then(), .catch(), .finally():**

When promises are resolved or rejected with success or failure result we can't directly access the state or result. We have to use promise methods.

i) **.then()**: Handle the result of a promise. **then()** can chained to handle successive asynchronous operations. **.then()** can take two optional callback arguments. One for **success(resolve**) and one for **failure(reject)**

ii) **.catch()**: Handle errors if the promise is rejected.

iii) **.finally()**: Executes code after the promise is settled, whether it's fulfilled or rejected. Sometimes we need to cleanup or finalization tasks after the promise chain completes.
```javascript
// Example: .then(), .catch() and .finally()
// If .then() take one argument, .catch() will use for failure handle
promiseObj.then((result) => {
  console.log("Promise fulfilled:", result);
}).catch((error) => {
  console.error("Promise rejected:", error);
}).finally(() => {
  console.log("Promise settled."); // This will be executed regardless of the promise's outcome.
});


// Example: .then() can take two arguments to handle success or failure result
promiseObj.then((result) => {
  console.log("Promise fulfilled:", result);
}, (error) => {
  console.log("Promise failed:", error);
}).finally(() => {
  console.log("Promise settled."); // This will be executed regardless of the promise's outcome.
});
```


##### Promises as a: Producing Code, Consuming Code
Promises in JavaScript provide a powerful way to handle asynchronous operations. To understand promises fully, it's helpful to break them down into two main parts: "producing code" and "consuming code." Let's explore each part in detail, including examples.

**Producing Code:**

Producing code is the code that creates and resolves a promise. This code is responsible for starting an asynchronous operation and eventually resolving or rejecting the promise based on the outcome of the operation.

###### Example of Producing Code,

Let's create a promise that simulates an asynchronous task, such as fetching data from a server.

```javascript
// Example: Producing code
const fetchData = new Promise((resolve, reject) => {
  console.log("Fetching data...");

  // Simulate an asynchronous operation with setTimeout
  setTimeout(() => {
    const success = true; // Change this to false to simulate a failure

    if (success) {
      resolve("Data fetched successfully!");
    } else {
      reject("Error fetching data.");
    }
  }, 2000);
});
```
###### In this example,

i) The fetchData promise is created with the **new Promise constructor**.

ii) The executor function starts the asynchronous operation.
```javascript
(resolve, reject) => { ... }
```
iii) If the operation is successful, resolve is called with the result (**Data fetched successfully!**).

iv) If the operation fails, reject is called with an error message (**Error fetching data.**).


**Consuming Code:**

Consuming code is the code that uses the promise produced by the producing code. This code handles the promise's resolution or rejection by attaching handlers to it.

###### Example of Consuming Code,

Now let's see how we can consume the **fetchData** promise using **.then** and **.catch**.

```javascript
// Example: Consuming code
fetchData
  .then((result) => {
    console.log(result); // Output: Data fetched successfully!
  })
  .catch((error) => {
    console.error(error); // This will not run in this case
  });
```
###### In this example,

i) **fetchData.then((result) => { ... })** attaches a handler for when the promise is resolved. It receives the result and logs it to the console.

ii) **fetchData.catch((error) => { ... })** attaches a handler for when the promise is rejected. It receives the error and logs it to the console.


**Working with Producing and Consuming Code:**

As a developer, you will often work with both producing and consuming code. However, the nature of the task determines which type of code you spend more time writing.

###### Producing Code,

When creating APIs or libraries that perform asynchronous operations.

When you need to wrap asynchronous operations (like AJAX calls, file reads, etc.) into promises.


###### Consuming Code,

When using APIs or libraries that return promises.

When handling the results of asynchronous operations in your application.

###### Combined Example:


Let's look at a the following example that combines both producing and consuming code.

###### Producing Code,
```javascript
// Example: Producing Code
function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    console.log(`Fetching data for user with ID: ${userId}`);

    // Simulate an asynchronous operation with setTimeout
    setTimeout(() => {
      const data = { id: userId, name: "Khan", age: 50 };
      const success = true; // Change this to false to simulate a failure

      if (success) {
        resolve(data);
      } else {
        reject("Error fetching user data.");
      }
    }, 3000);
  });
}
```

###### Consuming Code,
```javascript
// Example: Consuming Code
fetchUserData(1)
  .then((userData) => {
    console.log("User Data:", userData);
  })
  .catch((error) => {
    console.error("Failed to fetch user data:", error);
  });
```
###### Explanation:
###### Producing Code,

i) **fetchUserData(userId)** is a function that returns a promise.

ii) Inside the promise executor, a simulated asynchronous operation is performed using setTimeout.

iii) Based on the outcome of the operation, the promise is either resolved with user data or rejected with an error message.


###### Consuming Code,

i) The **fetchUserData** function is called with a user ID of 1.

ii) The **.then** handler processes the resolved data, logging the user information to the console.

iii) The **.catch** handler handles any potential errors.



### I) Javascript Async/Await
We have learned a great deal about **callbacks** and how they handle asynchronous operations. Additionally, we have explored the difficulties and frustrations that arise when managing asynchronous operations with **nested callbacks**. Furthermore, we have seen how **promises**, with their magical **.then()** method, can simplify handling asynchronous operations as well as chaining asynchronous operations without passing callbacks.

Now, we will learn how **Async/Await**, built on promises, can manage asynchronous code in an even more elegant, more intuitive and straightforward way.


#### i) Introducing Async
<p style="height:1px; margin-bottom:19px;"></p>
##### Async function syntax
<p style="height:1px; margin-bottom:9px;"></p>

The async keyword is used to declare a function as asynchronous. 

An async function always returns a Promise. 

The keyword async before a function makes the function returning promise.

Though async function return promise, It can be proofed that without **.then()** method we can't get settled result.
```javascript
// Example: Simple async function
async function iAmAsyncFunc() {
  return "I am async function!";
}

iAmAsyncFunc()
.then(data => console.log(data))


// Example: Anonymous async function
const iAMAsyncFunc = async function () {
  return 'I am async function!'
}

iAMAsyncFunc()
.then(data => console.log(data))


// Example: Arrow async function
const iAMAsyncFunc = async () => {
  return 'I am async function!'
}

iAMAsyncFunc()
.then(data => console.log(data))


# Output:

I am async function!
```
<p style="height:1px; margin-bottom:14px;"></p>

##### Async function always return Promise
```javascript
// Example: Async function always return promise even no promise constructor
const iAmAsyncFunc = async () => {
  return 'I am async function without promise constructor'
}

iAmAsyncFunc()
.then((data) => {
  console.log(data)
})

# Output:

I am async function without promise constructor



// Example: Async function always return promise even resolved with a promise constructor
const iAmAsyncFunc = async () => {
  const promiseObj = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('I am async function resolved with promise')
    }, 3000)
  })

  return promiseObj
}

iAmAsyncFunc()
.then((data) => {
  console.log(data)
})


# Output:

I am async function resolved with promise
```
<p style="height:1px; margin-bottom:14px;"></p>

##### Async function returned result can be handled by promise method .then()
```javascript
// Example: Using .then() method handling async return result
const iAmAsyncFunc = async () => {
  return 'I am async function without promise constructor'
}

iAmAsyncFunc()
.then((data) => {
  console.log(data)
})

# Output:

I am async function without promise constructor

```
<p style="height:1px; margin-bottom:14px;"></p>
##### It's not that much interesting only using async keyword!
<p style="height:1px; margin-bottom:9px;"></p>

Only using async keyword with no internal promise call need to implicitly create a resolved promise with a value.

Only use async keyword with implicitly created a resolve promise actually return the vlue immediately.

Only use async keyword need promise methods to handle settled result. So, basically promise style result handling.

Only creating async keyword the function itself can not directly wait for the time-consuming asynchronous task to complete before returning a result because time-taking methods are non-blocking.
```javascript
// Example: Async function no internal promise call implicitly creates a resolved promise
const iAmAsyncFunc = async () => {
  console.log('Operation started...')

  setTimeout(() =>  {
    console.log('Operation completed after delay') // logged after 2 second delay independently
  }, 2000)

  return ('Operation will complete after delay') // implicitly resolved promise
}

iAmAsyncFunc()
.then(data => console.log(data)) // Handling the immediately settled promise result
.catch(error => console.log(error))


# Output:

Operation started...
Operation will complete after delay
Operation completed after delay
```
It's obvious from the above code that only using async keyword doesn't come any speciality to handle asynchronous operation as an asynchronous function. This approach achieves the requirement of lackings any waiting mechanism while still demonstrating asynchronous behavior. So, need a pattern to fully utilize the promise-based-asynchronous handling over smartly on top of promises. And here comes 'Await' into the scene.


#### ii) Introducing Await
<p style="height:1px; margin-bottom:19px;"></p>
##### Async/Await function syntax
<p style="height:1px; margin-bottom:9px;"></p>
```javascript

```



## Conclusion

I've endeavored to provide a concise overview of the transition from legacy JavaScript to the contemporary async/await model in this article. Instead of delving into intricate technical discussions about single-threaded or multi-threaded systems, I've focused on presenting theoretical insights alongside practical examples in a manner that's clear, elegant, and succinct.

I would be greatly pleased if anyone identifies any errors or inaccuracies within this content and notifies me through comments. Such feedback would motivate me to produce more articles in the future. 


**                                                                       **





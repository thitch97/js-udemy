# Udemy JS Course - Section 4

## Objects and the dot

Objects have properties and methods. Properties can either be primitive types or other objects.
Methods are functions that are attached to specific object.

The commputed member access operator can be used to lookup the properties of an object. It takes a string as input and so is more dynamic in that you can use a variable to perform the lookups.
**E.g. :**:

```javascript
person["firstname"] = "Tony";

firstNameProperty = "firstname";

console.log(person[firstNameProperty]); ```

The member access operator has the same function but is more readable and less verbose

```javascript
console.log(person.firstname);
console.log(person.lastname); ```

The dot operator cannot be used to create properties on the fly. It simply returns undefined for nonexistent properties.

Precedence for both operators is left-to-right and can be chained together, for example:

```javascript
person.address = new Object();
person.address.street = "111 Main St.";

console.log(person["address"]["street"]);
```

## Objects and Object literals

We can create a new object like so:
```javascript
var person = new Object();
```
 Or:
```javascript
var person = {};
console.log(person)  {}
```
The latter is a shorthand version of the former and can be used to set properties as well.
**E.g. :**:

```javascript

var person = {
	firstname : 'Tony',
	lastname : 'Alicea',
	address : {
		street : "111 Main St.",
		city : "New York",
		state : "NY"
	}
};
```

 This syntax can also be used to declare objects on the fly

```javascript
function greet(person) {

	console.log ('Hi ' + person.firstname);

}

greet({
	firstname : "Mary",
	lastname : "Doe"
});
```

Object literal syntax can be mixed with the dot syntax
 **E.g. :**:

```javascript
Tony.address2 = {
	street : '333 Second St.';
};
```


## Framework Aside - Faking Namespaces


A namespace is a container for variables and functions. JavaScript does not have them.
 We can however "fake" namespaces using objects.


## JSON and Object Literals


JSON is inspired by object literal sytax but is not the same thing.

In JSON, property names have to be wrapped in quotes:

```javascript
var objectLiteral = {
	"firstname" : "Mary",
	"isAProgrammer" : true
}
```

Object literal notation gives the option of wrapping these properties in quotes or not.

JavaScript provides built-in functions for converting between the two:
console.log(JSON.stringify(objectLiteral));
var jsonValue = JSON.parse('{ "firstname": "Mary", "isAProgrammer": true }');

jsonValue is an object created using the JSON information.


## FUNCTIONS ARE OBJECTS


The fact that JS has first-class functions means that everything you can do with any other type
can be done on functions as well.

 Functions in Javascript are themselves objects. As such, primitives, objects and other
 functions can all be attached to a function

 The properties of a function object  include:
 	primitives, objects, functions, NAME(the name of the function, optional),
 CODE (this is the code that you have written which is invocable)


## Function statements and function expressions


 An expression is unit of code that result in a value. This does not have to be saved
 to a variable.

 A statement on the other hand does work but does not return a value. Such as an if statement.

 Functions also have expressions and statements

**E.g. :** Function statement
```javascript
function greet() {
	console.log('hi');
}
```

**E.g. :** Function expression
```javascript
var anonymousGreet = function() {
	console.log('hi');
}
```

The function created as part of the expression may be run using ():
```javascript
anonymousGreet();
```

 Whereas invocation for function statements may be used before or after the statement itself,
 invocation for expressions must be placed after the expression itself.

 This is due to the way in which the engine sets up the execution context before running the code.
 FUnctions are hoisted and placed in memory before the code runs, which is why the point of invocation 
 does not matter. Variables (such as our function expression) are placed in memory as well but
 are assigned a default value of undefined. Therefore, the variable anonymousGreet would
 not have the function assigned to it until the function expression.

 **E.g. :**
```javascript
greet();  hi

function greet() {
	console.log('hi');
}

anonymousGreet(); //Undefined Error

var anonymousGreet = function() {
	console.log('hi');
}
```
Function literals can also be passed as parameters to other functions. 
**E.g. :**
```javascript
function log(a) { 
	console.log(a);
}

log(function() {
	console.log('hi');
}) 
```

To invoke the passed function we can use ()
**E.g. :**
```javascript
function log(a) {
	a();
}
```

## By Value vs By Reference


 In JS, all objects (including functions) operate by reference while primitives usually 
 operate by value.

 Assigning a variable to an existing object points the variable to the same memory location
 instead of creating a copy. If an existing variable is assigned to a new object, new memory
 space is created.

**E.g. :**
```javascript
c = {greeting : 'Hello'};
var d = c;

console.log(c);
console.log(d);

c = {greeting : 'Howdy'};

console.log(c);
console.log(d);
```

 the first two lines of output would be the same as c and d both point to the same object in memory. However, after the new assignment of c, the outputs will differ.


## Objects, Functions and 'this'


 When a function is invoked, and its execution context created, the JS engine gives us 
 a variable called 'this'. 'this' points at a different object based on where the function is
 and how it is called.

'this' is immediately available without any declaration needed.

When you create a function statement, 'this' still points to the global object, if you're simply invoking
 the function.

**E.g. :**
```javascript
function a() {
  console.log(this);
}

a(); prints the global object
```

> Sidenote:
> If 'this' points to the global object, we could create a new variable by simply writing:

```javascript
this.newvariable = 'hello'; 
```




If we create an object and define a method for that object, 'this' points to the object
 that contains the method.
```javascript
var c = {
	name : 'The c object',
	log : function () {
		console.log(this);
	}
}

c.log();  outputs the object c
```

Best practice for using 'this' in nested objects is to set a separate variable called 'self' to the location of this that we wish to reference.

**E.g. :**
```javascript
var c = {
	name: 'The c object',
	log : function() {

		var self = this;
		self.name = 'Updated c object';
		console.log(self);

		var setname = function(newname) {
			self.name = newname;
		}
		setname('Updated again! The c object');
		console.log(self);
	}
}
``` 

## Arrays: Collections of anything


**Javascript arrays are different because it is dynamically typed. Therefore, arrays in JavaScript are heterogenous (individual elements can be of any type).**

Additionally, we can use this feature to do interesting things such as:
```javascript
var arr = [
	1,
	false,
	{
		name : 'Tony',
		address : '111 Main St.'
	},
	function(name) {
		var greeting = 'Hello ';
		console.log(greeting + name);
	},
	"hello"
];

console.log(arr);
arr[3](arr[2].name);  Hello Tony
```

## 'arguments' and SPREAD

**'arguments' holds all the values of all the values of all the parameters that are passed to a function.**

Parameters are hoisted just like any other variable and their inital value set as undefined. This is why functions may be invoked with no parameters even when they expect parameters. Additionally, it is perfectly legal to declare less parameters than is expected.

```javascript
function greet(firstname, lastname, language) {
  
  language = language || 'en'; //sets up default value for language argument
  
  console.log(firstname);
  console.log(lastname);
  console.log(language);
  console.log(arguments);
  console.log('--------------');
  
}

greet();
greet('John');
greet('John', 'Doe');
greet('John', 'Doe', 'es');
```

**Output:**

```
undefined
undefined
en
{}
--------------
John
undefined
en
{ 0: 'John' }
--------------
John
Doe
en
{ 0: 'John', 1: 'Doe' }
--------------
John
Doe
es
{ 0: 'John', 1: 'Doe', 2: 'es' }
--------------

```

The 'arguments' data structure which is returned is array-like but is not truly an array. Still, it allows us to utilize array-like properties:

```javascript
if (arguments.length === 0){
	console.log("Missing parameters!");
	console.log("------------------")
	return;
}

```

'arguments' is deprecated in ES6. Instead we use spread.

We can use spread to take any extra parameters that aren't explicitly defined and wrap them in a JavaScript array.

```javascript
function greet(firstname, lastname, language, ...other) {
  
// ... //
  
}

greet('John', 'Doe', 'es', '111 main st.', 'new york');

```
The arguments after 'es' will all be wrapped in the '...other' variable.

## Framework Aside: Function Overloading

Function overloading is not technically possible with the way Javascript defines functions.

A similar pattern may be employed to replace explicit function overloading whereby helper functions can call a base function which governs standard behaviour and simply change what variables are passed to the base function.


## Conceptual Aside: Syntax Parsers

**\-\-REVISIT IF NECESSARY\-\-**

## Dangerous Aside: Automatic Semicolon Insertion

Semicolons are optional in JS because the syntax parser inserts semicolons where it thinks they should be if they are missing.

For example, 

```javascript
function getPerson() {

	return
	{
		firstname : 'Tony'
	}

}

console.log(getPerson());
``` 

The above code will return 'undefined' because the syntax parser inserts a semicolon next to the return statement, which in turn causes the function to stop where it is. In order to avoid errors related to this:

* Always type your semicolons in yourself
* Put your opening curly braces on the same line as the keyword that needs it:

```javascript
function getPerson() {

	return {

		firstname : 'Tony'
	}

}

console.log(getPerson());
``` 

## Framework Aside: Whitespace

JS is quite liberal with whitespace allowances in that it allows whitespace within statements.

For example:

```javascript
var 
	// first name of the person
	firstname,

	// last name of the person
	lastname,

	//the language
	//can be 'en' or 'es'
	language;

var person = {
	// the first name
	firstname : 'John',

	// the last name 
	// (always required)
	lastname: 'Doe'
}
```
Everything in the above code is completely legal and should be used to make code more readable for other programmers.

## Immediately Invoked Function Expressions (IIFEs)

We recall that a function expression is a function object that is created on the fly (not put into memory in the creation phase) and can be assigned to a variable. Kind of like a 'function literal'. 

Though function expressions can be declared in line, invocations of the function must be done separately unless IIFEs are used.

```javascript

//using a function expression
var greetFunc = function(name) {
	console.log('Hello ' + name);
};

// we can invoke it like this:
greetFunc('John');

// but, since the created function object has a code property, we can invoke it on-the-fly
// using an IIFE

var greetFunc = function(name) {
	return 'Hello ' + name;
}('John');

// this will return 'Hello John' and place it into greeting
```

On a related note, in order to create a function expression without the need to assign it to a variable, we can enclose a function statement within parentheses.

```javascript
var firstname = 'John';

(function(name) {
	var greeting = 'Hello';
	console.log(greeting + ' ' + name);

}(firstname));

```
*Note: Could be used to run XSS attacks.*

## Framework Aside: IIFEs and Safe Code

Since an IIFE has its own execution context, any variables created within the function does not interfere with those outside its scope.

Alternatively, we can pass variables into the IIFE so that they can interact.

```javascript
var firstname = 'John';
var greeting = 'Hola';

//we pass the global context into the IIFE as a variable which allows us to interact with variables across scopes.
(function(global, name) {

	var greeting = 'Hello';
	global.greeting = 'Hello';
	console.log(greeting + ' ' + name);

}(window, 'John'));

//global greeting variable is changed within the function
console.log(greeting)
```

## Understanding Closures

```javascript
function greet(whattosay) {

	return function(name) {
		console.log(whattosay + ' ' + name);
	}
}

var sayHi = greet('Hi');
sayHi('Tony'); //outputs 'Hi Tony'
```

The above code seems strange because we are able to access the whattosay variable even after greet has been completed and popped off of the execution stack. This happens for a few reasons:

1. When a function completes in JS, it is popped off the execution stack but its variable environment and references to that environment remain intact until garbage collection is done.

2.  A function created within another function which is executed after the outer function has finished maintains the references it had to its outer environment (the function it was created within). So, in the above example, when we return the inner function, it is stored in the sayHi variable as a function object. sayHi's code is invoked and the engine performs a lookup on 'whattosay'. Since it cannot find it within sayHi's scope, it follows the scope chain to locate the variable. At this point, even though greet's execution context has finished, the references to its memory location persists, where whattosay can be found.

In this way, we say that the inner function's execution context closed in on its outer variables. This phenomenon is called a closure. 

*__In general, then, the JS engine ensures that each execution context maintains access to its outer variables irrespective of the status of those execution contexts.__*

## Understanding Closures: Part 2

```javascript
function buildFunctions() {

	var arr = [];

	for (var i = 0; i < 3; i++){ 
		arr.push(function() {
			console.log(i);
		});
	}
	return arr
}

var fs = buildFunctions();

fs[0]();
fs[1]();
fs[2]();
```

The above code prints: 
```
3
3
3
```
This might seem counterintuitive, but we must realize that the inner function is not run during the for loop. Three separate function objects are created and each are added to the array 'arr'. When we invoke each function later on, the engine looks for i in the outer variable environment and since i = 3 at the end of buildFunction()'s execution context and each function has a reference to the same memory location for i, 3 is returned each time.

This is analogous to asking three siblings what age their father is. Each child will tell you what the age of their father is at that time, not what age he was when each they were born.

We can modify the above code to print out the answer that makes sense intuitively as follows:
```javascript
function buildFunctions() {

	var arr = [];

	for (var i = 0; i < 3; i++){ 
		arr.push(
			(function(j) {

				return function() {
					console.log(j);
				}
			}(i))
		)
	}
	return arr
}

var fs = buildFunctions();

fs[0]();
fs[1]();
fs[2]();

```
In this case, we utilize IIFEs to invoke each function on-the-fly, creating a new execution context (EC) each time. Within each EC, we declare a variable j and pass i to the function as j so that the value of i at that time is output.

Output:
```
0
1
2
```


## Framework Aside: Function Factories

We can use our knowledge of functions and closures to create functions which create and return other function for us.

```javascript
function makeGreeting(language) {

	return function(firstname, lastname) {

		if (language === 'en') {
			console.log('Hello ' + firstname + ' ' + lastname);
		}

		if (language === 'es') {
			console.log('Hello ' + firstname + ' ' + lastname);
		}

	}
}

var greetEnglish = makeGreeting('en');
var greetSpanish = makeGreeting('es');

greetEnglish('John', 'Doe');
greetSpanish('John', 'Doe');
```

In the above code, makeGreeting is called on two separate occasions. Each time it is called, a new EC is created even though it is the same function. In one EC, language is 'en' and in the other language is 'es'. Both are saved in memory and bound within the closure of its inner function. 

The inner function in each case is returned to the variable greetEnglish and greetSpanish respectively. Thus, when each of those function objects is invoked, it maintains the reference to the specific outer environment under which it was created (one with language = 'en' and the other with language = 'es').


## Closures and Callbacks

A callback function that is given to another function to be run when that function has completed (i.e. function A takes function B and runs function B when it has finished running).

```javascript
function tellMeWhenDone(callback) {
	var a = 1000;
	var b = 2000;

	callback();
}

tellMeWhenDone(function () {
	console.log('I am done!');
});

tellMeWhenDone(function () {
	alert('All done... ');
});

```

## call(), apply(), bind()

Recalling the 'this' variable that is automatically created for objects, we remember that 'this' refers to the containing object. For example, for an object's method, 'this' points to the object itself.

The 'bind' function can be used to specify which object a given function expression points to. It creates a copy of the function and sets its 'this' property to the object passed into it.

'call' does something similar, but actually executes the function instead of just making a copy of it.
 
'apply' is similar to 'call' in that regard, but takes the arguments of the function as an array instead of just declaring the arguments explicitly in the invocation.

```javascript
var person = {
	firstname: 'John',
	lastname: 'Doe',
	getFullName: function() {
		var fullname = this. firstname + ' ' + this.lastname;
		return fullname;
	}
}

var logName = function(lang1, lang2) {

	console.log('Logged: ' + this.getFullName);// this will throw an error because 'this' references the global object
												// and there is no method getFullName attached to the global object.

}.bind(person); // I can also call bind here on-the-fly

var logPersonName = logName.bind(person); // creates a copy of logName which points 'this' of logName function object to the 										   //person object.

logPersonName('en', 'es');

logName.call(person, 'en', 'es'); //does the same thing as logName() but points 'this' to the first parameter (i.e.'person') 
logName.apply(person, ['en', 'es']); // same as .call() but takes arguments as an array.

// we can also do:

(function(lang1, lang2) {

	console.log('Logged: ' + this.getFullName);

}).apply(person, 'en', 'es');
```

Practical uses of this include 'function borrowing' whereby a method of one object is used on another object with similar property names and 'function currying'.

```javascript
//function borrowing

console.log(person.getFullName.apply(person2)); 
// we're using the method of the person object and pointing 'this' to person2 


//function currying
function multiply(a, b) {
	return a * b;
}

//passing an argument to .bind() sets the first parameter of (a copy of) multiply() (i.e. 'a') to 2 permanently.
var multiplyByTwo = multiply.bind(this, 2);

console.log(multiplyByTwo(4)); // evaluates to 8
```

Function Currying is the practice of creating a copy of a function but with some preset parameters. This is important for functional programming.

## Functional Programming

In functional programming, one thinks and codes in terms of functions.

The following is my own example of checking for palindromes using functional programming:
```javascript
arr1 = prompt("Enter a word:").split("");

function mapForEach(arr, fn) {

	var newArr = [];

	for (i = 0; i < arr.length; i++){
		newArr.push(
			arr[fn(i)]
		);
	}

	return newArr;
}

var swap = function(length){
	return function(length, item) {
		return (length - item) - 1 ;
	}.bind(this, length);
};

word2 = mapForEach(arr1, swap(arr1.length)).join("");

console.log(word2 === arr1.join(""));

```
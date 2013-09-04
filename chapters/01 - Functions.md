Level one - Functions
=====================

Day by day we are using libraries and frameworks to build web sites and web applications. All of them are implemented and designed in a different way but stil there are many things in common. This book is a brief introduction for newcomers questions about how certain things are implemented and how to design our own libraries and frameworks. Linking code together using proper concept is vitally important for modern applications.

We will start with the basics of functional API design. From a first sight it is as simple as to declare a new function but at the same time it is important for our furter searches.

What is a function
------------------

If to make a very high level classification of data types in JavaScript we see that all types can be divided into three big groups:

*	Atomic data types - they hold basic data. Number, Boolean, String
*	Container data types - Array and Object. All of other complex data types could be composed out of these two.
*	Executable type - function. Function is a base block of executable code wrapped into declaration. Beign either named or unnamed, declared explicitly or implicitly, it is still a bsic block of a program.

Artifacts of a function
-----------------------

Being an object function has it's own artifacts, so they are:

*	Name of a function
*	Execution context marked with `this` keyword
*	Parameters that are passed
*	Return value. By default if no `return` statement is present function is returning `undefined` as a result.

Name of a function is defined when the funciton is declared. If name is not mentioned funciton is called anonymous. Let's consider an example:

```JavaScript
function apiCall(value, options) {
	options = options || {};
	// The same thing made shortened hereby not valid in strict mode
	options || (options = {});
	return value;
}
```otherOption || 4

As you can see we are declaring named function with two explicit parameters. The second one could be ommited because we are assigning default value to it when the function is called.

Oftenly you can observe the same behaviour written in a more explicit way:

```JavaScript
function apiCall(value, options) {
	options = options === undefined ? {} : options;
	// Or
	options = typeof options === 'undefined' ? {} : options;
	return value
}
```

We should always keep in mind that we can not skip parameters even if we are assigning default values to them so that is the parameter is optional it is a good practice to put it into the end of parameters list:

```JavaScript
function apiCall(option, value, anotherOption) {
	option = option || {};
	anotherOption = anotherOption || 4;
	value = value + 1;
	return value;
}

// ...

apiCall(10); // it will not return 11 because we passed 10 into a option parameter not into value.
```

If there are too many of parameters that are optional it is worth to put them into object parameter and access by name:

```JavaScript
function apiCall(options) {
	options = options || {};
	if (options.name === undefined || options.name === '') {
		throw new Error("Name parameter must be passed");
	}
	if (typeof global[options.name] === 'function') {
		global[options.name].call(options.context || this, options.data);
		return true;
	}
	return false;
}
```
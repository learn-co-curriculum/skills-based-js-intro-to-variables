# JavaScript Variables

## Overview

* About
* Local vs. Global Variables
* Changing Variable Values
* Declaring Variables
* Multi-line Variable Assignment
* Resources

## About

As in Ruby, variables in JavaScript are used to store information/data that will be used in our program.  A variable can point to almost any type of value including numbers, strings, arrays, and hashes.

Just like Ruby, variables are assigned values using the `=` operator. Variable names are typically all lower case, and in the case of multiple words, the words are joined together using [lowerCamelCase](http://c2.com/cgi/wiki?LowerCamelCase).

## Local vs. Global Variables

You can declare a variable in two ways but each have different consequences:

* Declaring a variable with `var` keyword:

```javascript
var someLocalNumber = 10; // can only be accessed within the current scope
```

* Declaring a variable without `var` keyword:

```javascript
someGlobalNumber = 42; // is now window.someGlobalNumber and can be accessed anywhere
```

These consequences are due to JavaScript's approach to scoping. In Ruby, we didn't have to worry too much about scoping because all variables assigned within a method were scoped to just that method. For instance:

```ruby
def make_variable
  cute_animal = "sugar glider"
  return cute_animal
end

make_variable
# => "sugar glider"

cute_animal
# => NameError: undefined local variable or method `cute_animal' for main:Object
```

Unlike Ruby, JavaScript will make a variable have local scope only if you use the keyword `var`. For instance:

```javascript
function makeVariable() {
  cuteAnimal = "sugar glider";
  return cuteAnimal;
}

makeVariable();
// "sugar glider"

cuteAnimal;
// "sugar glider"
```

See how Ruby forgets that there is a variable outside of the method but JavaScript doesn't? Now might be a good time to drop to your knees, throw your fists into the air, and scream-ask, "What?!?" 

Let me give you a second. You ready? Okay, here's what's going on:

Ruby automatically locally scopes variables but JavaScript does not unless you use the keyword `var`. Without this keyword, variables have a global scope. JavaScript knew about the variable `cuteAnimal` because we accidentally gave it a global scope. To make it local in scope (usually what you want), you'd have to add that `var` keyword, like so:

```javascript
function makeVariable() {
  var cuteAnimal = "sugar glider";
  return cuteAnimal;
}

makeVariable();
// "sugar glider"

cuteAnimal;
// ReferenceError: cuteAnimal is not defined
```

It's been mentioned already, but again, it is best to use the key word `var` before declaring a variable. This ensures that the variable is set to the current scope. If `var` is not used in defining a new variable it becomes global and is accessible throughout the program.

## Changing Variable Values

Local variable assignment can overwrite global variable assignment:

```javascript
function makeNumber() {
  num = 10;     // Declares a global variable and returns 10
  var num = 11; // Declares a non-global variable and returns 11
  return num;
}

makeNumber()
// Returns 11 showing that the local variable assignment overwrote the global variable assignment

num;
// ReferenceError: num is not defined
// This demonstrates that the global variable num became a local variable
```

However, global variable assignment can't overwrite local variable assignment, rather it simply reassigns the value of the local variable:

```javascript
function sayHello() {
  var greeting = "hola";
  greeting = "hello";
  return greeting;
}

sayHello()
// Returns "hello",
// This demonstrates that the variable greeting is now pointing to the string "hello" instead of "hola"

greeting
// ReferenceError: greeting is not defined
// This demonstrates that the variable greeting is still local instead of global
```

## Declaring Variables

A pattern that you'll see in JavaScript that you probably didn't see in Ruby is variable declaration. In JavaScript, variables can also be declared, but not necessarily assigned a value. The following two are equivalent:

Declaration and value assignment in one line:

```javascript
var greeting = "hello";

greeting;
// Returns "hello"
```

Declaration before assigning a value:

```javascript
var greeting;

greeting;
// Returns undefined

greeting = "hello";

greeting;
// Returns "hello"
```
## Multi-line Variable Assignment

Variables can also be assigned at once with multiple lines, using commas to delimit each. You must terminate the assignment with a semicolon.

Let's condense the below code into one line:

```javascript
var a = 5;
var b = 2;
var c = 3;
var d = {};
var e = [];
```

The above is equivalent to:

```javascript
var a = 5
  , b = 2
  , c = 3
  , d = {}
  , e = [];
```

which can be converted to:

```javascript
var a = 5, b = 2, c = 3, d = {}, e = [];
```

Some people prefer to keep new lines between each new variable assignment, other people like the look of the single line. Whichever way you swing, the important thing to remember is [to use commas to separate each variable](http://stackoverflow.com/a/4166789/2890716).

## Resources

* [MDN - Var Keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* [MSDN - Variable Scope](https://msdn.microsoft.com/library/bzt2dkta(v=vs.94).aspx)
* [StackOverflow - How to define multiple variables on a single line?](http://stackoverflow.com/q/4166785/2890716)

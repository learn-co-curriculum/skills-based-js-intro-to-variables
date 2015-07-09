# JavaScript Variables

## Overview

* About
* Local vs. Global Variables
* Declaring Variables
* Resources

## About

As in Ruby, variables in JavaScript are used to store information/data that will be used in our program.  A variable can point to almost any type of value including numbers, strings, arrays, and hashes.

In JavaScript, variables are assigned values using the `=` operator. Variable names are typically all lower case, and in the case of multiple words, the words are joined together using [lower camelCase](http://c2.com/cgi/wiki?LowerCamelCase).

## Local vs. Global Variables

You can declare a variable in two ways but each have different consequences:
- declaring a variable **using** the `var` keyword
  ```javascript
    var someLocalNumber = 10; // can only be accessed within the current scope
  ```
  <br>
- declaring a variable **without using** the `var` keyword

  ```javascript
    someGlobalNumber = 42; // is now window.someGlobalNumber and can be accessed anywhere
  ```

It is best to use the key word `var` before declaring a variable.  This ensures that the variable is set to the current scope.  If `var` is not used in defining a new variable it becomes global and is accessible throughout the program.  This happens because it becomes attached to the global object, which in most cases is `window`.

## Declaring Variables

Variables can also be declared, but not necessarily assigned a value.  The following two are equivalent:

```javascript
  someNumber  = 10; // declares a global variable and returns 10
  
  var someNumber = 10; // declares a non-global variable and returns 10
```
<br>
Variables can also be assigned at once with multiple lines, using commas to delimit each. You must terminate the assignment with a semicolon.
- ex:
  ```javascript
    var someVariable, someNumber = 10, aString = 'Hello World';
  ```

## Resources

* [MDN - Var Keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* [MSDN - Variable Scope](https://msdn.microsoft.com/library/bzt2dkta(v=vs.94).aspx)

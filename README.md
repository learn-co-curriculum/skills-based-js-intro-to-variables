# JavaScript Variables

## Objectives

- Declare a variable without assigning a value
- Declare and define a variable
- Explain multi-line variable assignment (with the comma operator!)
- Explain how local and global variables differ

## About

Variables in JavaScript are used to store data that will be used in our program. A variable can point to almost any type of value including numbers, strings, arrays, objects, and functions.

Variables are assigned values using the `=` operator. Variable names are typically all lower case; in the case of multiple words, the words are joined together using [lowerCamelCase](http://c2.com/cgi/wiki?LowerCamelCase).

## Declaring Variables

Lets say I have the variable `word`. We could, if we wanted to, write

``` javascript
word = 'bird'
```

in order to create our variable and assign it the value of the string `'bird'`. Thing is, now we've declared a _global variable_. Global variables can be accessed anywhere in an application, which can lead to strange behavior. What if, for example, we wanted `word`'s value to be something other than `'bird'` at some point in the application? Or what if we needed to make use of a variable called `word` but not _this particular `word`_?

In the browser, global variables are all properties of `window`. What is `window`? Well, it's the — erm — window in which the browser displays the current page. It holds a whole bunch of things (which is probably obvious), global variables among them.

Clearly globals aren't the way to go.

### `var`

In the olden days (1995), JavaScript had one way to declare a non-global variable, `var`. Using the keyword `var` creates _local variable_, meaning that it is only accessible inside the current function in which it is declared. (If it's not declared inside a function, it's actually still global!)

Here's how this works — follow along in your console!

``` javascript
// declare the variable
var word;

// assign a value to the variable
word = 'bird';

console.log(word); // 'bird'

// assign another value to the variable
word = 'dog';

console.log(word) // 'dog'
```

Now we have declared a local variable `word`, and we can assign and reassign its value as we please.

We can perform variable declaration and assignment on the same line to save space:

``` javascript
var word = 'bird';
```

What does it mean that `word` is a local variable? Well, if we're just entering it in the console, not much — the variable still becomes a property of `window`, just like global variables (as mentioned above). (Go ahead, try typing `window.word` in the console — prepare to be amazed!)

But inside a function, things get more interesting. Variables in JavaScript have _function-level scope_, meaning that variables are bound to the function context in which they're declared. An example will make what we mean clearer.


``` javascript
function speaker() {
  var sentence = 'Bird is the word.';

  console.log(sentence)
}
```

If we call `speaker()` in console, we'll see `'Bird is the word.'` logged out — all is well. But if we call `console.log(sentence)` outside of the `speaker` function, we'll get an error — the variable `sentence` is _bound_ to the context of the function `speaker`.

If, however, we write

``` javascript
function speaker() {
  sentence = 'Bird is the word.';

  console.log(sentence);
```

and run `speaker()`, we can now call `console.log(sentence)` outside of the `speaker` function because we have declared the variable `sentence` without the `var` keyword — it's now a global variable.

## Multi-line Variable Assignment

Let's say I needed to declare and define multiple variables. It feels like a lot to have to repeat `var` over and over again. JavaScript allows us to do multi-line variable assignment to alleviate this pain. Every variable must be separated with a comma, and end the entire line must end with a semicolon.

Let's condense the below code into one line:

```javascript
var a = 5;
var b = 2;
var c = 3;
var d = 'hello';
var e = 'goodbye';
```

The above is equivalent to:

```javascript
var a = 5,
    b = 2,
    c = 3,
    d = 'hello',
    e = 'goodbye';
```

which can be converted to:

```javascript
var a = 5, b = 2, c = 3, d = 'hello', e = 'goodbye';
```

Try typing each variable in the console. You should see the appropriate values returned for each one.

Personally, we're of the opinion that it's best to declare each variable with its own `var` keyword. The comma fanciness saves a little bit of typing, but at the expense of nonstandard indentation (you're using two spaces, right?) and can introduce a bit of weirdness if we're doing anything other than simple assignment.

## Same Variable, Different Scopes

Keep in mind too that the same variable name used in different scopes is effectively a different variable. We sometimes refer to repeating a variable name in an inner scope as "shadowing" — it's best to avoid, as you'll quickly see how confusing it can be:

``` javascript
var cuteAnimal = 'quokka';

function makeVariable() {
  var cuteAnimal = 'sugar glider';
  return cuteAnimal;
}

makeVariable();
// 'sugar glider'

cuteAnimal;
// 'quokka'

```

See? Nothing breaks, but if you have a lot of shadowed variables (or even just a lot of space between a variable's initial declaration and its subsequent change(s)), you're gonna have a bad time.

## Changing Variable Values

Local variable assignment can overwrite global variable assignment:

```javascript
volume = 10; //declares a global variable called volume and sets it to 10

function returnEleven () {
  var volume = 11;  //declares a local variable called volume and sets it to 11
  return volume;
}

returnEleven(); // returns 11
volume; // the global variable is still 10

function goToEleven(){
  volume = 11;  //changes the global variable to 11
  return volume;
}

goToEleven(); // returns 11
volume; // the global variable volume has been changed to 11
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

## Resources

* [MDN - Var Keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* [MSDN - Variable Scope](https://msdn.microsoft.com/library/bzt2dkta(v=vs.94).aspx)
* [StackOverflow - How to define multiple variables on a single line?](http://stackoverflow.com/q/4166785/2890716)
* [You Don't Know JS - Function vs. Block Scope](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch3.md)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/intro-to-variables.js'>Intro To Variables in JS</a> on Learn.co and start learning to code for free.</p>

# JavaScript Variables

## Objectives
+ Declare a variable without assigning a value
+ Declare and define a variable
+ multi-line variable assignment
+ Explain how local and global variables differ


## About

Variables in JavaScript are used to store data that will be used in our program.
A variable can point to almost any type of value including numbers, strings,
arrays, objects, and functions.

Variables are assigned values using the `=` operator. Variable names are
typically all lower case; in the case of multiple words, the words are joined
together using [lowerCamelCase](http://c2.com/cgi/wiki?LowerCamelCase).

## Declaring Variables

Lets say I have the variable `word`. We could, if we wanted to, write

``` javascript
word = 'bird'
```

in order to create our variable and assign it the value of the string `'bird'`.
Thing is, now we've declared a _global variable_. Global variables can be
accessed anywhere in an application, which can lead to strange behavior. What
if, for example, we wanted `word`'s value to be something other than `'bird'`
at some point in the application? Or what if we needed to make use of a variable
called `word` but not _this particular `word`_?

Clearly globals aren't the way to go.

### `var`

In the olden days (1995), JavaScript had one way to declare a non-global
variable: `var`. Using the keyword `var` binds the variable to the _local
scope_, so we might as well call it a _"local variable."_

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

Now we have declared a local variable `word`, and we can assign and reassign its
value as we please.

We can perform variable declaration and assignment on the same line to save
space:

``` javascript
var word = 'bird';
```

What does it mean that `word` is a local variable? Well, if we're just entering
it in the console, not much — the variable still becomes a property of `window`,
just like global variables. (Go ahead, try typing `window.word` in the console —
prepare to be amazed!)

But inside a function, things get more interesting. (Don't worry, we'll go over
functions in more detail soon.) Variables in JavaScript have _function-level
scope_, meaning that variables are bound to the function context in which they're
declared. An example will make what we mean clearer:

``` javascript
function speaker() {
  var sentence = 'Bird is the word.';

  console.log(sentence)
}
```

If we call `speaker()` in console, we'll see `'Bird is the word.'` logged out — all
is well. But if we call `console.log(sentence)` outside of the `speaker` function,
we'll get an error — the variable `sentence` is _bound_ to the context of the
function `speaker`.

If, however, we write

``` javascript
function speaker() {
  sentence = 'Bird is the word.';

  console.log(sentence);
```

and run `speaker()`, we can now call `console.log(sentence)` outside of the `speaker`
function because we have declared the variable `sentence` without the `var` keyword —
it's now a global variable.

### `const`

ECMAScript 6 introduces the [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) keyword.
MDN defines this keyword:

> The *`const` declaration* creates a read-only reference to a value. It does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned.

``` javascript
const tryToChangeMe = 'foo';

tryToChangeMe = 'bar'; // error!

const notImmutable = {};

notImmutable.prop = 'change!';

console.log(notImmutable); // includes `prop`
```

Additionally, variables declared with `const` are block-scoped — you can read more
about the distinction between function- and block-scope [here](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch3.md).

### `let`

ECMAScript 6 also makes `let` official. The `let` keyword behaves essentially like
`var`, with the important distinction of making the variable block-scoped.

## Multi-line Variable Assignment

Let's say I needed to declare and define multiple variables. It feels like a lot to have to repeat `var` over and over again. JavaScript allows us to do multi-line variable assignment to alleviate this pain. Every variable must be separated with a comma, and end the entire line must end with a semicolon.

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
var a = 5,
    b = 2,
    c = 3,
    d = {},
    e = [];
```

which can be converted to:

```javascript
var a = 5, b = 2, c = 3, d = {}, e = [];
```

Try returning each variable in the console. You should see the appropriate values returned for each one.

Some people prefer to keep new lines between each new variable assignment, other people like the look of the single line. Whichever way you swing, the important thing to remember is [to use commas to separate each variable](http://stackoverflow.com/a/4166789/2890716).

## Same Variable, Different Scopes

Keep in mind too that the same variable name used in different scopes is effectively a different variable.
We sometimes refer to repeating a variable name in an inner scope as "shadowing" — it's best to avoid,
as you'll quickly see how confusing it can be:

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

See? Nothing breaks, but if you have a lot of shadowed variables (or even just a lot of space between a
variable's initial declaration and its subsequent change(s)), you're gonna have a bad time.

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

## Function Expressions

What, what's a section on functions doing in this variables lesson? Well, prepare for a mind-blowing revelation.

![kapow](http://i.giphy.com/OK27wINdQS5YQ.gif)

You can assign functions as a value to variables. This means that we can take this

``` javascript
function square(number) {
  return number * number
}
```

and combine it with this

``` javascript
const square // or `var square` or `let square`
```

to get this

``` javascript
const square = function square(number) {
  return number * number
}
```

Typically, we'll omit the name from the function in this case, because in this simple case JavaScript will pick up the name of the variable:

``` javascript
const square = function(number) {
  return number * number
}
```

But, as you can read about [here](https://kangax.github.io/nfe/#named-expr), sometimes giving the function in a function expression an identifier can be a good idea.

## Resources

* [MDN - Var Keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* [MSDN - Variable Scope](https://msdn.microsoft.com/library/bzt2dkta(v=vs.94).aspx)
* [StackOverflow - How to define multiple variables on a single line?](http://stackoverflow.com/q/4166785/2890716)
* [You Don't Know JS - Function vs. Block Scope](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch3.md)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/intro-to-variables.js'>Intro To Variables in JS</a> on Learn.co and start learning to code for free.</p>

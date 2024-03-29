# JavaScript Variables

## Objectives

- Explain how variables are tied to their contexts
- Explain how local and global variables differ

## Introduction

In JavaScript, variables become global when they aren't declared with the `var`
keyword. The story is actually a little bit more interesting.

Think of variables as notes on pieces of paper. Local variables are written
normally, maybe on a post-it — they're for one person to see. Global variables,
contrastingly, are written on billboards in big, bold letters — they're for
everyone to see!

Variables in JavaScript have _function-level scope_, meaning that variables are
bound to the function context in which they're declared. An example will make
what we mean clearer.

```javascript
function speaker() {
  var sentence = 'Bird is the word.';

  console.log(sentence);
}
```

Above is an example of a _local_ variable - it is defined within a function and
will not be accessible outside of the function.

If we call `speaker()` in console, we'll see `'Bird is the word.'` logged out —
all is well. But if we call `console.log(sentence)` outside of the `speaker`
function, we'll get an error — the variable `sentence` is _bound_ to the context
of the function `speaker`.

If, however, we write

```javascript
function speaker() {
  sentence = 'Bird is the word.';
}

speaker();
console.log(sentence);
```

and run `speaker()`, we can now call `console.log(sentence)` outside of the
`speaker` function because we have declared the variable `sentence` without the
`var` keyword — it's now a global variable.

## Same Variable, Different Scopes

Keep in mind too that the same variable name used in different scopes is
effectively a different variable. We sometimes refer to repeating a variable
name in an inner scope as "shadowing" — it's best to avoid, as you'll quickly
see how confusing it can be:

```javascript
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

See? Nothing breaks, but if you have a lot of shadowed variables (or even just a
lot of space between a variable's initial declaration and its subsequent
change(s)), you're gonna have a bad time.

## Changing Variable Values

Local variable assignment can overwrite global variable assignment:

```javascript
volume = 10; //declares a global variable called volume and sets it to 10

function returnEleven() {
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

Notice that in the first function above, a local variable, `var volume` is
declared and assigned to `11`, but the global `volume` remains unchanged.

However, in the _second_ function, the `volume` variable does not have `var` in
front of it. JavaScript considers this to be a reassignment of the  existing
`volume` global variable. The result is that the global `volume` variable gets
reassigned.

Moving in the opposte direction, global variable assignment cannot overwrite
local variable assignment, rather it simply reassigns the value of the local
variable:

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

Since `greeting = "hello"` is in the same scope and follows
`var greeting = "hola"` in sequence, JavaScript understands this to be a
reassignment of the local `greeting` variable.

## Resources

* [MDN - Var Keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* [MSDN - Variable Scope](https://msdn.microsoft.com/library/bzt2dkta(v=vs.94).aspx)
* [StackOverflow - How to define multiple variables on a single line?](http://stackoverflow.com/q/4166785/2890716)
* [Function vs. Block Scope](https://medium.com/@josephcardillo/the-difference-between-function-and-block-scope-in-javascript-4296b2322abe)

<p class='util--hide'>View <a href='https://learn.co/lessons/skills-based-js-intro-to-variables'>Variables</a> on Learn.co and start learning to code for free.</p>
